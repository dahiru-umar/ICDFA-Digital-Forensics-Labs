# CIP-B105 Case Study II: Email Harassment Attribution Investigation

## Overview
This repository contains the completed submission for **CIP-B105 – Computer Forensics Case Study II** at the **International Cybersecurity and Digital Forensics Academy (ICDFA)**.

The project investigates an email harassment incident through forensic analysis of a historical network packet capture. Using industry-standard digital forensic methodologies and network analysis tools, the investigation reconstructs user activity, recovers relevant communications, and develops an evidence-based attribution chain.

---

## Student Information

| Field | Details |
|---------|---------|
| Student Name | Dahiru Abdulwahid Umar |
| Registration Number | C11/26/DFIT/17283 |
| Programme |  Digital Forensics  |
| Course | CIP-B105 – Computer Forensics Case Study II |

---

## Investigation Objectives

The primary objectives of this case study were to:

- Preserve and validate evidential integrity.
- Characterize the captured network traffic.
- Reconstruct user interactions with the target website.
- Recover and analyze HTTP POST submissions.
- Identify the originating client IP and MAC address.
- Examine identity-bearing artifacts within captured traffic.
- Establish a defensible packet-level attribution chain.
- Reconstruct the incident timeline in Coordinated Universal Time (UTC).
- Evaluate attribution confidence, assumptions, and investigative limitations.

---

## Methodology

The investigation followed a structured digital forensic workflow:

1. Evidence acquisition and integrity verification.
2. Packet capture profiling and protocol analysis.
3. Endpoint identification and TCP conversation analysis.
4. Website workflow reconstruction.
5. HTTP POST request recovery and examination.
6. Client IP and MAC address attribution.
7. Identity artifact discovery and analysis.
8. Timeline reconstruction in UTC.
9. Attribution matrix development.
10. Reporting and documentation.

---

## Repository Structure

```text
CIP-B105-CS2/
├── Report/
├── Documentation/
├── Evidence/
├── Output/
├── Screenshots/
├── Submission/
└── README.md
```

---

## Tools and Environment

The following tools were used during the investigation:

- Ubuntu Linux
- Wireshark 4.6.4
- TShark 4.6.4
- Capinfos
- md5sum
- sha256sum
- GNU Bash

---

## Primary Evidence

| Evidence Item | Description |
|--------------|-------------|
| nitroba.pcap | Historical packet capture used for forensic analysis |

---

## Key Findings

The investigation successfully:

- Reconstructed network activity associated with **www.willselfdestruct.com**.
- Recovered and analyzed the relevant HTTP POST request.
- Identified the originating client IP address and MAC address.
- Recovered identity-bearing browser artifacts, including a Gmail cookie artifact.
- Reconstructed a detailed UTC-based incident timeline.
- Documented investigative limitations, including unavailable supporting records.

---

## Repository Contents

- Investigation Report
- Activity Log
- Evidence Register
- UTC Timeline
- Hash Verification Records
- Commands Executed
- Analysis Output Files
- Supporting Screenshots

---

## Learning Outcomes

This case study demonstrates practical application of:

- Network forensics
- Packet analysis
- Evidence preservation
- Digital attribution methodology
- Timeline reconstruction
- Investigative reporting
- Forensic documentation standards

---

## Academic Integrity Statement

This repository was developed solely for academic assessment purposes using historical training data provided as part of the course curriculum.

No live systems were accessed, targeted, or interacted with during this investigation. All analysis was conducted in a controlled educational environment following accepted digital forensic principles and ethical guidelines.

---

## Author

**Dahiru Abdulwahid Umar**  
Registration Number: **C11/26/DFIT/17283**  
International Cybersecurity and Digital Forensics Academy (ICDFA)

---

## License

This repository is intended for educational and academic demonstration purposes only unless otherwise specified.
