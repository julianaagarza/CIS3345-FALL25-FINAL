# Analysis Methodology  

---

## Overview
This methodology explains how the document and email evidence was examined using forensic tools.  
The purpose of these procedures was to determine whether any files showed signs of tampering, modification, or inconsistent communication patterns.

All steps were completed using a controlled Ubuntu 24.04 forensic environment.  
No original files were altered during the analysis.

---

## 1. Preparation of the Analysis Workspace

### Procedures
- The analyst worked inside a dedicated forensic virtual machine.
- Evidence files (PDF documents and email files) were placed in structured directories:
  - `~/Documents/MortgageApps/` for PDFs  
  - `~/Documents/Emails/` for `.eml` files
- A separate analysis directory (`~/Forensics/Analysis/`) was used to store all extracted metadata, comparison files, and summary notes.
- The primary tools installed for this phase were:
  - **ExifTool** — used to extract PDF metadata
  - **Text-based utilities** — used to review email headers and message structures

### Rationale
A consistent environment ensures accurate results and prevents accidental modification of evidence.  
Segregating working files from original evidence maintains integrity and supports forensic documentation standards.

---

## 2. PDF Metadata Examination

### Purpose
To determine whether any document showed irregular metadata—such as mismatched timestamps or unusual software information—that could indicate unauthorized edits.

### Procedures
- ExifTool was used to extract key metadata fields from each PDF, such as:
  - File creation date  
  - File modification date  
  - Author  
  - Creator  
  - Software used to generate the file  
- A metadata summary file was generated and saved for reference.
- Full metadata dumps for each file were exported to allow deeper inspection when needed.

### Rationale
Metadata often reveals information not visible in the document contents.  
Unexpected software names, unexpected modification dates, and conflicting author fields may indicate local editing or unauthorized document manipulation.

---

## 3. Draft vs Final Document Comparison

### Purpose
To determine whether the applicant’s draft W-2 and final W-2 were created under consistent conditions, or whether the final version may have been altered.

### Procedures
- Metadata from **W2_JDoe_draft.pdf** and **W2_JDoe_final.pdf** was compared side-by-side.
- A diff file was generated to highlight every differing field between the two metadata outputs.
- Key attention was given to:
  - Timestamp inconsistencies  
  - Different author or creator names  
  - Different PDF software signatures  
  - Modification dates that occurred unusually close to submission activity  
- Observations were documented in a comparison notes file.

### Rationale
A legitimate final W-2 typically shares consistent metadata with its original version.  
Differences between the draft and final files may indicate local editing, regeneration, or the use of unauthorized software.

---

## 4. Email Header Examination

### Purpose
To determine whether a suspicious email was legitimately sent by the lender or originated from another source attempting to impersonate the lender.

### Procedures
- Raw `.eml` files were opened using Linux text tools.
- Key header fields were extracted and recorded:
  - `From` address and domain  
  - `To` address  
  - `Subject`  
  - `Date`  
- The suspicious email was compared to legitimate lender emails to identify:
  - Inconsistent sender domains  
  - Differences in header structure  
  - Unusual timestamps  
  - Formatting abnormalities  
- Notes were saved documenting observed discrepancies.

### Rationale
Email headers are reliable forensic sources.  
A mismatch between legitimate sender domains and suspicious email domains is a strong indicator of impersonation.  
Unusual routing or inconsistent header formatting can reveal fraudulent activity.

---

## 5. Summary of Applied Methods

### Methods Used
- Metadata extraction using ExifTool  
- Side-by-side metadata comparison using text diff tools  
- Manual header examination of `.eml` files  

### What These Methods Achieve
- Identify whether PDFs show signs of unauthorized editing  
- Reveal inconsistencies between document versions  
- Confirm whether emails originate from trusted sources  

### Overall Outcome
This methodology establishes a foundation for determining whether document tampering or communication irregularities suggest fraudulent intent.

---

