# Digital Forensic Report: Mortgage Document Investigation

---

# 1. Introduction

## 1.1 Purpose of Investigation
This investigation was initiated in response to concerns raised during a mortgage application review, where a submitted W-2 document appeared inconsistent with standard employer-issued formatting and timing. The forensic team was tasked with determining whether the document had been altered, fraudulently generated, or submitted through deceptive means. The case centers on a workstation believed to have been used to prepare and transmit the questionable file, and the goal of this investigation is to determine:

- Whether the final W-2 document was modified or fabricated locally.
- Whether email communications associated with the submission were legitimate or fraudulent.
- Whether the workstation’s network and system activity aligns with intentional document manipulation.
- Whether any attempted unauthorized access contributed to suspicious behavior.

To accomplish this, investigators analyzed multiple categories of digital evidence, including PDF metadata, email headers, packet capture data, and system authentication logs. The findings from these independent sources were correlated to build a comprehensive understanding of the events surrounding the document submission.

## 1.2 Scope of Investigation
This investigation examines only the evidence provided within a controlled forensic environment. A preconfigured Ubuntu 24.04 virtual machine was used to ensure isolation, repeatability, and integrity throughout the analysis. Original evidence files—PDFs, .eml email messages, PCAP data, and authentication logs—were preserved in read-only form, and all examination was performed on working copies in accordance with forensic best practices.

The scope of this report includes:

- Extraction and evaluation of metadata from the draft and final W-2 documents.
- Examination of email headers and message attributes to assess authenticity.
- Inspection of network activity to identify file uploads and correlate timestamps.
- Review of system authentication logs for signs of unauthorized access attempts.
- Construction of a consolidated timeline to establish sequence and intent.

The investigation adheres to core digital forensic principles:

- **Integrity:** Original evidence remains unaltered; all actions are performed on verified duplicates.
- **Repeatability:** Every step is documented so that another analyst can reproduce results.
- **Minimization of Change:** Only noninvasive tools and read-only access methods were used.

Assumptions and constraints relevant to the investigation:

- No full disk image of the workstation was provided; analysis is limited to the evidence package.
- Network captures include only loopback activity; external traffic was not available.
- The investigation relies on the timestamps present in the provided artifacts, assuming they were not tampered with before intake.

All evidence was handled according to forensic best practices. Original evidence was never modified. Only copies were used for analysis.

---

# 2. Evidence Overview

## 2.1 Evidence Received
The following evidence was included in the mortgage fraud scenario:

| Evidence Type | Description |
|---------------|-------------|
| PDF Files | W-2 draft and final versions for John Doe, plus additional applicant PDFs |
| Email Files | Two legitimate lender emails and one suspicious impersonation email |
| PCAP File | Network traffic showing HTTP activity on the workstation |
| SSH Logs | Authentication attempts recorded in `/var/log/auth.log` |
| Documentation | Integrity log and chain of custody documentation |

Each category was analyzed using appropriate forensic tools.

## 2.2 Evidence Handling and Integrity
Upon receiving the evidence package, it was placed into specific directories inside the forensic VM. Immediately after placement:

- SHA-256 hashes were generated for each file.
- A chain of custody document was recorded.
- Original files were marked as read-only to prevent modification.
- A working directory structure was established for proper separation of original vs. analysis artifacts.

These steps ensured that all conclusions drawn would be reproducible and verifiable.

---

# 3. Methodology

The investigation followed a structured, repeatable forensic workflow designed to ensure systematic analysis and proper correlation of events.

## 3.1 Overview of Approach
The methodology consisted of:

1. **PDF Metadata Analysis** – Examine document origins, creation/modification times, and software signatures.
2. **Draft vs Final W-2 Comparison** – Compare metadata and structural differences to identify possible manipulation.
3. **Email Header Examination** – Assess authenticity of communication by analyzing sending domains, timestamps, and formatting.
4. **Network Traffic Review (PCAP)** – Identify upload activity, timestamp alignment, and source/destination indicators.
5. **Tshark Structured Extraction** – Export network metadata to validate findings through structured analysis.
6. **SSH Authentication Log Review** – Look for unauthorized login attempts that might correlate with suspicious activity.
7. **Timeline Construction** – Establish chronological order to reveal intent, sequence, and causality.

## 3.2 Tools Used
The following tools were used for analysis:

