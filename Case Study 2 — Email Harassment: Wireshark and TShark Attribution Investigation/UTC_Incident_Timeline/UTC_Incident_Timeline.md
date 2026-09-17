# CIP-B105 – Computer Forensics Case Study II

# UTC Incident Timeline

## Case Study 2 – Email Harassment: Wireshark and TShark Attribution Investigation

---

## Student Information

| Item | Details |
|------|---------|
| **Student Name** | Dahiru Abdulwahid Umar |
| **Registration Number** | C11/26/DFIT/17283 |
| **Programme** |  Digital Forensics  |
| **Institution** | International Cybersecurity and Digital Forensics Academy (ICDFA) |
| **Course** | CIP-B105 – Computer Forensics Case Study II |
| **Case Study** | Case Study 2 |
| **Evidence** | `nitroba.pcap` |

---

# Purpose

The purpose of this document is to present a chronological reconstruction of the anonymous messaging incident based solely on the packet-level evidence recovered during the forensic examination.

All timestamps have been normalised to **Coordinated Universal Time (UTC)** to provide a consistent evidential timeline independent of local timezone settings.

---

# Timeline Reconstruction Methodology

Timeline reconstruction was performed using packet timestamps recovered from the supplied packet capture. The reconstruction focused exclusively on packets associated with **www.willselfdestruct.com** and the recovered HTTP POST transaction.

The analysis correlated:

- HTTP request timestamps
- Packet frame numbers
- Source and destination IP addresses
- HTTP request methods
- Application-layer requests
- Browser workflow

The resulting timeline represents the sequence of observable events recovered directly from the packet capture.

---

# Timeline Summary

The investigation identified three principal events associated with the anonymous messaging service:

1. Initial access to the message submission page.
2. Submission of the completed anonymous message.
3. Successful confirmation returned by the web server.

Together these events reconstruct the complete interaction between the client browser and the anonymous messaging website.

---


---

# UTC Incident Timeline

| Sequence | UTC Timestamp | Frame Number | Event | Source IP | Destination IP | Evidence |
|-----------|---------------|-------------:|-------|-----------|----------------|----------|
| 1 | 06:03:43.825871 UTC | 82936 | Initial access to `/secure/submit` | 192.168.15.4 | 69.25.94.22 | HTTP GET |
| 2 | 06:04:24.311700 UTC | 83601 | Anonymous message submitted | 192.168.15.4 | 69.25.94.22 | HTTP POST |
| 3 | 06:04:24.564165 UTC | 83614 | Confirmation page returned (`/secure/success`) | 192.168.15.4 | 69.25.94.22 | HTTP GET |

---

# Event Analysis

## Event 1 — Initial Website Access

**Frame:** 82936

The client initiated communication with **www.willselfdestruct.com** by requesting the anonymous message submission page (`/secure/submit`). This represents the beginning of the observable user interaction with the web application.

---

## Event 2 — HTTP POST Submission

**Frame:** 83601

Approximately forty seconds after the initial page request, the client transmitted an HTTP POST request containing the completed anonymous message.

Recovered form fields included:

| Field | Value |
|--------|-------|
| To | lilytuckrige@yahoo.com |
| Subject | you can't find us |
| Message | and you can't hide from us. Stop teaching. Start running. |

This event represents the principal evidential artefact recovered during the investigation.

---

## Event 3 — Successful Submission

**Frame:** 83614

Immediately following the HTTP POST request, the server returned the `/secure/success` page, confirming successful processing of the submitted message.

The absence of retransmissions or application-layer errors indicates that the web application accepted the submitted request.

---

# Timeline Interpretation

The reconstructed sequence demonstrates normal web application behaviour.

```text
HTTP GET
/secure/submit
        │
        ▼
User completes form
        │
        ▼
HTTP POST
/secure/submit
(Frame 83601)
        │
        ▼
Server Processing
        │
        ▼
HTTP GET
/secure/success
```

The packet sequence provides direct evidence that the anonymous message was successfully transmitted during the captured session.

---

# Timeline Observations

The investigation established the following observations:

- The client successfully reached the anonymous messaging service.
- The submission page was retrieved before any form submission occurred.
- A completed HTTP POST request was transmitted to the server.
- The server acknowledged successful processing by returning the success page.
- The recovered timestamps are internally consistent with the observed HTTP workflow.

---

# Timeline Limitations

The reconstructed timeline is limited to activity visible within the supplied packet capture.

The timeline does **not** establish:

- Who was physically operating the client device.
- Activities occurring before packet capture began.
- Activities occurring after packet capture ended.
- Server-side processing beyond what is visible through the HTTP responses.

These limitations are consistent with packet-level network forensic investigations.

---

# Timeline Validation

The reconstructed timeline was validated through correlation of:

| Validation Source | Status |
|-------------------|--------|
| HTTP request sequence | ✓ Verified |
| Packet timestamps | ✓ Verified |
| Frame numbers | ✓ Verified |
| Client IP address | ✓ Verified |
| Destination IP address | ✓ Verified |
| Website workflow | ✓ Verified |

No inconsistencies were identified between the recovered packet timestamps and the reconstructed sequence of events.

---

# Timeline Conclusion

The UTC incident timeline provides a chronological reconstruction of the anonymous messaging activity recovered from the supplied packet capture.

The sequence demonstrates:

- Initial access to the anonymous messaging website.
- Successful submission of the anonymous message.
- Successful confirmation returned by the web server.

When considered alongside the packet-level attribution evidence, the reconstructed timeline supports the conclusion that the anonymous message was transmitted from the identified client device during the captured session.

---

## Author

**Dahiru Abdulwahid Umar**

**Registration Number:** C11/26/DFIT/17283

**Programme:** Diploma in Digital Forensics and Incident Response (DFIT)

**International Cybersecurity and Digital Forensics Academy (ICDFA)**

---

**End of UTC Incident Timeline**
