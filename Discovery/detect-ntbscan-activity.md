# Detect nbtscan activity

This query was originally published in the threat analytics report, *Operation Soft Cell*.

Operation Soft Cell is a series of campaigns targeting users' call logs at telecommunications providers throughout the world. These attacks date from as early as 2012.

Operation Soft Cell operators have been known to run *[nbtscan.exe](https://unixwiz.net/tools/nbtscan.html),* a legitimate MS-DOS command line tool used to discover any NETBIOS nameservers on a local or remote TCP/IP network.

The following query detects nbtscan activity potentially associated with Operation Soft Cell.

## Query

```Kusto
let nbtscan = pack_array("9af0cb61580dba0e380cddfe9ca43a3e128ed2f8",
"90da10004c8f6fafdaa2cf18922670a745564f45");
union ProcessCreationEvents, FileCreationEvents
| where EventTime > ago(7d)
| where FileName =~ "nbtscan.exe" or SHA1 in (nbtscan)
| project FolderPath, FileName, InitiatingProcessAccountName,
InitiatingProcessFileName, ProcessCommandLine, EventTime
```

## Category

This query can be used the following attack techniques and tactics ([see MITRE ATT&CK framework](https://attack.mitre.org/)) or security configuration states.

| Technique, tactic, or state | Covered? (v=yes) | Notes |
|------------------------|----------|-------|
| Initial access |  |  |
| Execution |  |  |
| Persistence |  |  |
| Privilege escalation |  |  |
| Defense evasion |  |  |
| Credential Access |  |  |
| Discovery | v |  The nbtscan tool is also incorporated in legitimate software packages not associated with Operation Soft Cell, to generate network inventories. After running this query, admins should investigate further to determine if the activity is suspicious. |
| Lateral movement |  |  |
| Collection |  |  |
| Command and control |  |  |
| Exfiltration |  |  |
| Impact |  |  |
| Vulnerability |  |  |
| Misconfiguration |  |  |
| Malware, component |  |  |

## Contributor info

**Contributor:** Microsoft Threat Protection team
