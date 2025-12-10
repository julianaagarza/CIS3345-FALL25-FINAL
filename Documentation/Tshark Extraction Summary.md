# Tshark Extraction Summary  

---

## Overview
This document explains the extracted upload activity obtained through tshark.  
While Wireshark provides a visual inspection of network packets, tshark allows the analyst to export specific fields for easier comparison, documentation, and timeline construction.

The primary goal of this extraction was to gather clear, structured information about any HTTP POST requests associated with the workstation.

---

## Extraction Method
The technical analyst used tshark to extract fields relevant to document submission behavior.  
The extraction targeted HTTP POST events and collected:

- Timestamp of each POST request  
- Source IP address  
- Destination IP address  
- The request URI (upload path)  
- Additional header information when available  

This data was saved to a CSV file for later use.

### Why This Matters
Structured data allows investigators to:

- More easily identify patterns in upload behavior  
- Compare timestamps against document modification logs  
- Prepare information for forensic reporting and presentation  
- Validate findings across multiple tools  

Tshark is particularly valuable when building timelines because it outputs predictable, machine-readable fields.

---

## Key Findings from the Extraction

### POST Upload Event
The extracted CSV showed a POST request that matched the upload activity previously noted in Wireshark.  
Important characteristics provided by the analyst include:

- The POST request originated from the same workstation where the W-2 document was modified  
- The destination was a local upload endpoint  
- The URI indicated document submission activity  

### Timing Observations
The timestamp recorded in the tshark output closely aligns with:

- The final modification time of the suspect W-2 document  
- The expected timeframe in which the upload occurred  

This reinforces the connection between document handling and network transmission.

---

## Interpretation of Results

### Relationship to Document Activity
The structured tshark output adds clarity to the investigator’s understanding of what occurred:

- It confirms that the upload event happened  
- It verifies when it happened  
- It ties the activity directly to the workstation  
- It supports the hypothesis that the altered document was submitted from this system  

### Contribution to the Case
This data strengthens the investigation in several ways:

- Confirms the upload identified visually in Wireshark  
- Provides timestamps suitable for inclusion in a forensic timeline  
- Offers reliable structured evidence for reporting  
- Supports the narrative that the workstation was used for submission activity shortly after file modification  

---

## Summary
The tshark extraction produced clear, structured evidence of POST upload activity.  
This reinforces the findings from Wireshark and provides essential data for later stages of the investigation, including timeline development and report writing.

