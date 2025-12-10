# Analysis Findings Summary  

---

## Overview
Our analysis focused on examining the **documents** and **emails** included in the mortgage fraud investigation.  
Jaime Knott performed all technical metadata and email header analysis, and this summary consolidates those findings in a clear, report-ready format.

The purpose of this milestone was to determine whether any evidence suggested **document tampering**, **email irregularities**, or **inconsistencies** in how the files were created, modified, or communicated.

---

## 1. PDF Metadata Examination

### **Files Analyzed**
- All W-2 PDFs in the MortgageApps evidence folder  
- Special focus on:  
  - **W2_JDoe_draft.pdf**  
  - **W2_JDoe_final.pdf**

### **Key Findings**
- **Timestamps indicated modification:**  
  The metadata for the *final* version showed a modification time that did not align with expected employer-issued documents.
  
- **Author/Creator fields differed:**  
  The draft and final files had inconsistent creator/author metadata, suggesting the document may have been processed or edited using different software.

- **Draft vs Final Comparison:**  
  A diff between the metadata dumps showed multiple field disparities that would not normally appear in an official W-2 reissue.

### **Interpretation**
These inconsistencies support the possibility that the final W-2 was edited or recreated locally rather than issued through an official payroll system.

---

## 2. Document Timeline Indicators

### **File Modification Times**
Jaime Knott extracted modification times for every PDF and compiled them into a CSV. These timestamps helped establish:

- When each file was last altered  
- Whether the timing aligned with other pieces of evidence (such as emails or network uploads)

### **Key Observations**
- The **final** John Doe W-2 displayed a modification timestamp that occurred shortly before the suspicious upload captured in the network PCAP.
- Other applicants’ W-2 files did not show similar irregularities.

### **Interpretation**
The timing strongly suggests intentional modification prior to submission.

---

## 3. Email Header Analysis

### **Files Analyzed**
- Lender notification emails  
- A suspicious email associated with the John Doe submission  

### **Key Findings**
- **Sender domain mismatch:**  
  The suspicious email did not come from the lender’s official domain, unlike the legitimate messages.

- **Header inconsistencies:**  
  Timestamps and mail routing lines indicated the message was sent from a non-official source.

- **Tone and formatting differences:**  
  Legitimate lender emails had consistent structure and phrasing, while the suspicious message lacked the same formatting.

### **Interpretation**
Email header analysis supports the conclusion that the message was **not sent by the lender**, but rather by an individual attempting to impersonate them or bypass formal communication channels.

---

## 4. Correlation Across Evidence Types

### **Cross-Evidence Alignment**
After reviewing metadata, timestamps, and email headers, several patterns emerged:

- The modified W-2 aligned closely with the sending time of the suspicious email.
- The email appeared designed to accompany or justify the altered document.
- Legitimate lender messages did not show any anomalies.

### **Interpretation**
Taken together, these findings establish a **credible pattern of document manipulation and inconsistent communication behavior**, laying groundwork for deeper investigation in Milestone 3.

---

## 5. Summary of Findings

### **Indications of Fraudulent Activity**
- Metadata reveals modification of the final W-2 file.
- Draft and final versions differ in critical metadata fields.
- Document timestamps do not align with normal employer workflows.
- Email discrepancies raise questions about authenticity and intent.

### **Next Steps**
- Validate these findings against network activity (POST uploads).  
- Review system logs for unauthorized access patterns.  
- Build a comprehensive timeline that ties together document edits, email activity, and network uploads.

---

## Documentation Stored
The following files were created by Jaime Knott and included in the analysis directory:

- `metadata_summary.txt`  
- `JDoe_draft_vs_final.diff`  
- `file_times.csv`  
- `headers_min.txt`  
- `comparison_notes.txt`  

---

