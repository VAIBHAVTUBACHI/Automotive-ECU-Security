```md
# Secure CMAC with Freshness Value

This repository contains a **C implementation of a secure Message Authentication Code (CMAC)** generation and verification mechanism using the **OpenSSL 3.0 EVP_MAC API**.

The CMAC generation incorporates a **Freshness Value (FV)** to protect against **replay attacks**, aligning conceptually with **AUTOSAR SecOC** principles.

---

## ✨ Features

- **CMAC Generation**
  - Uses **AES-128-CBC** for CMAC computation.

- **CMAC Verification**
  - Verifies message integrity by recalculating and comparing CMAC tags.

- **Freshness Value (FV)**
  - Implements a **monotonic counter** to prevent replay attacks.

- **OpenSSL 3.0**
  - Uses the modern **EVP_MAC API** (provider-based crypto).

---

## 📁 Files Overview

### `SecOc.c`
Main C source file implementing CMAC generation, verification, and FV handling.

**Key Functions:**
- `GenerateCMAC`  
  Generates CMAC using AES-128-CBC and prepended Freshness Value.
- `VerifyCMAC`  
  Recalculates and verifies CMAC against received data.
- `generateFV`  
  Increments the monotonic Freshness Value.
- `verifyFV`  
  Validates that the received FV is newer and untampered.

---

## 🔁 Secure Communication Flow

```

Application Payload (PDU)
        |
        v
+---------------------------+
| Generate Freshness Value  |
| (Monotonic Counter)       |
+---------------------------+
        |
        v
+---------------------------+
| Construct Secured Data    |
| [FV || Payload]           |
+---------------------------+
        |
        v
+---------------------------+
| CMAC Generation           |
| - EVP_MAC_init            |
| - EVP_MAC_update(FV||PDU) |
| - EVP_MAC_final           |
+---------------------------+
        |
        v
+--------------------------------+
| Transmitted Frame              |
| [FV || Payload || CMAC Tag]    |
+--------------------------------+
        |
        v
        >>>>>>>>> Sent over Bus / Network >>>>>>>>>
        
Received Frame
[FV || Payload || CMAC Tag]
        |
        v
+---------------------------+
| Extract Fields            |
| - Freshness Value (FV)    |
| - Payload                 |
| - Received CMAC Tag       |
+---------------------------+
        |
        v
+---------------------------+
| Verify Freshness Value    |
| - FV > Last Stored FV ?   |
+---------------------------+
        |
        |---- NO ---->  ❌ Reject (Replay Detected)
        |
        v
+---------------------------+
| CMAC Recalculation        |
| - EVP_MAC_init            |
| - EVP_MAC_update(FV||PDU) |
| - EVP_MAC_final           |
+---------------------------+
        |
        v
+---------------------------+
| Compare CMAC Tags         |
| Calculated == Received ?  |
+---------------------------+
        |
        |---- NO ----> ❌ Reject (Integrity Failure)
        |
        v
+---------------------------+
| Accept Payload            |
| Update Stored FV          |
+---------------------------+
        |
        v
      ✅ PASS


````

---

## 📦 Dependencies

- **OpenSSL 3.0**
  - Required for EVP_MAC cryptographic operations.

Ensure OpenSSL is installed and properly linked during compilation.

---

## 🛠️ Compilation Instructions

Install OpenSSL development libraries:

```bash
sudo apt-get install libssl-dev
````

Compile the program:

```bash
gcc SecOc.c -o SecOc -lssl -lcrypto
```

---

## ▶️ Usage

### Run the Program

```bash
./SecOc
```

### Example Output (Valid Payload)

```bash
Generated CMAC: 97A8A4F5B51F8D3BFC463F22D4A95BBF
Freshness value is  1
CMAC verification successful
```

### Example Output (Tampered Payload)

```bash
Generated CMAC: 97A8A4F5B51F8D3BFC463F22D4A95BBF
Freshness value is  1
CMAC verification failed
```

---

## 🔧 Function Details

### `GenerateCMAC`

* Prepends Freshness Value to payload.
* Computes CMAC using AES-128-CBC.

### `VerifyCMAC`

* Recomputes expected CMAC.
* Compares against received tag.

### `generateFV`

* Increments and returns monotonic FV.

### `verifyFV`

* Ensures received FV is greater than last stored FV.
* Prevents replay attacks.

---

## 🔐 Comparison with AUTOSAR Crypto APIs

| OpenSSL (This Repo)                           | AUTOSAR Crypto Stack (Typical)                   | Description                                    |
| --------------------------------------------- | ------------------------------------------------ | ---------------------------------------------- |
| `EVP_MAC_init(ctx, key, keyLen, params)`      | `Csm_MacGenerateStart(jobId, …)`                 | Initializes MAC operation and internal context |
| `EVP_MAC_update(ctx, data, dataLen)`          | `Csm_MacGenerateUpdate(jobId, dataPtr, dataLen)` | Streams input data for MAC computation         |
| `EVP_MAC_final(ctx, outTag, &outLen, maxLen)` | `Csm_MacGenerateFinish(jobId, tagPtr, &tagLen)`  | Finalizes MAC and outputs authenticator/tag    |

> **Note:**
> This table demonstrates a **conceptual mapping** between OpenSSL cryptographic primitives and AUTOSAR Crypto Stack services.
> Exact API names, configuration, and behavior may vary by vendor.

---

## 📌 Notes

* Designed as a **learning and demonstration implementation**
* Aligns conceptually with **AUTOSAR SecOC**
* Suitable for **simulation, PoC, and security experimentation**

Feel free to modify and extend the implementation based on your deployment needs.


---



