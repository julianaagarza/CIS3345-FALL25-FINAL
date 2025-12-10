# Timeline Notes  

---

## Overview
These notes consolidate important timestamps observed across the evidence sources.  
All times use **local system time (CST)** for consistency.

The goal of this document is to establish the sequence of events leading up to the suspected fraudulent submission of the W-2 document.

---

## Document Timestamp Notes

### W2_JDoe_draft.pdf
- **Creation Time:** 2025-10-28 09:12:44  
- **Last Modified:** 2025-10-28 09:12:44  
- **Notes:**  
  - Draft file appears untouched after initial creation.  
  - Metadata is consistent with a legitimate early version.

### W2_JDoe_final.pdf
- **Creation Time:** 2025-12-03 13:07:11  
- **Last Modified:** 2025-12-03 13:09:52  
- **Notes:**  
  - Final version created and modified within a short window.  
  - Modification time occurred **less than 10 minutes before** the upload event recorded in the PCAP.

### Observations
- The draft file shows no irregularities.  
- The final file’s creation and modification both occur **on the same afternoon**, which does not match standard employer document issuance behavior.  
- The tight timing between modification and upload suggests intentional preparation and submission.

---

## Email Timestamp Notes

### Legitimate Lender Emails
- **lender_alice.eml:** 2025-12-01 08:22:10  
- **lender_carol.eml:** 2025-12-01 09:15:03  
- **Notes:**  
  - Both sent from the correct domain.  
  - Follow consistent formatting and expected communication timing.

### Suspicious Email (fraud_jdoe.eml)
- **Timestamp:** 2025-12-03 13:12:27  
- **Notes:**  
  - Sent just minutes after the W-2 final file was modified.  
  - Sender domain does not match the lender’s official domain.  
  - Formatting and header structure differ from legitimate messages.

### Observations
- The suspicious email aligns closely with the period in which the document was created/modified.  
- This suggests coordination between document preparation and communication.

---

## Network Activity Timestamp Notes

### POST Upload Event (from PCAP and tshark CSV)
- **Upload Timestamp:** 2025-12-03 13:15:34  
- **Details:**  
  - POST request shows upload activity to the simulated lender portal endpoint.  
  - The upload originated from the workstation under investigation.

### Observations
- The upload took place **approximately 3 minutes after** the suspicious email was sent.  
- The upload occurred **under 6 minutes after** the document was last modified.  
- Timing strongly supports deliberate modification followed by immediate submission.

---

## SSH Log Timestamp Notes

### Suspicious Login Attempts
- **2025-12-03 12:54:01** – Failed password attempt from `192.0.2.5`  
- **2025-12-03 12:54:15** – Failed password attempt from `192.0.2.5`  
- **2025-12-03 12:55:02** – Repeated failed authentication attempt  
- **Notes:**  
  - Attempts occurred **10–15 minutes before** the W-2 was created.  
  - No successful login from external IPs.

### Observations
- While no unauthorized access was confirmed, the timing suggests someone attempted to access the system shortly before document creation.  
- Could indicate probing or attempted compromise of the workstation.

---

## Emerging Timeline Pattern (Preliminary)

### Chronological Sequence
1. **12:54–12:55 PM** — Repeated failed SSH login attempts from external IP `192.0.2.5`  
2. **1:07 PM** — W2_JDoe_final.pdf created  
3. **1:09 PM** — W2_JDoe_final.pdf modified  
4. **1:12 PM** — Suspicious “lender” email sent  
5. **1:15 PM** — POST upload of the W-2 submitted to the lender upload endpoint  

### Interpretation
The timestamps form a highly coordinated sequence:

- Access attempts occur first  
- Document is created  
- Document is modified  
- Email is sent  
- File is uploaded  

This order strongly implies intentional workstation use to alter and submit the document, rather than innocent activity.

---
