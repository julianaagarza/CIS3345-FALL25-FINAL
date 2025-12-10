# Network Findings Summary  

---

## Overview
This document summarizes the results of the network traffic review completed by the technical analyst.  
The purpose of this analysis was to determine whether the workstation transmitted any files or communicated with external endpoints in a way that relates to the suspected document alteration.

The captured network activity was recorded in a packet capture (PCAP) file and examined using Wireshark and supporting tools.

---

## PCAP Examination

### Activity Observed
The PCAP revealed outbound HTTP POST activity originating from the workstation. POST requests typically indicate that data is being uploaded rather than downloaded.

Key observations include:

- A POST request directed to a local web service endpoint  
- Upload activity occurring shortly after the modified W-2 document’s last known edit time  
- HTTP fields consistent with file submission behavior  

### Relevance
The presence of an upload event is significant because:

- The timing aligns closely with the suspected document modification  
- POST requests can be used to transmit files to external systems  
- The workstation was the origin of the request, supporting the possibility that the altered file was submitted from this environment  

These patterns help correlate user activity with evidence of document handling and submission.

---

## Source and Destination Details

### Information Provided by the Analyst
The network analysis extracted the following characteristics:

- **Source:** The workstation that generated the suspected file  
- **Destination:** A local upload endpoint used in the scenario  
- **Method:** HTTP POST transmission  
- **Data Type:** Form-style upload fields consistent with submitting a document  

### Interpretation
Even though the destination was a local endpoint rather than a remote server, the POST transaction still demonstrates intentional upload behavior.  
This aligns with the hypothesis that someone used the workstation to submit a document—potentially the altered W-2.

---

## Timing of Events

### What the Analyst Reported
The POST request occurred within a short window following the modification of the final W-2 document. This temporal alignment strengthens the connection between:

1. **Document modification**  
2. **Upload activity**  

### Why This Matters
Establishing temporal relationships is a core part of forensic analysis.  
When two suspicious events occur in close sequence, it supports a narrative of intentional action rather than coincidence.

---

## Summary of Network Findings
- Network traffic shows a POST upload event originating from the workstation.  
- The upload timing closely follows the modification time of the W-2 document.  
- The POST request structure is consistent with document submission behavior.  
- These findings support the possibility that the altered W-2 was uploaded using this workstation.

---

## Documentation Stored
The following network-related artifacts have been organized in the project documentation:

- PCAP screenshots and filtered views  
- Extracted Wireshark summaries  
- Notes describing upload patterns and timestamps  

These materials support reporting, validation, and the final presentation.

