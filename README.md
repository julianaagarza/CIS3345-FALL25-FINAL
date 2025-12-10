# Mortgage Fraud Digital Forensics Investigation  
CIS 3345 – Fall 2025  
University of the Incarnate Word  

---

## Project Overview

This project simulates a real-world digital forensic investigation involving suspected mortgage document fraud. Internal reviewers at a lending institution noticed irregularities in a W-2 submitted for a borrower named John Doe. The loan officer responsible for processing the file claimed that all documents were uploaded exactly as received from the applicant. However, several system indicators suggested possible misconduct.

---

## Case Scenario: The Suspicious Loan Officer – A Mortgage Document Fraud Case

### Core Concept: 
- We are digital forensic investigators assigned to analyze activity on a loan officer’s workstation. A W-2 document submitted during a mortgage application appeared inconsistent with employer-issued files. The timing of events on the loan officer’s computer raised concerns that the document may have been altered and uploaded internally rather than provided by the borrower.

### Background Scenario:
**Several red flags were discovered:**

- Failed SSH login attempts occurred shortly before the suspicious activity window.  
- A final W-2 file for John Doe was created and modified within minutes—unusual for authentic employer documents.  
- A suspicious email resembling lender communication was sent around the same time but contained domain and formatting inconsistencies.  
- Network activity showed an HTTP POST upload of a W-2 file shortly after the modifications occurred.

Because these events all occurred closely together, the lender initiated a forensic review to determine whether the workstation had been used to alter and submit a falsified document.

---

## Key Forensic Tasks Performed:

- **Verify Evidence Integrity:** Checked SHA-256 hashes of all PDFs, EML files, and logs.  
- **Analyze W-2 Metadata:** Used ExifTool to review timestamps, creator fields, and modification history.  
- **Compare Draft vs Final Files:** Identified differences between original and altered versions.  
- **Examine Email Headers:** Verified sender authenticity and detected spoofing indicators.  
- **Review Network Traffic:** Analyzed PCAP files for POST uploads and correlated the upload timing with document edits.  
- **Inspect SSH Logs:** Identified failed login attempts originating from an external IP.  

This scenario allowed the team to practice real forensic workflows such as maintaining evidence integrity, applying multiple forensic tools, and correlating multiple forms of digital evidence to reach a conclusion.

---

## Tools Used
- **ExifTool** – PDF metadata extraction  
- **Wireshark** – Network traffic inspection  
- **tshark** – Structured packet data export  
- **Ubuntu 24.04** – Forensic analysis platform  

---

## Milestone Summary

### **Milestone 1 – Environment Setup & Evidence Preservation**  
Established the forensic VM, installed tools, imported evidence, validated integrity, and documented the chain of custody.

### **Milestone 2 – Metadata & Email Analysis**  
Reviewed W-2 metadata, compared draft and final versions, and analyzed email headers for signs of spoofing.

### **Milestone 3 – Network & Log Forensics**  
Inspected PCAP files for upload activity, extracted structured POST data, and reviewed SSH logs for suspicious login attempts.

### **Milestone 4 – Report Development & Validation**  
Drafted and validated the full forensic report and organized appendices.

### **Milestone 5 – Final Presentation & Submission**  
Created and delivered the case presentation summarizing findings and methodology.

---

## How to Navigate the Wiki
The Wiki contains full technical documentation, including:

- Case summary and scenario background  
- Chain of custody & evidence intake  
- Detailed methodology  
- Metadata, email, network, and log findings  
- Consolidated timeline  
- Final interpretations   

---

## How to Reproduce the Environment (Short Overview)
1. Import Ubuntu 24.04 VM into VirtualBox.  
2. Install ExifTool, Wireshark, tshark, PHP, and Git.  
3. Import evidence ZIP via shared folder.  
4. Create required directory structure.  
5. Compute SHA-256 hashes.  
6. Follow analysis steps outlined in the Wiki.

---

## License
This project was completed for CIS 3345 – Digital Forensics.  
All evidence is fictional and created solely for educational use.

---

## Story Point Contribution Summary

| Member | Total Story Points | Contribution Percentage |
|--------|---------------------|------------------------|
| **Juliana Garza** | **36** | **55%**  
| **Jaime Knott**   | **30** | **45%**
