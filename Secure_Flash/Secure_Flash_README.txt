---

Secure Flashing with SHA-256 Verification

This repository demonstrates a secure flashing mechanism that verifies firmware integrity using SHA-256 hashing before allowing a flash operation.
The goal is to ensure that only authentic and untampered firmware images are accepted, preventing corrupted or malicious software from being flashed onto the device.

---

KEY FEATURES

* SHA-256 Integrity Verification
  Uses OpenSSL EVP digest APIs to compute cryptographic hashes of firmware images.

* Pre-Flash Validation
  Compares the calculated firmware hash against a trusted reference hash before flashing.

* Tamper Detection
  Automatically blocks the flash operation if the firmware image has been modified or corrupted.

---

SECURE FLASH FLOW

Firmware / Image File
|
| 1) Digest Init   (EVP_DigestInit_ex)
| 2) Read chunk -> Digest Update (EVP_DigestUpdate) [repeated]
| 3) Digest Final  (EVP_DigestFinal_ex -> SHA-256 hash)
v
Computed Hash  -------------------->  Compare with Expected / Reference Hash
|
|-- MATCH     -> Allow Flash
|-- MISMATCH  -> Block Flash

---

HOW IT WORKS

1. The firmware image is read and hashed using the SHA-256 algorithm.
2. The calculated hash is compared with a stored reference hash.
3. If both hashes match, the firmware is considered authentic and flashing is allowed.
4. If the hashes differ, the flashing process is aborted to prevent tampering.

---

CODE OVERVIEW

* Hash Computation and Verification
  The verify_sha256() function computes the SHA-256 hash using OpenSSL EVP_DigestInit,
  EVP_DigestUpdate, and EVP_DigestFinal APIs.

* Reference Hash
  The stored_hash represents a known-good hash of a legitimate firmware image and is
  used for comparison.

---

EXAMPLE OUTPUT

Valid Firmware (Hash Match)

Calculated hash is:
A3 7F 2C D9 4B 1E 88 6A F0 3D B7 5C 9A 0E 14 C2
6D E1 93 AF 78 05 39 CB 12 8F DA 47 60 BE 25 91

Stored hash is:
A3 7F 2C D9 4B 1E 88 6A F0 3D B7 5C 9A 0E 14 C2
6D E1 93 AF 78 05 39 CB 12 8F DA 47 60 BE 25 91

HASH MATCHED - PROCEEDING TO FLASH THE SOFTWARE

Tampered Firmware (Hash Mismatch)

HASH MISMATCH - FLASH OPERATION BLOCKED

---

AUTOSAR CONCEPTUAL MAPPING

This implementation demonstrates cryptographic primitives using OpenSSL.
In production AUTOSAR Classic systems, similar functionality is typically
provided via the AUTOSAR Crypto Stack (CSM / CryIf).

## OpenSSL API (This Repo)          AUTOSAR Crypto Stack (Typical)         Purpose

EVP_DigestInit_ex()              Csm_HashStart(jobId)                  Initialize hash calculation
EVP_DigestUpdate()               Csm_HashUpdate(jobId, data, length)   Stream firmware data
EVP_DigestFinal_ex()             Csm_HashFinish(jobId, hash, length)   Finalize hash and output digest
Application hash comparison      Application logic / Secure Boot       Allow or block flashing

Note: AUTOSAR API names and behavior may vary depending on the vendor implementation.

---

REQUIREMENTS

* OpenSSL library
* C compiler with OpenSSL support

---

BUILD AND RUN

Install OpenSSL (Windows):

* Download OpenSSL from the official website
* Add OpenSSL to system PATH
* Verify installation using:
  openssl version

Compile:
gcc -o secure_flash secure_flash.c -lssl -lcrypto

Run:
./secure_flash

---

IMPORTANT NOTES

* This project demonstrates firmware integrity verification only.
* It does not implement a full OEM bootloader.
* Production secure flashing typically integrates secure boot,
  key storage or HSM, and digital signature verification.

---
