# Validation Notes  

---

## Overview
These notes describe the validation checks performed after the initial analysis.  
The goal of this phase is to ensure:

- All analysis steps can be repeated with the same results  
- No evidence changed during the investigation  
- All findings are supported by consistent and verifiable data  

Validation is essential in digital forensics because conclusions must remain reliable regardless of when or by whom the steps are repeated.

---

## 1. PDF Metadata Re-Extraction

### Procedure
- Metadata for all W-2 documents was re-extracted using the same ExifTool commands originally used by the analyst.  
- Full metadata dumps were compared to the previously saved outputs.

### Validation Result
- Output matched the original metadata summary and full metadata files.  
- No fields showed unexpected changes or discrepancies.  
- Creation and modification timestamps remained identical to the initial extraction.

### Conclusion
Metadata extraction is reproducible, and the PDF files remained unchanged.

---

## 2. Draft vs Final File Comparison Recheck

### Procedure
- The diff between **W2_JDoe_draft.pdf** and **W2_JDoe_final.pdf** metadata was regenerated.  
- The newly generated diff file was compared to the previously saved version.

### Validation Result
- The diff output matched the original comparison exactly.  
- Differences in modification time, author fields, and software identifiers appeared consistently.

### Conclusion
The comparison is reproducible, and no metadata changed between runs.

---

## 3. Email Header Verification

### Procedure
- Header fields from each `.eml` file were viewed again using text-based tools.  
- Key fields (`From`, `To`, `Date`, `Subject`) were cross-checked with the previously recorded results.

### Validation Result
- The suspicious email continued to show a mismatched sender domain and formatting inconsistencies.  
- Legitimate lender emails retained their consistent domain and timestamp structure.  
- No `.eml` content had changed.

### Conclusion
Email header findings are stable and fully reproducible.

---

## 4. Network POST Event Re-Extraction (tshark)

### Procedure
- The tshark command used earlier was re-run to extract POST events into a new CSV output.  
- The timestamps, source/destination IPs, and request URI were compared to the first extraction.

### Validation Result
- All fields matched the initial CSV produced by the analyst.  
- The POST upload event remained present with identical timestamp and metadata.

### Conclusion
Network extraction results are repeatable and consistent with earlier findings.

---

## 5. PCAP Re-Inspection (Wireshark)

### Procedure
- Wireshark was reopened and the same display filters were applied (`http.request.method == "POST"`).  
- The analyst verified that the same upload packet appeared in the filtered results.

### Validation Result
- The POST request appeared in the same position with the same timestamp and fields.  
- No packets had changed or disappeared.

### Conclusion
PCAP data remains intact, and network findings are reproducible.

---

## 6. SSH Authentication Log Re-Review

### Procedure
- `/var/log/auth.log` was searched again for references to the suspicious IP address (`192.0.2.5`).  
- Failed login attempts and timestamps were cross-checked with earlier notes.

### Validation Result
- The same failed login entries appeared with no differences.  
- No new login events emerged.  
- No successful remote login events were found.

### Conclusion  
SSH log findings remain unchanged and confirm consistent system behavior.

---

## 7. Evidence Integrity Confirmation

### Procedure
- File hashes recorded during the initial collection stage were compared to new hashes generated during validation.  
- All PDF, email, and log files were included.

### Validation Result
- All hash values matched the original hash log.  
- No files showed evidence of alteration or corruption.

### Conclusion
Evidence integrity has been preserved throughout the investigation.

---

## Overall Validation Summary
- All major analysis steps were repeated successfully.  
- No discrepancies were found between initial results and validation results.  
- Evidence files remained unchanged, as confirmed through hashing and repeated analysis.  
- The investigation’s findings are reproducible, defensible, and suitable for final reporting.

---

