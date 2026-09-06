# Security Baseline — Command Reference

Run these commands in PowerShell on the Windows PC being observed. Keep your usual applications open and record the date, time, and applications in use.

## 1. Active TCP connections

Shows established TCP connections and their associated process names.

```powershell
Get-NetTCPConnection -State Established |
    Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort,
        @{Name='Application';Expression={
            (Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue).ProcessName
        }} |
    Sort-Object Application |
    Format-Table -AutoSize
```

## 2. Listening TCP ports

Shows services waiting for TCP connections and their associated process names.

```powershell
Get-NetTCPConnection -State Listen |
    Select-Object LocalAddress, LocalPort,
        @{Name='Application';Expression={
            (Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue).ProcessName
        }} |
    Sort-Object LocalPort |
    Format-Table -AutoSize
```

Address meanings:

- `127.0.0.1` and `::1`: loopback, within this PC.
- A specific local IP: listening on that address.
- `0.0.0.0` and `::`: listening across local IPv4 or IPv6 interfaces.
- Listening does not establish internet exposure; firewall and router settings also matter.

## 3. Identify unfamiliar services

This was used to identify the Intel and Razer services observed during the initial baseline.

```powershell
Get-CimInstance Win32_Service |
    Where-Object { $_.PathName -match 'jhi_service|GameManagerService3' } |
    Select-Object Name, DisplayName, State, PathName |
    Format-List
```

For future investigations, replace `jhi_service|GameManagerService3` with the relevant executable name or names. The `|` means either name can match.

## 4. Identify the interface associated with an IP address

```powershell
$InvestigatedAddress = Read-Host "Enter the local IP address to investigate"
Get-NetIPAddress -IPAddress $InvestigatedAddress |
    Select-Object InterfaceAlias, IPAddress |
    Format-Table -AutoSize
```

The address is supplied interactively and is not embedded in this public reference. Keep any collected address mappings in private evidence.

## 5. Identify the adapter behind an interface name

```powershell
Get-NetAdapter -Name "Ethernet 2" |
    Select-Object Name, InterfaceDescription, Status |
    Format-Table -AutoSize
```

`Ethernet 2` is an environment-specific example, not a universal adapter name. Replace it with the interface alias returned by the previous command.

During the initial baseline, this identified the VirtualBox Host-Only Ethernet Adapter.

## 6. DNS observation — Wireshark

This step used Wireshark rather than PowerShell.

1. Capture on the main network adapter.
2. Apply this display filter:

```text
dns
```

3. Use normal applications for about five minutes.
4. Stop the capture.
5. Record example domains and applications in use; save a screenshot.

Cached lookups and encrypted DNS can limit the traffic visible through this filter. DNS packets alone do not identify the requesting process.

## 7. Authentication events — Event Viewer

This step used Event Viewer rather than PowerShell.

Navigate to:

```text
Windows Logs → Security → Filter Current Log
```

Enter these Event IDs:

```text
4624,4625
```

- `4624`: successful logon.
- `4625`: failed logon.

For an event requiring investigation, record its timestamp, target account, logon type, failure reason, status/substatus, caller process, and source network information where available.

## 8. Resource usage — Task Manager

This step used Task Manager rather than PowerShell.

Record:

- Date and time.
- Applications open.
- Background-process count.
- CPU, memory, disk, and network utilization.

Treat readings as an observation, not fixed alert thresholds.

## Saving command output for future baselines

The commands above originally displayed results. To save a future result, append `Out-File` to the end of its pipeline.

For example, change:

```powershell
Format-Table -AutoSize
```

to:

```powershell
Format-Table -AutoSize |
    Out-File -FilePath ".\established-connections.txt" -Width 300 -Encoding utf8
```

For the listening-port command, use `tcp-listeners.txt` instead.

Relative paths save into PowerShell’s current folder. Use a separate dated evidence folder for each baseline; writing to an existing filename replaces its contents.

## Public evidence handling

These commands can display real addresses, account names, application paths, and network activity. Save raw results outside the public repository. Publish only separately reviewed, sanitized excerpts. No raw command output, packet captures, or event-log exports are included in this package.

## Scope

The initial command snapshots covered established TCP connections and TCP listeners. They did not capture UDP endpoints or provide continuous monitoring. The normal-device list came from the asset inventory.
