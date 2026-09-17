# CIP-B105 – Computer Forensics Case Study II

# Case Study 2

# Email Harassment: Wireshark and TShark Attribution Investigation

---

## Student Information

| Item | Details |
|------|---------|
| **Student Name** | Dahiru Abdulwahid Umar |
| **Registration Number** | C11/26/DFIT/17283 |
| **Programme** |  Digital Forensics  |
| **Institution** | International Cybersecurity and Digital Forensics Academy (ICDFA) |
| **Course** | CIP-B105 – Computer Forensics Case Study II |
| **Submission** | Case Study 2 |
| **Investigation Type** | Network Forensic Investigation |
| **Evidence Type** | Historical Packet Capture (PCAP) |
| **Primary Evidence** | `nitroba.pcap` |

---

> **Academic Notice**
>
> This investigation was conducted exclusively for academic purposes using historical packet capture evidence supplied as part of the CIP-B105 assessment. All analysis was performed offline against the supplied evidence without interacting with live systems.

---

# Table of Contents

- [Executive Summary](#executive-summary)
- [1. Authority, Scope and Investigative Questions](#1-authority-scope-and-investigative-questions)
- [2. Evidence Inventory and Integrity Verification](#2-evidence-inventory-and-integrity-verification)
- [3. Tools, Versions and Methodology](#3-tools-versions-and-methodology)
- [4. Detailed Findings and Evidential Interpretation](#4-detailed-findings-and-evidential-interpretation)
- [5. Integrated UTC Timeline](#5-integrated-utc-timeline)
- [6. Packet-Level Attribution Matrix](#6-packet-level-attribution-matrix)
- [7. Alternative Explanations, Limitations and Confidence Assessment](#7-alternative-explanations-limitations-and-confidence-assessment)
- [8. Professional Conclusion](#8-professional-conclusion)
- [Appendices](#appendices)

---

# Executive Summary

This report presents the forensic investigation conducted for **CIP-B105 – Computer Forensics Case Study II**, involving the analysis of a historical packet capture associated with an anonymous email harassment incident. The objective of the investigation was to determine whether packet-level evidence could reconstruct the use of an anonymous messaging service and attribute the observed activity to the originating network device.

The investigation followed accepted digital forensic principles, beginning with evidence preservation and cryptographic integrity verification. MD5 and SHA-256 hash values were generated for the supplied packet capture before any analytical activities were undertaken. A separate working copy of the evidence was created to preserve the integrity of the original evidence throughout the investigation.

Network traffic was examined using Wireshark's command-line utilities, primarily **TShark** and **Capinfos**. Protocol hierarchy analysis, endpoint identification, TCP conversation analysis and HTTP inspection were performed to reconstruct the interaction with the anonymous messaging website **www.willselfdestruct.com**.

The analysis successfully reconstructed the complete interaction with the web service, including retrieval of the message submission page, recovery of the HTTP POST request, identification of the submitted anonymous message, reconstruction of the service workflow and retrieval of the confirmation page following successful submission.

Packet-level examination further identified the originating client IP address and associated Ethernet MAC address responsible for the HTTP POST transaction. Additional browser artefacts recovered from the supplied packet capture identified a Gmail Chat cookie associated with the client browser session, extending the attribution chain beyond simple network addressing.

An evidential timeline was reconstructed by normalising the packet timestamps into Coordinated Universal Time (UTC), enabling chronological reconstruction of the incident from initial webpage access through successful message submission.

The investigation also considered attribution limitations associated with evidence collected from a shared network environment. Although the supplied packet capture provided sufficient evidence to attribute the activity to a specific client device and browser session, the Chemistry 109 class roster referenced in the assessment instructions was not present within the supplied evidence package. Consequently, attribution to a named individual could not be completed using the available evidence alone.

Overall, the investigation demonstrates that packet-level forensic examination can effectively reconstruct web-based activity, recover application-layer artefacts and support evidence-based attribution while appropriately recognising the evidential limitations imposed by incomplete supporting material and shared network environments.

---

# 1. Authority, Scope and Investigative Questions

## 1.1 Authority

This examination was undertaken as part of the practical assessment requirements for **CIP-B105 – Computer Forensics Case Study II**. The investigation was conducted solely using the evidence supplied with the assessment and did not involve acquisition of additional evidence from external systems or live network environments.

---

## 1.2 Scope

The scope of this investigation was limited to forensic examination of the supplied packet capture evidence and associated supporting files provided with the assessment. Analysis focused exclusively on reconstructing the anonymous messaging activity associated with **www.willselfdestruct.com**, identifying the originating client device, recovering evidential artefacts and documenting findings supported directly by the supplied evidence.

Where supporting evidence referenced in the assessment instructions was unavailable, this limitation has been documented within the relevant sections of this report rather than supplemented through inference or speculation.

---

## 1.3 Investigative Questions

The investigation addressed the following questions:

1. Which client accessed **www.willselfdestruct.com**?
2. Was a HTTP POST request submitted?
3. Did the recovered POST contain evidence consistent with the reported harassment?
4. Which client IP address initiated the submission?
5. Which Ethernet MAC address was associated with the client?
6. Were any identity-bearing browser artefacts recovered?
7. Could the recovered identity be compared with the Chemistry 109 roster?
8. When did the relevant activity occur?
9. What packet-level evidence supports each attribution step?
10. What confidence can be assigned to the final attribution?

---

# 2. Evidence Inventory and Integrity Verification

## 2.1 Evidence Received

The primary evidence supplied for examination consisted of the following packet capture:

| Evidence ID | Description | Status |
|-------------|-------------|--------|
| EV-001 | `nitroba.pcap` | Primary Evidence |

Supporting packet captures supplied with the assessment were examined where relevant; however, the investigation findings presented within this report are based primarily upon the analysis of **nitroba.pcap**.

---

## 2.2 Evidence Preservation

Immediately following acquisition, the supplied archive was extracted without modification. The original packet capture was preserved within the **Original Evidence** directory, while all subsequent forensic examination was conducted exclusively on a separate working copy.

This approach ensured that the integrity of the original evidence remained unchanged throughout the investigation.

---

## 2.3 Integrity Verification

Evidence integrity was verified prior to analysis through generation of both MD5 and SHA-256 cryptographic hash values.

The generated hash values were retained within the case documentation and formed part of the documented chain of custody.

> **Figure 4.1**  
<img width="1097" height="710" alt="Fig_4_1_Evidence_Integrity_and_Capture_Summary" src="https://github.com/user-attachments/assets/58e8ada3-2227-481b-a034-81feac819038" />


The capture summary generated using **Capinfos** confirmed:

- Ethernet packet capture format
- Approximately 94,410 packets
- Capture duration of approximately 4 hours and 22 minutes
- Chronologically ordered packets
- No evidence of corruption within the supplied capture

---

# 3. Tools, Versions and Methodology

## 3.1 Forensic Environment

The investigation was conducted using the following software environment.

| Tool | Version | Purpose |
|------|---------|---------|
| Ubuntu Linux | Current | Analysis platform |
| Wireshark | 4.6.4 | Packet inspection |
| TShark | 4.6.4 | Command-line packet analysis |
| Capinfos | Included with Wireshark | Capture metadata |
| md5sum | GNU Coreutils | MD5 integrity verification |
| sha256sum | GNU Coreutils | SHA-256 integrity verification |
| GNU Bash | Shell | Command execution |

---

## 3.2 Investigation Methodology

The investigation followed a structured workflow consistent with accepted digital forensic practice.

1. Evidence preservation.
2. Cryptographic integrity verification.
3. Capture characterization.
4. Protocol hierarchy analysis.
5. Endpoint identification.
6. TCP conversation analysis.
7. Website workflow reconstruction.
8. HTTP POST recovery.
9. Client IP attribution.
10. Client MAC attribution.
11. Identity artefact analysis.
12. Timeline reconstruction.
13. Attribution matrix development.
14. Confidence assessment.
15. Reporting.

Each analytical stage was documented within the accompanying Activity Log and supported by reproducible command-line output.

# 4. Detailed Findings and Evidential Interpretation

## 4.1 Capture Scope, Protocols and Network Endpoints

Following integrity verification, the working copy of the supplied packet capture was examined to determine the capture scope, protocol distribution and participating network endpoints.

Protocol hierarchy analysis identified Ethernet as the link-layer protocol with IPv4 as the dominant network protocol. TCP accounted for the majority of network traffic, while HTTP represented the principal application-layer protocol relevant to the investigation. Other protocols such as DNS, TLS, SSDP, SIP, RTP and NTP were also present within the capture but were not directly related to the anonymous messaging activity.

### Figure 5.1 – Protocol Hierarchy and IPv4 Endpoints

<img width="1017" height="557" alt="ScreenshotsFig_5_1_Protocol_Hierarchy_and_IPv4_Endpoints" src="https://github.com/user-attachments/assets/d5318a05-c7bc-4605-af77-8473e3a77523" />


The IPv4 endpoint summary identified **192.168.15.4** as the principal internal client involved in the subsequent anonymous messaging activity. HTTP traffic associated with **www.willselfdestruct.com** was observed communicating with **69.25.94.22**, which was identified as the destination web server for the relevant service.

---

## 4.2 TCP Conversation Analysis

TCP conversation analysis was performed to identify persistent client-server communications and to establish the sessions associated with the anonymous messaging service.

### Figure 5.2 – TCP Conversations

<img width="1006" height="717" alt="Fig_5_2_TCP_Conversations" src="https://github.com/user-attachments/assets/3a6f9556-9730-4383-a92c-f38d6513edf1" />


Although numerous HTTP sessions were present within the packet capture, subsequent filtering isolated the conversation associated with **www.willselfdestruct.com**, enabling reconstruction of the complete website interaction.

---

## 4.3 Website Workflow Reconstruction

HTTP filtering identified communications directed to **www.willselfdestruct.com**. Examination of the recovered requests reconstructed the complete user interaction with the anonymous messaging service.

### Table 4.1 Website Workflow

| Frame | Request | Description |
|--------|---------|-------------|
| 82936 | GET /secure/submit | User accessed the anonymous message submission page |
| 83601 | POST /secure/submit | Completed message submitted to the service |
| 83614 | GET /secure/success | Confirmation page returned following successful submission |

The recovered sequence demonstrates a normal web application workflow:

1. Initial access to the message submission page.
2. Completion and submission of the online form.
3. Successful confirmation returned by the server.

This sequence confirms that the anonymous message was transmitted successfully during the capture period.

---

## 4.4 Recovery of the HTTP POST Request

Detailed inspection of **Frame 83601** recovered the HTTP POST request responsible for transmitting the anonymous message.

The POST request was directed to:

```
POST /secure/submit HTTP/1.1
Host: www.willselfdestruct.com
```

The recovered HTML form contained the following fields.

### Table 4.2 Recovered Form Data

| Field | Value |
|--------|-------|
| to | lilytuckrige@yahoo.com |
| from | *(empty)* |
| subject | you can't find us |
| message | and you can't hide from us. Stop teaching. Start running. |
| type | 0 |
| ttl | 30 |
| submit.x | 92 |
| submit.y | 26 |

### Figure 5.3 – HTTP POST and Recovered Form Fields

<img width="1135" height="702" alt="Fig_5_3_HTTP_POST_and_Recovered_Form_Fields" src="https://github.com/user-attachments/assets/0b313e70-f3b2-4ff4-b7cd-9fd7d2025541" />


The recovered POST request provides direct packet-level evidence that the anonymous message was submitted through the web application.

---

## 4.5 Client IP Attribution

Packet inspection identified the originating client IP responsible for the HTTP POST request.

### Table 4.3 Client IP Attribution

| Attribute | Value |
|-----------|-------|
| Frame | 83601 |
| Source IP | 192.168.15.4 |
| Destination IP | 69.25.94.22 |
| Protocol | HTTP POST |

The recovered POST originated from **192.168.15.4**, establishing the internal client responsible for transmitting the anonymous message.

---

## 4.6 Client MAC Attribution

Inspection of the Ethernet header associated with **Frame 83601** identified the physical network interface responsible for transmitting the recovered HTTP POST request.

### Table 4.4 Ethernet Attribution

| Attribute | Value |
|-----------|-------|
| Source MAC | 00:17:f2:e2:c0:ce |
| Destination MAC | 00:1d:d9:2e:4f:60 |
| Source IP | 192.168.15.4 |
| Destination IP | 69.25.94.22 |

### Figure 5.4 – Client IP and MAC Attribution

<img width="1142" height="187" alt="Fig_5_4_Client_IP_and_MAC_Attribution" src="https://github.com/user-attachments/assets/3cb04be0-0103-4343-918b-115e4c3ff18b" />


This establishes the packet-level relationship between the HTTP POST, the client IP address and the originating Ethernet interface.

---

## 4.7 Identity-Bearing Browser Artefacts

Traffic associated with the attributed client device was examined for browser cookies and identity-bearing artefacts.

Analysis recovered a Gmail Chat cookie referencing the following account:

```
jcoachj@gmail.com
```

The recovered cookie demonstrates that the browser associated with the client device had previously interacted with that Gmail account during the capture period.



The recovered cookie is an identity-bearing artefact associated with the browser session. It should not, by itself, be interpreted as conclusive proof of the identity of the individual operating the device at the time of the message submission.

---

## 4.8 Chemistry 109 Comparison

The assessment instructions required comparison of the recovered identity with a supplied **Chemistry 109** class roster.

During examination of the supplied evidence package, no Chemistry 109 roster or equivalent class list was identified. Consequently, no evidential comparison could be performed.

This limitation has been retained within the investigation rather than supplemented through external information or unsupported inference.

---

## 4.9 Summary of Findings

### Table 4.5 Summary of Evidential Findings

| Finding | Result |
|----------|--------|
| Evidence integrity verified | Yes |
| HTTP communications identified | Yes |
| Website reconstructed | Yes |
| HTTP POST recovered | Yes |
| Anonymous message recovered | Yes |
| Client IP identified | 192.168.15.4 |
| Client MAC identified | 00:17:f2:e2:c0:ce |
| Browser identity artefact recovered | Yes |
| Chemistry 109 comparison completed | No (roster unavailable) |

The findings presented in this section form the evidential basis for the attribution analysis, incident timeline and confidence assessment presented in the following sections.

# 5. Integrated UTC Incident Timeline

## 5.1 Timeline Reconstruction

Following recovery of the HTTP requests associated with **www.willselfdestruct.com**, the relevant packet timestamps were examined to reconstruct the sequence of events. The timestamps recorded within the packet capture were normalized to **Coordinated Universal Time (UTC)** to provide a consistent chronological reference for evidential interpretation.

The reconstructed timeline demonstrates a logical progression from initial access to the anonymous messaging service, through successful message submission, and finally to confirmation of successful delivery.

---

## 5.2 UTC Incident Timeline

### Figure 5.6 – Incident Timeline and Service Usage



### Table 5.1 UTC Incident Timeline

| UTC Time | Frame | Event | Evidence |
|----------|------:|-------|----------|
| 06:03:43.825871 | 82936 | Client accessed `/secure/submit` | HTTP GET |
| 06:04:24.311700 | 83601 | Anonymous message submitted | HTTP POST |
| 06:04:24.564165 | 83614 | Confirmation page returned | HTTP GET `/secure/success` |

The reconstructed timeline indicates that approximately **40 seconds** elapsed between the user's initial access to the message submission page and the successful submission of the completed form. The subsequent confirmation page was returned almost immediately following submission, indicating that the web application accepted and processed the request successfully.

---

## 5.3 Interpretation of Timeline Evidence

The recovered HTTP sequence is internally consistent with normal web application behaviour:

1. The client first requested the anonymous message submission page.
2. The user completed the online form.
3. The completed form was transmitted using an HTTP POST request.
4. The server responded by redirecting the client to a success page.

This sequence provides strong packet-level evidence that the anonymous message was successfully transmitted during the captured session.

---

# 6. Packet-Level Attribution Matrix

## 6.1 Attribution Methodology

Attribution was performed by linking evidence across multiple protocol layers. Rather than relying on a single artefact, the investigation correlated Ethernet, IP, TCP and HTTP evidence to construct a defensible attribution chain.

Each attribution step is supported by directly observed packet-level evidence.

---

## 6.2 Packet-Level Attribution Matrix

### Table 6.1 Attribution Matrix

| Investigation Step | Supporting Evidence | Result |
|--------------------|--------------------|--------|
| Anonymous messaging website identified | HTTP Host Header | **www.willselfdestruct.com** |
| Destination web server identified | Destination IP | **69.25.94.22** |
| Client identified | Source IP | **192.168.15.4** |
| Client network interface identified | Source MAC | **00:17:f2:e2:c0:ce** |
| Message recovered | HTTP POST Form | Successfully recovered |
| Browser identity artefact recovered | Gmail Chat Cookie | **jcoachj@gmail.com** |
| Timeline reconstructed | HTTP GET / POST sequence | Completed |
| Named student identified | Chemistry 109 roster | **Not possible** |

---

## 6.3 Attribution Chain

The evidential chain developed during the investigation is summarised below.

```text
Anonymous Message
        │
        ▼
HTTP POST
(Frame 83601)
        │
        ▼
www.willselfdestruct.com
        │
        ▼
Destination Server
69.25.94.22
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
Browser Cookie
jcoachj@gmail.com
        │
        ▼
Chemistry 109 Roster
Unavailable
```

The attribution chain demonstrates continuity from the anonymous message through the associated network communication and browser artefacts. However, because the referenced Chemistry 109 roster was not included in the supplied evidence, the chain cannot be extended to attribute the activity to a named individual.

---

# 7. Alternative Explanations, Limitations and Confidence Assessment

## 7.1 Alternative Explanations

Although the packet capture provides clear evidence linking the anonymous message to a specific client device, several alternative explanations remain possible due to the nature of the available evidence.

### Shared Network Environment

The packet capture originated from a shared network environment. While the originating device can be identified through its IP address and Ethernet MAC address, packet captures alone cannot establish who was physically operating the device at the relevant time.

### Browser Artefacts

The recovered Gmail Chat cookie demonstrates that the browser associated with the client device interacted with the identified Gmail account during the capture period. However, browser cookies identify browser sessions rather than individuals. A browser session may have been accessed by multiple users if the device was shared.

### Missing Supporting Evidence

The assessment instructions referenced a Chemistry 109 class roster for comparison with recovered identity artefacts. As this supporting evidence was unavailable, the investigation could not determine whether the recovered Gmail identity corresponded to a member of the class.

---

## 7.2 Investigation Limitations

The investigation was subject to the following limitations:

- Analysis was restricted to the supplied packet capture.
- No endpoint forensic image was available for examination.
- No operating system logs were supplied.
- No DHCP lease records were available.
- No authentication logs were available.
- No physical device examination was possible.
- The referenced Chemistry 109 roster was unavailable.
- Attribution to a named individual could therefore not be completed.

These limitations have been documented rather than supplemented through unsupported inference.

---

## 7.3 Confidence Assessment

### Table 7.1 Confidence Assessment

| Finding | Confidence |
|---------|------------|
| Evidence integrity | High |
| Website reconstruction | High |
| HTTP POST recovery | High |
| Client IP attribution | High |
| Client MAC attribution | High |
| Timeline reconstruction | High |
| Browser identity artefact recovery | High |
| Attribution to named individual | Low (insufficient evidence) |

The available evidence supports a **high level of confidence** in attributing the anonymous message to the originating client device and browser session. However, the absence of corroborating endpoint evidence and the missing Chemistry 109 roster prevent attribution to a specific individual.

---

# 8. Professional Conclusion

This investigation examined the supplied packet capture to determine whether packet-level evidence could reconstruct an anonymous email harassment incident and attribute the activity to the originating client device.

The investigation successfully preserved and verified the integrity of the supplied evidence before conducting protocol analysis, endpoint identification, website reconstruction and application-layer examination. HTTP analysis reconstructed the complete interaction with **www.willselfdestruct.com**, including retrieval of the submission page, transmission of the completed HTTP POST request and successful return of the confirmation page.

Detailed inspection of the recovered POST request identified the anonymous message, destination recipient and associated form fields. Network-layer analysis attributed the communication to client IP address **192.168.15.4**, while Ethernet analysis identified the corresponding client MAC address **00:17:f2:e2:c0:ce**. Examination of browser artefacts recovered a Gmail Chat cookie associated with the browser session, extending the attribution chain beyond network addressing.

The reconstructed UTC timeline demonstrated a coherent sequence of events consistent with normal operation of the anonymous messaging service. Together, the recovered HTTP requests, packet metadata and browser artefacts provide strong evidence that the anonymous message was successfully transmitted from the identified client device during the capture period.

Although the investigation established a robust packet-level attribution to the originating device, attribution to a named individual could not be completed because the Chemistry 109 class roster referenced in the assessment was not included within the supplied evidence package. Furthermore, the shared nature of the network environment requires recognition that packet captures alone cannot identify the individual operating the device at the time of the incident.

Accordingly, the conclusions presented in this report are limited to what is directly supported by the available evidence. The investigation demonstrates the value of packet-level forensic analysis for reconstructing historical web activity while emphasising the importance of corroborating network evidence with endpoint and administrative records when individual attribution is required.

# Appendices

---

# Appendix A – Investigation Activity Log (Summary)

The investigation was conducted using a structured and repeatable workflow. Each major investigative activity was documented as part of the case record.

## Table A.1 Investigation Activity Summary

| Step | Activity | Output Produced |
|------|----------|-----------------|
| 1 | Evidence extraction | Original packet capture recovered |
| 2 | Working copy creation | Working evidence created |
| 3 | MD5 hash generation | `md5.txt` |
| 4 | SHA-256 hash generation | `sha256.txt` |
| 5 | Capture summary | Capinfos output |
| 6 | Protocol hierarchy analysis | `protocol_hierarchy.txt` |
| 7 | IPv4 endpoint analysis | `ip_endpoints.txt` |
| 8 | Ethernet endpoint analysis | `mac_endpoints.txt` |
| 9 | TCP conversation analysis | `tcp_conversations.txt` |
| 10 | Website reconstruction | HTTP request inventory |
| 11 | HTTP POST recovery | Recovered message |
| 12 | Client IP attribution | Source IP identified |
| 13 | Client MAC attribution | Source MAC identified |
| 14 | Identity artefact recovery | Gmail cookie recovered |
| 15 | Timeline reconstruction | UTC incident timeline |
| 16 | Attribution matrix | Completed |
| 17 | Report preparation | Investigation documented |

> The complete investigation activity log is provided separately as **Activity_Log_CIP-B105-CS2.docx**.

---

# Appendix B – Evidence Register (Summary)

## Table B.1 Evidence Register

| Evidence ID | Description | Purpose | Status |
|-------------|-------------|---------|--------|
| EV-001 | nitroba.pcap | Primary packet capture | Examined |
| EV-002 | Working copy | Analysis copy | Examined |
| EV-003 | MD5 hash | Integrity verification | Verified |
| EV-004 | SHA-256 hash | Integrity verification | Verified |
| EV-005 | Protocol hierarchy output | Protocol analysis | Generated |
| EV-006 | IPv4 endpoints | Endpoint identification | Generated |
| EV-007 | Ethernet endpoints | MAC attribution | Generated |
| EV-008 | TCP conversations | Session reconstruction | Generated |
| EV-009 | HTTP POST recovery | Message recovery | Generated |
| EV-010 | Screenshots | Evidential documentation | Generated |

The complete evidence register accompanies this report as **Evidence_Register_CIP-B105-CS2.docx**.

---

# Appendix C – Cryptographic Hash Records

Cryptographic integrity verification was performed before analysis commenced.

## Table C.1 Hash Records

| Algorithm | File | Purpose |
|-----------|------|---------|
| MD5 | `Documentation/Hashes/md5.txt` | Integrity verification |
| SHA-256 | `Documentation/Hashes/sha256.txt` | Integrity verification |

The exact hash values are retained within the accompanying hash record files.

---

# Appendix D – Commands Executed

The investigation was performed using standard Linux command-line forensic utilities.

## Principal Tools

- Ubuntu Linux
- Wireshark 4.6.4
- TShark 4.6.4
- Capinfos
- GNU Bash
- md5sum
- sha256sum

The exact commands executed during the investigation are documented in:

```
Documentation/Commands_Executed.txt
```

---

# Appendix E – Screenshot Index

The following screenshots provide visual evidence supporting the investigation.

## Table E.1 Screenshot Register

| Figure | Screenshot File | Description |
|---------|----------------|-------------|
| Figure 4.1 | Fig_4_1_Evidence_Integrity_and_Capture_Summary.png | Evidence integrity verification and capture summary |
| Figure 5.1 | Fig_5_1_Protocol_Hierarchy_and_IPv4_Endpoints.png | Protocol hierarchy and IPv4 endpoint analysis |
| Figure 5.2 | Fig_5_2_TCP_Conversations.png | TCP conversation analysis |
| Figure 5.3 | Fig_5_3_HTTP_POST_and_Recovered_Form_Fields.png | HTTP POST request and recovered form fields |
| Figure 5.4 | Fig_5_4_Client_IP_and_MAC_Attribution.png | Client IP and MAC attribution |
| Figure 5.5 | Fig_5_5_Gmail_Cookie_Identity_Attribution.png | Browser identity artefact |
| Figure 5.6 | Fig_5_6_Incident_Timeline_and_Service_Usage.png | UTC incident timeline |

---

# Appendix F – Submission Package

The completed submission package contains the following deliverables.

```
CIP-B105-CS2/
│
├── README.md
├── Evidence_Report.md
│
├── Report/
│   ├── Investigation_Report.docx
│   └── Investigation_Report.pdf
│
├── Documentation/
│   ├── Activity_Log_CIP-B105-CS2.docx
│   ├── Evidence_Register_CIP-B105-CS2.docx
│   ├── UTC_Incident_Timeline_CIP-B105-CS2.docx
│   ├── Commands_Executed.txt
│   └── Hashes/
│       ├── md5.txt
│       └── sha256.txt
│
├── Output/
│   ├── protocol_hierarchy.txt
│   ├── ip_endpoints.txt
│   ├── mac_endpoints.txt
│   └── tcp_conversations.txt
│
├── Evidence/
│   ├── Original/
│   ├── Working/
│   └── Exports/
│
└── Screenshots/
    ├── Fig_4_1_Evidence_Integrity_and_Capture_Summary.png
    ├── Fig_5_1_Protocol_Hierarchy_and_IPv4_Endpoints.png
    ├── Fig_5_2_TCP_Conversations.png
    ├── Fig_5_3_HTTP_POST_and_Recovered_Form_Fields.png
    ├── Fig_5_4_Client_IP_and_MAC_Attribution.png
    ├── Fig_5_5_Gmail_Cookie_Identity_Attribution.png
    └── Fig_5_6_Incident_Timeline_and_Service_Usage.png
```

---

# References

The investigation relied primarily on evidence recovered from the supplied packet capture and standard digital forensic tools.

### Software

- Wireshark Foundation. *Wireshark User's Guide*. https://www.wireshark.org/docs/
- Wireshark Foundation. *TShark Manual Pages*. https://www.wireshark.org/docs/man-pages/tshark.html

### Standards and Guidance

- National Institute of Standards and Technology (NIST). (2006). *Guide to Integrating Forensic Techniques into Incident Response (SP 800-86)*.
- National Institute of Standards and Technology (NIST). (2014). *Computer Security Incident Handling Guide (SP 800-61 Rev. 2)*.
- RFC 2616. *Hypertext Transfer Protocol -- HTTP/1.1*.
- RFC 7230. *Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing*.

---

# Repository Information

**Repository Name**

```
CIP-B105-CS2-Email-Harassment-Wireshark-TShark-Attribution
```

**Author**

**Dahiru Abdulwahid Umar**

Registration Number: **C11/26/DFIT/17283**

Diploma in Digital Forensics and Incident Response (DFIT)

International Cybersecurity and Digital Forensics Academy (ICDFA)

---

## Academic Declaration

I declare that this investigation report represents my own analysis of the evidence supplied for **CIP-B105 – Computer Forensics Case Study II**. All findings are supported by the packet-level evidence recovered during the investigation. Where supporting evidence referenced in the assessment instructions was unavailable, this limitation has been explicitly documented rather than supplemented through unsupported inference or speculation.

---

**End of Report**
