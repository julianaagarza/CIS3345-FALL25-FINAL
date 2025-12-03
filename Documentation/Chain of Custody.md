# Chain of Custody


---

# 1. Overview

This document records the full chain of custody for all original evidence used in the Mortgage Fraud VM scenario. It documents who collected, transferred, handled, and stored each piece of evidence beginning with the import of the evidence ZIP file.

Proper chain of custody ensures that digital evidence was acquired, preserved, and stored in a manner consistent with forensic best practices.

---

# 2. Evidence Items Included

The evidence ZIP file contained the following items:

- Multiple W-2 PDF documents (legitimate and fraudulent)
- Draft and final versions of John Doe’s W-2
- Email files in `.eml` format (legitimate lender and fraudulent sender)
- Fake lender upload portal components
- Supporting scenario files

All items were preserved exactly as extracted. No original evidence files were modified.

---

# 3. Evidence Acquisition

## 3.1 Source of Evidence
The evidence was provided as:

- `mortgage_lab_files.zip`

This ZIP file was made available on the host system for transfer via a VirtualBox shared folder.

## 3.2 Transfer into VM
The ZIP file was transferred into the VM using the shared folder:

- **Shared Folder Name:** sf_DF  
- **Mount Location:** `/media/sf_DF/`

The ZIP file was copied into the VM using:

    cp /media/sf_DF/mortgage_lab_files.zip ~/

This ensured a direct, unaltered read-only copy into the forensic workstation.

## 3.3 Extraction
The ZIP file was extracted inside the VM using:

    unzip mortgage_lab_files.zip -d ~/mortgage_lab_files/

This created a controlled directory containing all evidence items for forensic use.

---

# 4. Evidence Storage Locations

After extraction, the evidence was organized as follows:

- **W-2 PDF Documents:**  
  `~/Documents/MortgageApps/`

- **Email Files:**  
  `~/Documents/Emails/`

- **Fake Lender Portal Files:**  
  `~/FakePortal/`

- **Log and Hash Files:**  
  `~/Forensics/Logs/`

This structure maintains clear separation between original evidence and analysis output.

---

# 5. Evidence Integrity Verification

SHA-256 hashes were generated to prove the evidentiary integrity.

## 5.1 PDF Hashing

    cd ~/Documents/MortgageApps
    sha256sum *.pdf | tee ~/Forensics/Logs/pdf_hashes.sha256

## 5.2 Email Hashing

    cd ~/Documents/Emails
    sha256sum *.eml | tee ~/Forensics/Logs/email_hashes.sha256

## 5.3 Combined Hash Manifest

    cat ~/Forensics/Logs/pdf_hashes.sha256 \
    ~/Forensics/Logs/email_hashes.sha256 \
    > ~/Forensics/Logs/evidence_hash_manifest.txt

These logs form the baseline integrity record for the remainder of the case.

---

# 6. Custody Timeline (December 3rd, 2025)

The following timestamps reflect the actual sequence of evidence handling activities on **2025-12-03**. All times are in **Central Standard Time (CST, UTC-06:00)**.

| Date & Time (ISO 8601)        | Person          | Action                           | Notes |
|-------------------------------|-----------------|----------------------------------|-------|
| 2025-12-03T09:08:12-06:00     | Juliana Garza   | Acquired evidence ZIP            | Retrieved from host via sf_DF shared folder |
| 2025-12-03T09:10:47-06:00     | Juliana Garza   | Copied ZIP into VM               | ZIP copied without modification |
| 2025-12-03T09:13:26-06:00     | Juliana Garza   | Extracted ZIP contents           | Extracted into ~/mortgage_lab_files/ |
| 2025-12-03T09:19:58-06:00     | Juliana Garza   | Organized evidence files         | PDFs and EMLs moved to dedicated directories |
| 2025-12-03T09:24:35-06:00     | Juliana Garza   | Verified evidence accessibility  | Confirmed files readable and intact |
| 2025-12-03T09:31:14-06:00     | Juliana Garza   | Generated PDF SHA-256 hashes     | Logged to pdf_hashes.sha256 |
| 2025-12-03T09:33:02-06:00     | Juliana Garza   | Generated EML SHA-256 hashes     | Logged to email_hashes.sha256 |
| 2025-12-03T09:34:21-06:00     | Juliana Garza   | Created combined manifest        | evidence_hash_manifest.txt created |
| 2025-12-03T09:39:44-06:00     | Juliana Garza   | Verified hash logs               | Confirmed all integrity logs complete |
| 2025-12-03T09:45:57-06:00     | Juliana Garza   | Created VM snapshot              | Snapshot saved as “EnvironmentReady” |

---

# 7. Handling Notes

- Evidence remained entirely within the VM after import.  
- No network transfers, removable drives, or cloud services were used.  
- All hash values were recorded before any analysis occurred.  
- Permissions and folder structure were preserved during the entire process.  
- Only Juliana Garza handled the evidence during the setup.  
- A VirtualBox snapshot preserves the exact environment state.

---

# 8. Chain of Custody Declaration

I, **Juliana Garza**, certify that:

1. All evidence was received in its original form.  
2. Evidence was transferred into the VM securely and without modification.  
3. SHA-256 integrity verification was performed immediately after acquisition.  
4. Evidence was stored in an organized, controlled directory structure.  
5. No unauthorized access or modification occurred during Milestone 1.  
6. The environment state was preserved in a VirtualBox snapshot.

**Signature:**  
*Juliana Garza*  


---
