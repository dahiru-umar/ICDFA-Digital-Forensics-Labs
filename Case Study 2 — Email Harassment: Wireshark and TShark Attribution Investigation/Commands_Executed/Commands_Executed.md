# CIP-B105 – Computer Forensics Case Study II

# Commands Executed

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
| **Primary Evidence** | `nitroba.pcap` |

---

# Purpose

This document records the principal command-line operations executed during the forensic investigation. The commands are presented in the order they were performed to ensure transparency, repeatability, and reproducibility of the examination.

All commands were executed on the forensic **working copy** of the supplied packet capture unless otherwise stated.

---

# Command Log

---

## Step 1 – Extract Original Evidence

### Purpose

Extract the supplied packet capture from the archive.

```bash
unzip ~/Downloads/data.zip data/nitroba.pcap \
-d ~/CIP-B105-CS2/Evidence/Original
```

**Output**

- Original evidence extracted successfully.

---

## Step 2 – Create Working Copy

### Purpose

Create a forensic working copy for analysis.

```bash
cp \
~/CIP-B105-CS2/Evidence/Original/nitroba.pcap \
~/CIP-B105-CS2/Evidence/Working/
```

**Output**

- Working copy created.

---

## Step 3 – Generate MD5 Hash

### Purpose

Verify evidence integrity using MD5.

```bash
md5sum \
~/CIP-B105-CS2/Evidence/Original/nitroba.pcap \
> ~/CIP-B105-CS2/Documentation/Hashes/md5.txt
```

**Output**

```
Documentation/Hashes/md5.txt
```

---

## Step 4 – Generate SHA-256 Hash

### Purpose

Verify evidence integrity using SHA-256.

```bash
sha256sum \
~/CIP-B105-CS2/Evidence/Original/nitroba.pcap \
> ~/CIP-B105-CS2/Documentation/Hashes/sha256.txt
```

**Output**

```
Documentation/Hashes/sha256.txt
```

---

## Step 5 – Capture Summary

### Purpose

Obtain metadata describing the supplied packet capture.

```bash
capinfos \
~/CIP-B105-CS2/Evidence/Original/nitroba.pcap
```

**Output**

Capture statistics including:

- Packet count
- Capture duration
- File size
- SHA-256 verification
- Interface information

---

## Step 6 – Protocol Hierarchy

### Purpose

Identify protocols present within the capture.

```bash
tshark -r nitroba.pcap \
-q \
-z io,phs \
> ~/CIP-B105-CS2/Output/protocol_hierarchy.txt
```

**Output**

```
protocol_hierarchy.txt
```

---

## Step 7 – IPv4 Endpoint Analysis

### Purpose

Identify participating IPv4 endpoints.

```bash
tshark -r nitroba.pcap \
-q \
-z endpoints,ip \
> ~/CIP-B105-CS2/Output/ip_endpoints.txt
```

**Output**

```
ip_endpoints.txt
```

---

## Step 8 – Ethernet Endpoint Analysis

### Purpose

Identify participating Ethernet MAC addresses.

```bash
tshark -r nitroba.pcap \
-q \
-z endpoints,eth \
> ~/CIP-B105-CS2/Output/mac_endpoints.txt
```

**Output**

```
mac_endpoints.txt
```

---

## Step 9 – TCP Conversation Analysis

### Purpose

Identify TCP conversations within the packet capture.

```bash
tshark -r nitroba.pcap \
-q \
-z conv,tcp \
> ~/CIP-B105-CS2/Output/tcp_conversations.txt
```

**Output**

```
tcp_conversations.txt
```

---

## Step 10 – Identify Website Traffic

### Purpose

Locate communications associated with the anonymous messaging service.

```bash
tshark -r nitroba.pcap \
-Y "http.host contains \"willselfdestruct\"" \
-T fields \
-e frame.number \
-e frame.time \
-e ip.src \
-e ip.dst \
-e http.host \
-e http.request.uri
```

**Recovered Workflow**

| Frame | HTTP Request |
|--------|--------------|
| 82936 | GET /secure/submit |
| 83601 | POST /secure/submit |
| 83614 | GET /secure/success |

---

## Step 11 – Recover HTTP POST

### Purpose

Recover the submitted anonymous message.

```bash
tshark -r nitroba.pcap \
-Y "http.request.method == POST && http.host contains \"willselfdestruct\"" \
-V
```

**Recovered**

- Recipient
- Subject
- Message
- Form fields

---

## Step 12 – Client IP and MAC Attribution

### Purpose

Identify the originating client.

```bash
tshark -r nitroba.pcap \
-Y "frame.number==83601" \
-T fields \
-e frame.number \
-e eth.src \
-e eth.dst \
-e ip.src \
-e ip.dst
```

**Recovered**

| Attribute | Value |
|-----------|-------|
| Frame | 83601 |
| Client IP | 192.168.15.4 |
| Client MAC | 00:17:f2:e2:c0:ce |

---

## Step 13 – Timeline Reconstruction

### Purpose

Reconstruct the sequence of events.

```bash
tshark -r nitroba.pcap \
-Y "frame.number==82936 || frame.number==83601 || frame.number==83614" \
-T fields \
-e frame.number \
-e frame.time \
-e ip.src \
-e ip.dst \
-e http.request.method \
-e http.request.uri
```

**Recovered Timeline**

| Frame | Event |
|--------|-------|
| 82936 | GET /secure/submit |
| 83601 | POST /secure/submit |
| 83614 | GET /secure/success |

---

# Investigation Outputs

The commands generated the following artefacts.

| Output | Description |
|---------|-------------|
| md5.txt | MD5 hash |
| sha256.txt | SHA-256 hash |
| protocol_hierarchy.txt | Protocol hierarchy |
| ip_endpoints.txt | IPv4 endpoints |
| mac_endpoints.txt | Ethernet endpoints |
| tcp_conversations.txt | TCP conversations |

---

# Reproducibility

The commands documented in this file provide a reproducible workflow for repeating the forensic examination using the supplied packet capture. The investigation intentionally analysed a working copy of the evidence to preserve the integrity of the original packet capture.

---

## Author

**Dahiru Abdulwahid Umar**

**Registration Number:** C11/26/DFIT/17283

**Programme:** Diploma in Digital Forensics and Incident Response (DFIT)

**International Cybersecurity and Digital Forensics Academy (ICDFA)**

---

**End of Commands Executed**
