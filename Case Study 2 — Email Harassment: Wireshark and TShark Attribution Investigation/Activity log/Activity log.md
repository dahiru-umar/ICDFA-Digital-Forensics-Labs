# CIP-B105 – Computer Forensics Case Study II

# Investigation Activity Log

## Case Study 2 – Email Harassment: Wireshark and TShark Attribution Investigation

---

## Student Information

| Item | Details |
|------|---------|
| **Student Name** | Dahiru Abdulwahid Umar |
| **Registration Number** | C11/26/DFIT/17283 |
| **Programme** | Diploma in Digital Forensics and Incident Response (DFIT) |
| **Institution** | International Cybersecurity and Digital Forensics Academy (ICDFA) |
| **Course** | CIP-B105 – Computer Forensics Case Study II |
| **Case Study** | Case Study 2 |
| **Evidence** | `nitroba.pcap` |

---

# Purpose

This activity log documents the chronological sequence of forensic actions performed during the investigation. It provides an auditable record of the tools, commands, evidence, screenshots, and outputs generated throughout the examination while preserving the chain of custody.

---

# Investigation Activity Log

| Step | Date | Time | Examiner | Investigation Activity | Tool / Command | Evidence ID | Output Produced | Screenshot | Chain of Custody |
|------|------|------|----------|------------------------|----------------|-------------|-----------------|------------|------------------|
| 1 | 17 Sept 2026 | Investigation Start | Dahiru Abdulwahid Umar | Created investigation workspace | Ubuntu Linux | EV-001 | Working directory | — | COC-001 |
| 2 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Extracted supplied evidence | `unzip` | EV-001 | Original evidence | — | COC-001 |
| 3 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Created working copy | `cp` | EV-002 | Working PCAP | — | COC-002 |
| 4 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Generated MD5 hash | `md5sum` | EV-003 | md5.txt | Fig. 4.1 | COC-003 |
| 5 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Generated SHA-256 hash | `sha256sum` | EV-004 | sha256.txt | Fig. 4.1 | COC-003 |
| 6 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Examined capture summary | `capinfos` | EV-005 | Capture summary | Fig. 4.1 | COC-004 |
| 7 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Generated protocol hierarchy | `tshark -z io,phs` | EV-006 | protocol_hierarchy.txt | Fig. 5.1 | COC-005 |
| 8 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Generated IPv4 endpoint summary | `tshark -z endpoints,ip` | EV-007 | ip_endpoints.txt | Fig. 5.1 | COC-005 |
| 9 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Generated Ethernet endpoint summary | `tshark -z endpoints,eth` | EV-008 | mac_endpoints.txt | Fig. 5.4 | COC-005 |
| 10 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Generated TCP conversations | `tshark -z conv,tcp` | EV-009 | tcp_conversations.txt | Fig. 5.2 | COC-005 |
| 11 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Identified website traffic | `tshark` HTTP filter | EV-010 | Website workflow | — | COC-006 |
| 12 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Recovered HTTP POST | `tshark -V` | EV-011 | POST request | Fig. 5.3 | COC-007 |
| 13 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Extracted client IP | `tshark` | EV-012 | Source IP | Fig. 5.4 | COC-008 |
| 14 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Extracted client MAC | `tshark` | EV-013 | Source MAC | Fig. 5.4 | COC-008 |
| 15 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Examined browser identity artefacts | `tshark` | EV-014 | Gmail cookie | Fig. 5.5 | COC-009 |
| 16 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Compared recovered identity with supplied evidence | Manual examination | EV-015 | No Chemistry 109 roster located | — | COC-010 |
| 17 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Reconstructed UTC timeline | `tshark` | EV-016 | Timeline | Fig. 5.6 | COC-011 |
| 18 | 17 Sept 2026 | Investigation | Dahiru Abdulwahid Umar | Developed attribution matrix | Manual analysis | EV-017 | Attribution matrix | — | COC-012 |
| 19 | 17 Sept 2026 | Investigation End | Dahiru Abdulwahid Umar | Prepared final forensic report | Microsoft Word / Markdown | EV-018 | Final report | — | COC-013 |

---

# Investigation Outputs

The following artefacts were generated during the investigation.

| Output | Description |
|---------|-------------|
| md5.txt | MD5 integrity verification |
| sha256.txt | SHA-256 integrity verification |
| protocol_hierarchy.txt | Protocol hierarchy analysis |
| ip_endpoints.txt | IPv4 endpoint analysis |
| mac_endpoints.txt | Ethernet endpoint analysis |
| tcp_conversations.txt | TCP conversation analysis |
| Investigation_Report.docx | Final report |
| Investigation_Report.pdf | Final report (PDF) |
| Evidence_Report.md | GitHub Markdown report |
| README.md | Repository overview |

---

# Evidence Integrity

Evidence integrity was maintained throughout the investigation by:

- Preserving the original packet capture.
- Performing all analysis on a working copy.
- Verifying integrity using MD5 and SHA-256 cryptographic hashes.
- Recording every significant investigative action within this activity log.

---

# Chain of Custody Summary

| Chain of Custody ID | Description |
|---------------------|-------------|
| COC-001 | Original evidence received and preserved |
| COC-002 | Working copy created |
| COC-003 | Cryptographic integrity verified |
| COC-004 | Capture metadata documented |
| COC-005 | Network analysis completed |
| COC-006 | Website workflow reconstructed |
| COC-007 | HTTP POST recovered |
| COC-008 | Client IP and MAC attributed |
| COC-009 | Browser artefacts examined |
| COC-010 | Supporting evidence reviewed |
| COC-011 | Timeline reconstructed |
| COC-012 | Attribution matrix prepared |
| COC-013 | Final report completed |

---

# Activity Log Summary

The investigation followed a structured forensic methodology from evidence preservation through reporting. Each analytical stage was documented and supported by reproducible command-line output, ensuring transparency, repeatability, and evidential integrity throughout the examination.

---

## Author

**Dahiru Abdulwahid Umar**

**Registration Number:** C11/26/DFIT/17283

**International Cybersecurity and Digital Forensics Academy (ICDFA)**

---

**End of Activity Log**
