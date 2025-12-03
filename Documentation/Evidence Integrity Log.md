# Evidence Integrity Log


---

# 1. Overview

This document contains the complete integrity verification records for all evidence imported during Milestone 1.  
All SHA-256 hashes were generated inside the forensic VM immediately after importing and organizing the evidence ZIP file, ensuring the evidence remained unaltered and forensically sound.

Integrity logs provide the baseline that all future milestones will compare against.

---

# 2. Evidence Items Included

The following evidence items were hashed:

- Five W-2 PDF documents  
  - Three legitimate  
  - One draft version  
  - One fraudulent final version  
- Two email files  
  - One legitimate lender email  
  - One fraudulent email  

Original evidence copies are stored in:

- `~/Documents/MortgageApps/`  
- `~/Documents/Emails/`

Integrity logs are stored in:

- `~/Forensics/Logs/`

---

# 3. Hashing Procedure

SHA-256 hashing was performed using the commands below:

## 3.1 PDF Hash Generation

    cd ~/Documents/MortgageApps
    sha256sum *.pdf | tee ~/Forensics/Logs/pdf_hashes.sha256

## 3.2 Email Hash Generation

    cd ~/Documents/Emails
    sha256sum *.eml | tee ~/Forensics/Logs/email_hashes.sha256

## 3.3 Combined Manifest Creation

    cat ~/Forensics/Logs/pdf_hashes.sha256 \
    ~/Forensics/Logs/email_hashes.sha256 \
    > ~/Forensics/Logs/evidence_hash_manifest.txt

All commands were executed by Juliana Garza to preserve custody and prevent unauthorized modification.

---

# 4. PDF SHA-256 Hash Values (Actual Values)

The following are the **real hash values** generated inside the forensic VM:

    aaac362a177d7d47c0c2b2e7ee21fdfadd97ce32a4560b7fe478b4499c9a696c W2_Alice.pdf
    938d29462e11cf04f77345424de8fe46af1a5617f3ebacf083f3ffc7a15f4d09 W2_Bob.pdf
    05e525f37d971c7fcd0d3fe4e3ef79379f76c6899f2176b9f73dba12b5f96fc8 W2_Carol.pdf
    c769b15fcb509cc44597e727eb43d93e11ed965e50759ecf39209527939f6c31 W2_JDoe_draft.pdf
    654cc8a152f1994ed6094b69eabd90dda8b413daf7a46d7a9ca3b170fb7323a4 W2_JDoe_final.pdf


These values represent the complete and authentic state of all PDF evidence.

---

# 5. Email SHA-256 Hash Values (Actual Values)

     868e05f860017aa10288d9ee33eee806a81cbc392ff732a2b2492f986f4b13de fraud_jdoe.eml
     2246769164add3a5808aa39caefa949e59c0ccc27f2d353b55b11569c58444a2 lender_alice.eml


These represent the legitimate and fraudulent communication preserved from the ZIP file.

---

# 6. Combined Evidence Manifest

The consolidated manifest containing all hashes is stored at:

- `~/Forensics/Logs/evidence_hash_manifest.txt`

This file combines hashes for every evidence item, creating a single baseline record used during later forensic validation.

---

# 7. Integrity Verification Notes

- All hash values were generated **before analysis**, ensuring the originals remained untouched.  
- No evidence files were modified, renamed, or opened prior to hashing.  
- Evidence remained local to the VM.  
- Any future mismatch between these values and recalculated hashes will indicate tampering or corruption.  
- Only Juliana Garza handled and hashed the files, maintaining clean custody.

---

# 8. Integrity Declaration

I, **Juliana Garza**, certify that:

1. All evidence files were hashed immediately after extraction .
2. The hash values recorded reflect the exact state of the evidence at the time of acquisition.  
3. No alterations, modifications, or unauthorized access occurred during hashing.  
4. This log establishes the official forensic integrity baseline for the investigation.

**Signature:**  
*Juliana Garza*  
Milestone 1 – Evidence Integrity Log

---
