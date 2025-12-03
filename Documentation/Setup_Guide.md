# Setup Guide For Virtual Environment

---

# 1. Overview

This document explains how the forensic virtual machine was created, how tools were installed, how the evidence ZIP file was imported using the shared folder **sf_DF**, and how the environment was prepared for all later investigation milestones.

---

# 2. Virtual Machine Setup

## 2.1 Create the Ubuntu 24.04 VM

A new VM was created in **Oracle VirtualBox** with the following configuration:

- **Name:** MortgageFraud-Workstation  
- **Type:** Linux  
- **Version:** Ubuntu (64-bit)  
- **Memory:** 8000 MB  
- **CPUs:** 3
- **Disk:** 35GB

The Ubuntu 24.04 ISO was attached under:

- **Settings → Storage → Empty Disk → Choose a disk file**

Ubuntu Desktop 24.04 was installed normally and a user account was created:

- **Username:** loanofficer

After installation, system updates were applied:

    sudo apt update
    sudo apt upgrade -y

A baseline snapshot was taken in VirtualBox:

- **Machine → Take Snapshot → “Clean State”**

---

# 3. Enable VM Integrations

## 3.1 Install Guest Additions

Inside the running VM:

- **Devices → Insert Guest Additions CD Image**
- Chose **Run**
- Entered password when prompted
- Allowed installation to finish
- Restarted VM afterward

## 3.2 Enable Shared Clipboard & Drag-and-Drop

With the VM powered off:

- **Settings → General → Advanced**
  - Shared Clipboard: **Bidirectional**
  - Drag’n’Drop: **Bidirectional**

---

# 4. Create Forensic Working Directories

Inside the VM, the following directories were created to organize evidence and analysis output:

    mkdir -p ~/Documents/MortgageApps
    mkdir -p ~/Documents/Emails
    mkdir -p ~/Forensics/Logs
    mkdir -p ~/Forensics/Analysis

These directories maintain separation between **original evidence** and **analysis artifacts**.

---

# 5. Install Required Forensic Tools

All required tools were installed:

    sudo apt install -y wireshark tshark exiftool apache2 php git unzip zip tree

Additional configuration allowed packet capture without root:

    sudo dpkg-reconfigure wireshark-common
    sudo usermod -aG wireshark "$USER"
    newgrp wireshark

Apache was enabled for the fraudulent upload simulation:

    sudo systemctl enable apache2
    sudo systemctl start apache2

---

# 6. Import Evidence ZIP File (via sf_DF Shared Folder)

A ZIP file named `mortgage_lab_files.zip` was provided through the VirtualBox shared folder.

## 6.1 Shared folder mapping
The following shared folder was configured on the host:

- **Name:** sf_DF  
- **Auto-mount:** Enabled  
- **Make Permanent:** Enabled  

Inside the VM, it appeared at:

- `/media/sf_DF/`

## 6.2 Copy the ZIP into the VM

    cp /media/sf_DF/mortgage_lab_files.zip ~/

## 6.3 Extract ZIP contents into a working directory

    unzip mortgage_lab_files.zip -d ~/mortgage_lab_files/

The extracted ZIP contained:

- Multiple W-2 PDF files  
- Legitimate lender emails  
- Fraudulent email  
- Draft vs final John Doe PDFs  
- Fake lender upload portal folder  

---

# 7. Organize Evidence Into Proper Directories

All extracted files were placed into the directories created earlier.

Move PDFs:

    cp ~/mortgage_lab_files/*.pdf ~/Documents/MortgageApps/

Move emails:

    cp ~/mortgage_lab_files/*.eml ~/Documents/Emails/

Move fake portal folder:

    cp -r ~/mortgage_lab_files/lender_uploads ~/FakePortal/

---

# 8. Verify Tool Installation & Evidence Accessibility

Check tools:

    wireshark --version
    tshark --version
    exiftool -ver
    php -v

Check evidence folders:

    ls -l ~/Documents/MortgageApps
    ls -l ~/Documents/Emails

Check fake portal folder:

    ls -l ~/FakePortal

---

# 9. Evidence Hashing (Integrity Verification)

Hashes were generated for all PDF and email files.

## 9.1 Hash PDFs

    cd ~/Documents/MortgageApps
    sha256sum *.pdf | tee ~/Forensics/Logs/pdf_hashes.sha256

## 9.2 Hash Emails

    cd ~/Documents/Emails
    sha256sum *.eml | tee ~/Forensics/Logs/email_hashes.sha256

## 9.3 Combine Into One Manifest

    cat ~/Forensics/Logs/pdf_hashes.sha256 \
    ~/Forensics/Logs/email_hashes.sha256 \
    > ~/Forensics/Logs/evidence_hash_manifest.txt

This manifest serves as proof that original evidence was not modified.

---

# 10. Final Snapshot

After tool installation and evidence setup, a second snapshot was created:

- **Name:** M1_EnvironmentReady  
- **Purpose:** Fully prepared baseline to restore before analysis tasks

---

# 11. Completion Summary

Milestone 1 included:

- VM creation and configuration  
- Guest Additions, shared clipboard, and drag-and-drop  
- Evidence ZIP import via **sf_DF** shared folder  
- Evidence extraction and organization  
- Folder structure creation  
- All forensic tools installed  
- SHA-256 integrity hashing performed  
- Snapshots created for reproducibility  


---