| Tool | Purpose |
|------|---------|
| **ExifTool** | Extract PDF metadata such as authorship, timestamps, and software signatures |
| **diff utilities** | Compare metadata files and PDF structure line-by-line |
| **Wireshark** | Visually inspect captured packets, filter HTTP activity |
| **tshark** | Export packet metadata into CSV format for structured verification |
| **grep / less** | Review email headers and log entries |
| **Ubuntu 24.04 VM** | Provides an isolated, controlled forensic environment |

These tools were chosen due to reliability, repeatability, and standard acceptance in digital forensics.

---

# 4. Analysis Findings

---

# 4.1 PDF Metadata Analysis

## 4.1.1 Metadata Summary Table

| File | Creation Time | Modification Time | Notes |
|------|----------------|--------------------|-------|
| **W2_JDoe_draft.pdf** | 2025-10-28 09:12:44 | 2025-10-28 09:12:44 | Appears unmodified since creation |
| **W2_JDoe_final.pdf** | 2025-12-03 13:07:11 | 2025-12-03 13:09:52 | Modified minutes after creation, unusual for employer-issued W-2 |

## 4.1.2 Interpretation
The metadata revealed several key findings:

- The draft W-2 file showed stable metadata consistent with a legitimately issued document.
- The final W-2 file appeared *newly created* on December 3rd, 2025, and modified just minutes later.
- Employer-issued W-2s are normally generated by payroll systems and should not show such tightly spaced timestamps or workstation-created metadata.

**These indicators strongly suggest that the final W-2 was fabricated or modified locally.**

---

# 4.2 Draft vs Final W-2 Comparison

## 4.2.1 Summary of Key Differences
When comparing the metadata between the draft and final files:

- The **software identifiers** were different.  
- The **creator/producer** fields indicated that the final version was generated using software not associated with payroll systems.  
- The **timestamps** do not align with typical employer document issuance patterns.  
- The **structure** of the PDF also differed, consistent with regeneration rather than simple editing.

## 4.2.2 Interpretation
These differences indicate:

- The final W-2 was not derived from the draft file through an employer system.  
- Instead, it appears to have been recreated or altered manually on the workstation.  
- The timestamps align with other suspicious activity (email and network traffic).

This supports the hypothesis that the final W-2 document was intentionally altered.

---

# 4.3 Email Header Analysis

## 4.3.1 Summary of Email Findings

| Email Type | Sender Domain | Timestamp | Authenticity Indicators |
|------------|---------------|-----------|--------------------------|
| Lender Email #1 | Valid lender domain | 2025-12-01 (AM) | Legitimate structure, consistent formatting |
| Lender Email #2 | Valid lender domain | 2025-12-01 (AM) | Normal email headers |
| Suspicious Email | Incorrect domain mimicking lender | 2025-12-03 13:12:27 | Formatting inconsistencies, abnormal header fields |

## 4.3.2 Additional Observations
- The fraudulent email's domain visually resembles the lender’s domain but contains subtle alterations.  
- The message headers show irregular spacing and capitalization not present in legitimate communications.  
- The timing—minutes after the W-2 modification—suggests purposeful alignment with the submission process.

## 4.3.3 Interpretation
The suspicious email shows clear signs of impersonation:

- Incorrect domain  
- Formatting inconsistent with lender templates  
- Timestamp aligning with document modification  

**The email appears intentionally crafted to deceive the lender into accepting a fraudulent W-2.**

---

# 4.4 Network Traffic Analysis (PCAP)

## 4.4.1 Observed Activity
The packet capture contained HTTP POST request activity directed at the local submission endpoint.

| Event | Timestamp | Description |
|--------|-----------|-------------|
| HTTP POST containing W-2 | 2025-12-03 13:15:34 | Uploaded modified W-2 document |

## 4.4.2 Supporting Details
- The POST request originated from the same workstation where document manipulation occurred.  
- The timestamp shows the upload occurred only **3 minutes** after the suspicious email was sent.  
- The structure of the POST request indicates deliberate file submission, not background activity.

## 4.4.3 Interpretation
The network evidence confirms:

- A file was actively uploaded by the user.  
- The upload timestamp corresponds closely with the creation/modification times of the final W-2.  
- This behavior supports the idea of intentional filing of fraudulent documentation.

