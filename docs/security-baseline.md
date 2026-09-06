# Initial security baseline

Baseline date: September 5, 2026  
Environment: Home LAN  
Observed endpoint: Workstation-01 (Windows)  
Status: Initial observations documented; further validation planned

Network addresses and household identifiers are omitted. The baseline source recorded a subnet mask while the inventory-based diagram did not specify one; mask verification remains pending before publishing any addressing design.

## Normal devices

The [public inventory](../inventory/device-inventory-sanitized.csv) contains the device-level record. It includes Gateway-01 and Router-01 plus these 15 clients:

| Connection | Clients |
| --- | --- |
| Ethernet | Workstation-01 |
| Wi-Fi 2.4 GHz | TV-01, TV-02 |
| Wi-Fi 5 GHz | Phone-01 through Phone-06; Tablet-01 through Tablet-03; Laptop-01, Laptop-02; TV-03 |

These are inventory records rather than proof that every device was active during the baseline. Device trust and log collection have not been independently validated.

## Established TCP connections

An initial snapshot was collected during normal workstation use. Recorded application names included ChatGPT, Codex, Visual Studio Code, Discord, Dropbox, Firefox, Microsoft Edge, and Windows-related processes. The notes were not an exhaustive application or process list.

Most external connections used TCP destination port 443. Two connections attributed to ChatGPT used destination port 5228. The supplied notes do not include supporting evidence establishing the purpose of those connections; that purpose remains unverified here. Dropbox and Firefox also had loopback connections.

## Listening services and identification

Recorded TCP listeners were associated with svchost, System, lsass, wininit, spoolsv, services, Dropbox, Discord, Code, jhi_service, and GameManagerService3.

Some listeners used loopback, while others used specific addresses or all local interfaces. Firewall reachability and internet exposure were not assessed in this baseline.

| Question | Investigation | Recorded finding | Limit |
| --- | --- | --- | --- |
| What is jhi_service? | Inspected Windows service details | Intel(R) Dynamic Application Loader Host Interface Service | Service identity alone does not establish safety |
| What is GameManagerService3? | Inspected Windows service details | Razer Game Manager Service 3 | Replaced an initial tentative Xbox attribution |
| Which interface had the TCP port 139 listener? | Mapped an address to an interface and inspected the adapter | VirtualBox Host-Only Ethernet Adapter | Interface identity was established; firewall reachability was not tested |

The [command reference](baseline-command-reference.md) documents the method. These snapshots covered TCP listeners, not UDP endpoints.

## DNS observation

Queries from Workstation-01 to Router-01 and corresponding responses were observed. The notes included Discord-related domains, Spotify aliases in a response, GitHub Copilot, Microsoft/Azure domains, and a browser DNS-related domain. Exact domain strings and raw traffic are omitted from this public summary.

Background applications included Xbox, NVIDIA software, and Dropbox. Their presence does not establish which process requested each DNS name. This was a limited observation, not a complete traffic record; cached lookups and encrypted DNS may not appear in a DNS display filter.

## Windows authentication review

Multiple successful logon events (4624) and one failed logon event (4625) were observed in the reviewed log. The failed event predated the baseline and occurred in August 2026; its exact timestamp is omitted.

| Field | Recorded value |
| --- | --- |
| Target | Built-in Guest account, disabled |
| Logon type | 3 (network) |
| Caller process | C:\Windows\explorer.exe |
| Status | 0xC000006E |
| Substatus | 0xC0000072 |
| Source network address | Unavailable |

The substatus indicates a disabled-account logon failure. It does not establish the triggering action or whether the event was harmless. The caller path is a recorded field, not proof of process integrity. An Explorer-related account-availability check was considered in the private notes, but the cause was not confirmed. This is a baseline investigation observation, not a confirmed compromise or a completed incident response.

Microsoft's [Event 4625 reference](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4625) explains the event fields and status codes.

## Follow-up work

- Repeat observations with collection time, duration, and active applications recorded.
- Investigate repeated unexplained authentication failures, unfamiliar accounts or caller processes, and unexpected sources.
- Validate listener reachability against host firewall and router settings.
- Expand coverage to UDP endpoints and resource-usage observations; no resource readings are included in this baseline.
- Verify inventory uncertainties, subnet mask, and actual log availability.

Raw command output, captures, and event-log exports are not included. This report summarizes the supplied baseline notes and does not claim that their underlying raw evidence was independently revalidated.
