# Report Draft Notes  

---

# 1. Introduction (Draft)

### Purpose of Investigation  
- Summarize why the investigation was initiated.  
- Explain that the goal is to examine whether a mortgage application file (W-2) was altered and submitted fraudulently.  
- Clarify that the investigation analyzes documents, emails, network traffic, and authentication logs to determine if the workstation was used for manipulation or unauthorized submission.

*Draft phrasing:*  
“This report documents the forensic analysis of evidence related to a suspected fraudulent submission of a W-2 document. The purpose of this investigation is to determine whether the file was altered, how it was handled, and whether the workstation shows signs of misuse or unauthorized activity.”

### Scope of Work  
- Identify which evidence sources were examined.  
- Clarify that only the provided dataset was analyzed.  
- Note that the investigation was performed within a controlled VM environment.

---

# 2. Evidence Overview (Draft)

### Evidence Received  
- W-2 PDFs (multiple applicants)  
- Email files (.eml)  
- Network capture (.pcap)  
- Authentication logs  
- Integrity logs and chain-of-custody documentation  

### Evidence Handling Summary  
- All files were placed in structured directories.  
- No evidence was altered; analyses were performed on copies when appropriate.  
- File integrity verified using SHA-256 hashing.

*Note to expand:*  
Include a table of evidence types in the final version.

---

# 3. Methodology Summary (Draft)

### General Approach  
- Describe the forensic environment (Ubuntu VM, installed tools).  
- Emphasize structured workflow: document analysis → email analysis → network analysis → log review.

### Tools Used  
- ExifTool  
- Diff utilities  
- Wireshark  
- tshark  
- Text and log viewing tools  

### Forensic Principles  
- Repeatability  
- Integrity preservation  
- Documentation of each step  

*Note:* This section will later include diagrams or flowcharts for clarity.

---

# 4. Analysis Findings (Draft Outline)

This section will be expanded into full paragraphs in the final report.  
Current notes reflect the key findings that will be written more formally later.

---

## 4.1 PDF Metadata Findings

### Key Points to Develop  
- Final W-2 showed creation and modification timestamps on the same afternoon.  
- Modification timestamp occurred shortly before upload activity.  
- Metadata fields (creator, software) differed from typical employer-issued documents.  
- Draft W-2 had normal metadata with no signs of tampering.

### Draft Wording  
“Metadata analysis revealed discrepancies in the final version of the W-2, including modification timestamps and inconsistent software signatures. These indicators support the possibility of local document alteration.”

---

## 4.2 Draft vs Final Comparison

### Key Points to Develop  
- Metadata diff highlighted specific changes.  
- Differences included:  
  - Modification time  
  - PDF software identifiers  
  - Author fields  
- Final version appeared regenerated rather than officially issued.

### Draft Wording  
“Comparison between the draft and final documents showed several inconsistencies that would not normally be present in a legitimate employer reissue.”

---

## 4.3 Email Header Findings

### Key Points to Develop  
- Suspicious email used a non-lender domain.  
- Formatting and header structure did not match legitimate communications.  
- Timestamp aligns with the document modification period.  
- Legitimate lender emails show consistent patterns.

### Draft Wording  
“Email header analysis identified discrepancies in sender information and formatting, suggesting that the message associated with the submission was not sent from an authorized lender account.”

---

## 4.4 Network Activity Findings

### Key Points to Develop  
- POST request detected showing upload of a file.  
- Upload occurred minutes after W-2 modification.  
- Source was the local workstation.  
- Destination was the simulated lender upload endpoint.

### Draft Wording  
“The network capture confirmed that a file was uploaded using an HTTP POST shortly after the document was modified, supporting the hypothesis that the workstation was used to transmit the altered W-2.”

---

## 4.5 SSH Log Findings

### Key Points to Develop  
- Failed login attempts from unfamiliar IP `192.0.2.5`.  
- Occurred near the timeframe of document editing.  
- No successful remote access confirmed.

### Draft Wording  
“Authentication log review revealed repeated failed login attempts from an external IP address shortly before the document was modified. Although no successful login occurred, these attempts provide context for potential system probing or misuse.”

---

# 5. Preliminary Interpretation (Draft)

### Points to Develop into Full Paragraphs  
- Evidence suggests intentional local editing of the W-2 document.  
- Upload behavior aligns with the timing of document modification.  
- Email irregularities reinforce a pattern of intentional submission outside normal workflows.  
- SSH attempts add contextual suspicion but are not conclusive on their own.

### Draft Wording  
“Taken as a whole, the evidence points toward deliberate modification and submission activity conducted from the workstation.”

---

# 6. Report Items to Finalize

### Items to Expand  
- Full narrative paragraphs for each analysis area  
- Formal introduction and closing statements  
- Tables summarizing metadata, timestamps, and upload events  
- Figures/screenshots referenced in the narrative  
- A polished conclusion describing the investigation’s findings  

### Items Still Needed  
- Final timeline (to be created later)  
- Final recommendations section  
- References appendix  
- Evidence appendix list (file names only, no hashes)

---

# 7. Conclusion (Draft Notes)

### Initial Thoughts to Develop  
- Evidence supports a strong connection between document alteration and subsequent upload activity.  
- Email and metadata inconsistencies reinforce this pattern.  
- All observed evidence aligns with potential fraudulent submission behavior.

*Note:* Final conclusion will be expanded after timeline creation.

---