---

# 4.5 Tshark Structured Extraction

## 4.5.1 Summary of Extracted Data
The structured extraction produced:

- Timestamp of the upload event  
- Local loopback IP source address  
- Destination endpoint  
- Full URI of the upload request  

## 4.5.2 Interpretation
The structured output validates the Wireshark findings and:

- Confirms the upload came from the local machine  
- Confirms the upload was not automated but user-initiated  
- Allows precise alignment of the upload with other logged events

---

# 4.6 SSH Log Analysis

## 4.6.1 Summary of Log Entries

| Time | Source IP | Result |
|-------|------------|---------|
| 12:54:01 PM | 192.0.2.5 | Failed login attempt |
| 12:54:15 PM | 192.0.2.5 | Failed login attempt |
| 12:55:02 PM | 192.0.2.5 | Failed login attempt |

## 4.6.2 Interpretation
These repeated failed attempts indicate:

- Someone attempted to authenticate to the system shortly before the document activity.  
- No login was successful, meaning the workstation was not compromised via SSH.  
- However, the timing suggests reconnaissance or probing behavior.

While not directly responsible for the W-2 alteration, these attempts strengthen the contextual suspicion that the workstation was being manipulated around the time of the fraudulent activity.

---

# 5. Consolidated Timeline of Events

A chronological sequence of all findings is presented below:

| Time (Dec 3, 2025) | Event |
|---------------------|-------|
| **12:54:01 PM** | First failed SSH login attempt from 192.0.2.5 |
| **12:55:02 PM** | Additional failed SSH login attempt |
| **13:07:11 PM** | Final W-2 created on system |
| **13:09:52 PM** | Final W-2 modified locally |
| **13:12:27 PM** | Suspicious, impersonated email sent |
| **13:15:34 PM** | Final W-2 uploaded via HTTP POST |

## Timeline Interpretation
The timeline shows an aligned and rapid progression:

- Attempts to access the system  
- Creation of a new W-2  
- Modification of the W-2  
- Sending of a fraudulent email  
- Uploading the modified W-2  

The precise alignment of these events strongly suggests coordinated intent rather than coincidence.

---

# 6. Final Interpretation

After analyzing all evidence categories, the following conclusions are supported:

- The W-2 submitted during the mortgage application was **altered locally**, not employer-generated.  
- The manipulated document was **submitted intentionally** shortly after modification.  
- The suspicious email associated with the submission was indeed fraudulent.  
- SSH log activity, though unsuccessful, occurred close enough to be relevant contextual evidence.  
- The combination of metadata, communication irregularities, and network behavior forms a coherent narrative of deliberate fraud.

---

# 7. Conclusion

- The modified W-2 document was intentionally generated and altered on the workstation.  
- The fraudulent email indicates an attempt to deceive the lender into accepting the altered document.  
- Network activity confirms intentional submission of the modified W-2.  
- System logs provide supporting evidence of suspicious behavior occurring before the document activity.

The investigation concludes that the workstation was used as part of a deliberate attempt to falsify mortgage-related documents.

---

# 8. Recommendations

| Area | Recommendation |
|-------|--------------|
| **Authentication Security** | Require MFA and restrict SSH exposure to internal networks only |
| **Workstation Monitoring** | Implement logging of sensitive file access and modification events |
| **Network Monitoring** | Alert on outbound uploads to unapproved endpoints |
| **User Awareness Training** | Educate users on identifying fraudulent emails and domain spoofing |
| **System Hardening** | Enforce stronger password policies and audit SSH services regularly |

Applying these recommendations would reduce risks associated with document fraud, unauthorized changes, and impersonation attempts.

---

# 9. Appendices

## Appendix A – Evidence Descriptions
(Excludes hash values and sensitive data)

- **W2_JDoe_draft.pdf** – Baseline reference document  
- **W2_JDoe_final.pdf** – Suspected modified document  
- **lender_x.eml** – Verified legitimate communications  
- **fraud_jdoe.eml** – Impersonation email  
- **loopback_uploads.pcap** – Captured network upload activity  
- **auth.log excerpt** – SSH authentication attempts  

## Appendix B – Tools Used

- ExifTool  
- Wireshark  
- tshark  
- diff utilities  
- grep / less  
- Ubuntu 24.04 forensic VM environment  

---

