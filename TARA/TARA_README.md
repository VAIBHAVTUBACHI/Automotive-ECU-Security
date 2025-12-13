# Threat Analysis and Risk Assessment (TARA)

## What this is about

This document summarizes a **Threat Analysis and Risk Assessment (TARA)** performed on selected
automotive ECUs to understand cybersecurity risks and define suitable mitigation directions.

The analysis follows the **conceptual approach of ISO/SAE 21434**, focusing on practical reasoning
rather than compliance documentation.

---

## System in Scope

The system represents a connected vehicle architecture with multiple ECUs communicating over
in-vehicle networks and external interfaces.

The primary components considered are:
- **Telematics Control Unit (TCU)** – externally connected ECU
- **Central Zone Computer (HPC-CZC)** – central control and communication hub
- Interfaces such as **OBD, CAN, Ethernet, and network services**

These components were selected due to their **connectivity, exposure, and system influence**.

---

## Assets Considered

| Asset | Asset ID |
|------|---------|
| TCU | TARA:TCU:001, TARA:TCU:002 |
| HPC-CZC | TARA:HPCCZC:002 |

The analysis focuses on **confidentiality, integrity, and availability** of these assets.

---

## Key Threat Scenarios

### TCU – Network-based attacks
- Compromised application-layer protocol used to access the TCU
- Unauthorized control of vehicle functions (e.g., remote start, climate control)

**Possible impact:**
- Vehicle unavailability
- Driver distraction during operation

---

### HPC-CZC – Local attack
- Impersonation of HPC-CZC via internal Ethernet access

**Possible impact:**
- Manipulation of central ECU functions
- Cascading effects on dependent ECUs

---

## Impact and Feasibility Summary

- **Impact rating:** Severe  
  (mainly due to safety and operational consequences)

- **Attack feasibility:** Low to Very Low  
  (requires expertise, access, and favorable conditions)

---

## Risk Handling Approach

- Risks with **very low feasibility** are **retained**
- Higher-priority risks are **reduced** using technical mitigations

This ensures focus on **realistic and meaningful risks**.

---

## Security Goals and Direction

Derived security goals include:
- Protect integrity and confidentiality of in-vehicle communication
- Prevent unauthorized ECU control
- Detect impersonation or message manipulation

To achieve these goals, the following concepts are applied:
- Secure communication mechanisms
- Message authentication and integrity protection (**SecOC**)

Assigned **Cybersecurity Assurance Levels (CAL)**:
- CAL 3
- CAL 4

---

## Link to Practical Examples

The security concepts identified in this TARA are demonstrated in this repository using:
- SecOC message authentication examples
- Secure Flash firmware integrity checks

These demos use **OpenSSL** and are **conceptually mapped to AUTOSAR Crypto Stack services**.

---

## Notes

- This TARA covers selected assets and scenarios only
- It is intended for learning and demonstration
- It does not represent an OEM production TARA
