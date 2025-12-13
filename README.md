

# Automotive ECU Security

This repository demonstrates **automotive cybersecurity concepts** using practical examples
focused on **Electronic Control Units (ECUs)**.

The intent of this repository is to show **how security reasoning (TARA) translates into
implementation-level concepts** such as Secure Onboard Communication (SecOC) and Secure Flashing,
without relying on OEM-specific or proprietary code.

---

## What this repository covers

- **Threat Analysis and Risk Assessment (TARA)**  
  A system-level cybersecurity analysis aligned with ISO/SAE 21434 concepts, identifying assets,
  threat scenarios, risks, and security goals.

- **Secure Onboard Communication (SecOC)**  
  Demonstrates message authentication and integrity protection for ECU communication.

- **Secure Flash / Firmware Integrity**  
  Demonstrates firmware integrity verification using cryptographic hashing before flashing.

---

## Repository Structure

```

Automotive-ECU-Security/
│
├── README.md
│
├── SecOC/
│   ├── secoc_demo.c
│   └── SecOc_README.txt
│
├── Secure_Flash/
│   ├── secure_flash.c
│   └── Secure_Flash_README.txt
│
├── TARA/
│   ├── TARA_README.md
│   └── TARA_Example.xlsx
│
└── LICENSE

````

---

## Module Overview

### TARA (Threat Analysis and Risk Assessment)
The `TARA/` folder contains:
- A concise **TARA overview** describing assets, threat scenarios, risk evaluation, and security goals
- An **example TARA Excel sheet** used as the basis for the analysis

The TARA is used to **justify why specific security mechanisms are needed**, rather than adding
security features arbitrarily.

---

### Secure Onboard Communication (SecOC)
The `SecOC/` folder demonstrates:
- Message authentication and integrity protection concepts
- MAC generation and verification using cryptographic primitives
- Conceptual mapping to **AUTOSAR Crypto Stack services (CSM / CryIf)**

This module focuses on **protecting in-vehicle communication against spoofing and manipulation**.

---

### Secure Flash / Firmware Integrity
The `Secure_Flash/` folder demonstrates:
- Firmware integrity verification using **SHA-256 hashing**
- Blocking of unauthorized or tampered firmware before flashing
- Conceptual mapping to **AUTOSAR hash services**

This module focuses on **preventing unauthorized software updates** on ECUs.

---

## Scope and Intent

- Implementations use **OpenSSL** to demonstrate cryptographic primitives
- AUTOSAR API names and behavior are **vendor-dependent**
- The repository focuses on **conceptual understanding and security reasoning**
- This is **not an OEM production implementation**

---

## Requirements

- **OpenSSL** library
- **C compiler** with OpenSSL support

---

## Build and Run Example

```bash
gcc -o secure_flash Secure_Flash/secure_flash.c -lssl -lcrypto
./secure_flash
````

Refer to the individual module README files for detailed build and usage instructions.

---

## Notes

* This repository is intended for **learning and demonstration purpose only**
* No proprietary standards or OEM code are reproduced
* Security decisions are driven by **risk analysis (TARA)** rather than implementation convenience

---

## License

This project is licensed under the terms specified in the `LICENSE` file.
```

