# CIP-B105 – Computer Forensics Case Study II

# Evidence Register

## Case Study 2 – Email Harassment: Wireshark and TShark Attribution Investigation

---

## Student Information

| Item | Details |
|------|---------|
| **Student Name** | Dahiru Abdulwahid Umar |
| **Registration Number** | C11/26/DFIT/17283 |
| **Programme** |  Digital Forensics |
| **Institution** | International Cybersecurity and Digital Forensics Academy (ICDFA) |
| **Course** | CIP-B105 – Computer Forensics Case Study II |
| **Case Study** | Case Study 2 |

---

# Purpose

The Evidence Register documents every evidential item acquired, generated, or referenced during the investigation. It provides a structured inventory of digital evidence, analytical outputs, and supporting documentation while maintaining traceability throughout the forensic examination.

---

# Evidence Register

## Table 1. Primary Evidence

| Evidence ID | Evidence Description | Source | Acquisition Method | Integrity Verification | Status |
|-------------|----------------------|--------|--------------------|------------------------|--------|
| EV-001 | `nitroba.pcap` | Supplied case material | Extracted from supplied archive | MD5 & SHA-256 verified | Examined |

---

## Table 2. Working Evidence

| Evidence ID | Description | Purpose | Status |
|-------------|-------------|---------|--------|
| EV-002 | Working copy of `nitroba.pcap` | Forensic analysis | Examined |

---

## Table 3. Integrity Verification

| Evidence ID | File | Verification Method | Output File | Status |
|-------------|------|---------------------|-------------|--------|
| EV-003 | Original packet capture | MD5 | `Documentation/Hashes/md5.txt` | Verified |
| EV-004 | Original packet capture | SHA-256 | `Documentation/Hashes/sha256.txt` | Verified |

---

## Table 4. Network Analysis Outputs

| Evidence ID | Output File | Description | Generated Using |
|-------------|-------------|-------------|-----------------|
| EV-005 | `protocol_hierarchy.txt` | Protocol hierarchy statistics | TShark |
| EV-006 | `ip_endpoints.txt` | IPv4 endpoint summary | TShark |
| EV-007 | `mac_endpoints.txt` | Ethernet endpoint summary | TShark |
| EV-008 | `tcp_conversations.txt` | TCP conversation summary | TShark |

---

## Table 5. Packet-Level Evidence

| Evidence ID | Description | Supporting Frame(s) | Status |
|-------------|-------------|---------------------|--------|
| EV-009 | HTTP website reconstruction | 82936, 83601, 83614 | Verified |
| EV-010 | HTTP POST request | 83601 | Recovered |
| EV-011 | Submitted message | 83601 | Recovered |
| EV-012 | Source IP address | 83601 | Identified |
| EV-013 | Source MAC address | 83601 | Identified |
| EV-014 | Browser identity artefact (Gmail cookie) | Browser session | Recovered |
| EV-015 | UTC incident timeline | Multiple frames | Reconstructed |
| EV-016 | Packet-level attribution matrix | Combined evidence | Completed |

---

## Table 6. Supporting Documentation

| Evidence ID | Document | Purpose |
|-------------|----------|---------|
| DOC-001 | Investigation_Report.docx | Formal forensic report |
| DOC-002 | Investigation_Report.pdf | Submission copy |
| DOC-003 | Evidence_Report.md | GitHub investigation report |
| DOC-004 | Activity_Log.md | Investigation activity log |
| DOC-005 | Commands_Executed.txt | Command history |
| DOC-006 | README.md | Repository overview |

---

## Table 7. Screenshot Evidence

| Figure | Screenshot File | Description |
|---------|----------------|-------------|
| Figure 4.1 | `Fig_4_1_Evidence_Integrity_and_Capture_Summary.png` | Evidence integrity verification and capture summary |
| Figure 5.1 | `Fig_5_1_Protocol_Hierarchy_and_IPv4_Endpoints.png` | Protocol hierarchy and IPv4 endpoints |
| Figure 5.2 | `Fig_5_2_TCP_Conversations.png` | TCP conversation analysis |
| Figure 5.3 | `Fig_5_3_HTTP_POST_and_Recovered_Form_Fields.png` | HTTP POST request and recovered form fields |
| Figure 5.4 | `Fig_5_4_Client_IP_and_MAC_Attribution.png` | Client IP and MAC attribution |
| Figure 5.5 | `Fig_5_5_Gmail_Cookie_Identity_Attribution.png` | Browser identity artefact |
| Figure 5.6 | `Fig_5_6_Incident_Timeline_and_Service_Usage.png` | UTC incident timeline |

---

# Evidence Relationships

The investigation established the following evidential chain:

```text
EV-001 (Original Packet Capture)
          │
          ▼
EV-002 (Working Copy)
          │
          ▼
Integrity Verification
(MD5 / SHA-256)
          │
          ▼
Protocol Analysis
          │
          ▼
Endpoint Analysis
          │
          ▼
HTTP Reconstruction
          │
          ▼
Recovered HTTP POST
(Frame 83601)
          │
          ▼
Client IP
192.168.15.4
          │
          ▼
Client MAC
00:17:f2:e2:c0:ce
          │
          ▼
Browser Identity Artefact
(Gmail Cookie)
          │
          ▼
UTC Timeline
          │
          ▼
Attribution Matrix
```

---

# Evidence Integrity

The integrity of the primary evidence was preserved throughout the investigation by:

- Preserving the original packet capture in the **Original** evidence directory.
- Conducting all forensic analysis on a dedicated working copy.
- Verifying integrity using MD5 and SHA-256 cryptographic hash functions.
- Recording all generated outputs separately from the original evidence.

No modification was made to the original evidence during the investigation.

---

# Chain of Custody Summary

| Chain of Custody ID | Description | Status |
|---------------------|-------------|--------|
| COC-001 | Evidence received | Completed |
| COC-002 | Working copy created | Completed |
| COC-003 | Integrity verified | Completed |
| COC-004 | Analysis completed | Completed |
| COC-005 | Investigation documented | Completed |

---

# Evidence Register Summary

A total of **16 evidential items** and **6 supporting documents** were generated or examined during the investigation. Each artefact contributed to the reconstruction of the anonymous messaging workflow, attribution of the originating client device, and production of the final forensic report. The register provides traceability between the original evidence, analytical outputs, screenshots, and documentation while maintaining evidential integrity throughout the examination.

---

## Author

**Dahiru Abdulwahid Umar**

**Registration Number:** C11/26/DFIT/17283

**Programme:** Diploma in Digital Forensics and Incident Response (DFIT)

**International Cybersecurity and Digital Forensics Academy (ICDFA)**

---

**End of Evidence Register**
