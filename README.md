# Automotive Cybersecurity

This repository focuses on enhancing cybersecurity within automotive systems, particularly in
Electronic Control Units (ECUs). The main goal is to protect **in-vehicle communication** and
**software integrity** to prevent unauthorized access, manipulation, and tampering.

The repository combines **threat analysis** with **practical security demonstrations** to show
how cybersecurity concepts translate into real ECU-level implementations.

---

## Features

- **Threat Analysis and Risk Assessment (TARA)**  
  Performs a system-level cybersecurity risk analysis aligned with ISO/SAE 21434 concepts,
  identifying assets, threat scenarios, risks, and security goals.

- **Secure Flashing**  
  Verifies firmware integrity before flashing to ensure that only authentic software is installed
  on the ECU.

- **Secure Onboard Communication (SecOC)**  
  Demonstrates message authentication and integrity protection for data exchanged between ECUs.

- **Cryptographic Hashing**  
  Uses SHA-256 hashing for firmware integrity verification and secure communication concepts.

- **Tamper Detection**  
  Detects and blocks unauthorized software modification or message manipulation.

---

## Repository Structure

- `TARA/`
  - Contains Threat Analysis and Risk Assessment documentation and example analysis.
- `Secure_flash.c`  
  Implements secure flashing with SHA-256 verification.
- `SecOc.c`  
  Implements Secure Onboard Communication (SecOC) concepts.
- `Secure_Flash_README.md`  
  Documentation for the secure flashing implementation.
- `SecOc_README.txt`  
  Documentation for the SecOC implementation.

---

## Requirements

- **OpenSSL**  
  Required for cryptographic operations such as hashing and message authentication.
- **C Compiler**  
  A C compiler with OpenSSL support is required to build and run the examples.

---

## Usage

### Install OpenSSL (Windows)

- Download the OpenSSL installer from the official website:
  https://slproweb.com/products/Win32OpenSSL.html
- Install OpenSSL and ensure it is added to the system PATH.
- Verify installation:
  ```bash
  openssl version
````

### Compile

```bash
gcc -o secure_flash Secure_flash.c -lssl -lcrypto
```

### Run

```bash
./secure_flash
```

---

## Notes

* This repository demonstrates **automotive cybersecurity concepts**, not a full OEM production
  system.
* AUTOSAR API names and implementations may vary depending on the vendor.
* The focus is on understanding **security reasoning and architecture**, rather than compliance
  documentation.

---

Feel free to explore and modify the code for learning or experimentation purposes.

```


