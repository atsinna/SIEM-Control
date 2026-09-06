# Home network incident response roadmap

## Current position

The project is in the foundation stage. An initial asset inventory, topology, and Windows baseline are documented. This roadmap defines future work and completion standards; it is not evidence that those standards have been met.

| Phase | Status |
| --- | --- |
| 1. Define the environment | Initial inventory and diagram documented; validation continues |
| 2. Establish a baseline | Initial Windows observations documented; coverage expansion planned |
| 3. Harden the network | Planned; completed changes are not documented in this package |
| 4. Build monitoring | Planned |
| 5. Develop detections | Planned |
| 6. Create response procedures | Planned |
| 7. Run controlled simulations | Planned |
| 8. Improve and automate | Planned |
| 9. Develop the portfolio case study | Foundation documentation prepared; full case study planned |

## Final goal

Build and operate a small home security operations environment that identifies assets, collects useful logs, detects suspicious activity, supports repeatable investigations, and documents containment and recovery from controlled simulations.

## Phase 1: Define the environment — initial documentation available

Objective: Understand the assets and their roles before selecting security tools.

Actions:

- Maintain the asset inventory and inventory-based network diagram.
- Verify ambiguous device properties, private addressing, and potential log sources.
- Identify important systems and record identification uncertainties.
- Include virtual machines, containers, or new device classes when they are actually added and verified.
- Keep operational IPs, MACs, and ownership details in private records; publish aliases and functional roles.

Deliverables: Asset inventory, basic topology, important-system list, and unresolved-identification notes.

Completion standard: Important devices have explainable roles and documented evidence supporting their identification. Uncertainties remain explicit. The current inventory and diagram alone do not establish complete validation.

## Phase 2: Establish a security baseline — initial observations available

Objective: Document expected activity before defining abnormal behavior.

Actions:

- Record expected devices, applications, services, connections, DNS activity, and authentication events.
- Record observation dates, duration, active applications, and collection scope.
- Expand the existing TCP snapshots with UDP and CPU, memory, disk, and network observations.
- Use PowerShell, Wireshark, Windows Event Viewer, and relevant router or endpoint information.
- Add container-log observations only when containers are part of the verified environment.

Deliverables: Normal-device and service lists, traffic notes, selected sanitized evidence, and investigation triggers.

Completion standard: Expected activity can be explained from recorded evidence, and deviations requiring investigation can be identified. Short snapshots are not treated as continuous coverage or fixed alert thresholds.

## Phase 3: Harden the home network — planned

Objective: Reduce avoidable risk before expanding monitoring.

Actions: Review administrator and Wi-Fi credentials, WPA2/WPA3 settings, firmware, guest access, WPS, remote administration, UPnP, default accounts, operating-system updates, Defender, host firewalls, unused software, and unnecessary listeners. Evaluate separation of trusted computers, guest devices, IoT, and lab systems where supported. Record actual changes and verification results.

Deliverables: Hardening checklist, sanitized before/after records, rationale for changes, and a private operational risk register with a sanitized summary where appropriate.

Completion standard: Default credentials, unintended exposure, and avoidable insecure settings have been reviewed, addressed, or documented with a reason and follow-up. No completed hardening is claimed until evidence is recorded.

## Phase 4: Build the monitoring platform — planned

Objective: Establish a central place to review security information.

Proposed starting point: One Linux virtual machine for monitoring services. Docker may host supporting services where useful. This is a proposed architecture, not the current network diagram.

```text
Selected endpoints and log sources
               |
     Collectors / network sensors
               |
       Monitoring platform
               |
     Searches, dashboards, alerts
```

Evaluate Wazuh or Splunk and select one main platform. Supporting tools such as Sysmon, Zeek, Suricata, DNS logging, or availability monitoring can be evaluated gradually according to a specific visibility need. Their inclusion here does not mean they are installed or configured.

Deliverables: Monitoring server, one connected Windows endpoint, one connected Linux or Docker system, working searches, sanitized event evidence, and a monitoring data-flow diagram.

