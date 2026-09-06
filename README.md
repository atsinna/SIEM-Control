## SIEM-Control
I'll be using security and network principles for this project. I'll be focused on monitoring and detecting anomolies that appear on my network. The scope of this project is to gauge my understanding on SIEM principles and learn in my own environment. 

## Home Network Security Lab

An ongoing project to document a home network, establish a security baseline, and gradually build centralized monitoring and incident-response capabilities.

# Current stage

Foundation: an initial device inventory, network diagram, and Windows security baseline have been documented. Hardening validation and SIEM deployment are upcoming work.

# Work documented

Inventoried 17 devices, including two network devices and 15 clients.

Created an inventory-based network diagram showing wired and wireless connections.

Documented PowerShell commands for examining established TCP connections and listening services.

Identified unfamiliar services and a VirtualBox host-only network interface.

Recorded a limited DNS observation and reviewed Windows authentication events.

# What I learned

Service and interface details helped explain unfamiliar listeners. A listening port alone did not establish internet exposure. Limited traffic snapshots and individual authentication events required further context before drawing security conclusions.

# Limitations

The baseline covers initial observations rather than continuous monitoring. TCP snapshots do not include UDP endpoints.
Device trust labels and potential log availability have not been independently validated, and the diagram does not represent VLAN segmentation.

## Next steps

Refine the baseline and resolve remaining inventory uncertainties.

Review and document network and endpoint hardening.

Select and deploy one monitoring platform.

Verify log ingestion before building and testing detections.

# Data handling

Public artifacts use sanitized device identifiers and omit personal ownership details and real MAC addresses. Any illustrative addresses are labeled. Original inventories and raw evidence remain private.