Completion standard: A controlled event generated on a monitored system can be found in the central platform with the expected fields and timestamp.

## Phase 5: Develop detection use cases — planned

Objective: Turn collected data into understandable and testable alerts.

Candidate use cases:

1. Repeated failed Windows or SSH logins.
2. An unexpected device or new DHCP lease.
3. Suspicious PowerShell execution patterns.
4. Security tools, firewalls, or logging disabled or changed.
5. Unusual outbound connections considered in application and baseline context.
6. Changes to important configuration files or startup entries.

For each implemented detection, document the data source, logic, trigger, false positives, investigation steps, recommended response, and controlled test result. An unfamiliar country or port alone is not a verdict of malicious activity.

Deliverables: At least five tested detection write-ups.

Completion standard: Each alert can be explained, safely triggered, investigated, and distinguished from expected activity.

## Phase 6: Create the incident-response process — planned

Objective: Use a repeatable process from alert review through closure.

| Step | Work to document |
| --- | --- |
| Preparation | Inventory, tools, protected accounts, backups, evidence collection, and private escalation details |
| Identification | Alert source, affected device, timeline, expected behavior, supporting evidence, and severity |
| Containment | Proportionate actions such as disconnecting a lab device, disabling a test account, or stopping a test container; preserve evidence first |
| Eradication | Remove the simulated cause, correct configuration, patch, or rebuild as appropriate |
| Recovery | Restore services, verify the fix, and watch for recurrence |
| Lessons learned | Findings, effective actions, delays, and improvements |

Deliverables: Response checklist, severity criteria, evidence checklist, incident-report template, and lessons-learned template.

Completion standard: The documented process supports consistent investigation and justified decisions without inventing steps during each event.

## Phase 7: Run controlled incident simulations — planned

Objective: Practice investigation in explicitly included, owned lab systems.

Candidate exercises: Failed test logins; a controlled new device; harmless PowerShell activity resembling a detection pattern; the EICAR antivirus test file; or a test container/configuration change.

Deliverables for each exercise: Trigger and alert evidence, timeline, investigation, containment decision, recovery validation, cause analysis, and lessons learned. Label all scenarios as simulations.

Completion standard: At least three complete investigations demonstrate independent reasoning and a defensible evidence trail. Household activity is not reclassified as a simulated attack.

## Phase 8: Improve and automate — planned

Objective: Automate understood, repeatable manual work.

Candidates: Inventory comparison, new-device notification, log summaries, monitoring-health checks, configuration backup, detection enrichment, and container-status checks. Select PowerShell, Python, shell scripts, scheduled tasks, or platform alerting according to the task.

Deliverables: At least two useful scripts, a monitoring-health check, a tested automated detection or notification, sanitized configuration examples, and usage documentation.

Completion standard: Routine monitoring tasks run reliably and failures are visible. Credentials and notification tokens remain outside public files.

## Phase 9: Develop the portfolio case study — foundation package prepared; full case study planned

Objective: Explain the work, decisions, evidence, and learning to a reviewer.

The current repository covers the foundation stage. Add verified monitoring architecture, deployed technologies, detection write-ups, and two or three detailed investigations as that work is completed. Include actual challenges and explain proposed improvements separately from implemented changes.

Deliverables: Linked evidence, current architecture, investigation reports, lessons learned, and a final project presentation when the later phases are complete.

Completion standard: A reviewer can distinguish implemented work, observations, assumptions, simulations, and planned improvements, and understand the reasoning behind decisions.

## Sequence and final completion standard

Progress from foundation (Phases 1–3), to visibility (4), detection (5), response (6–7), then automation and the full case study (8–9). Update public documentation throughout.

The final project requires validated asset knowledge, documented hardening, central log collection, tested detections, repeatable investigation, demonstrated containment and recovery from simulations, and clear reports. Installing a monitoring tool alone does not meet this standard.
