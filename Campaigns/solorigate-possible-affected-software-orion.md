# Get an inventory of SolarWinds Orion software possibly affected by Solorigate

This query was originally published in the threat analytics report, *Solorigate supply chain attack*.

Microsoft detects the [2020 SolarWinds supply chain attack](https://msrc-blog.microsoft.com/2020/12/13/customer-guidance-on-recent-nation-state-cyber-attacks/) implant and its other components as *Solorigate*. A threat actor silently added malicious code to legitimate software updates for Orion, which is IT monitoring software provided by SolarWinds. In this way, malicious dynamic link libraries (DLLs) were distributed to SolarWinds customers.

The following query retrieves an inventory of SolarWinds Orion software use in your organization, organized by product name and ordered by how many devices the software is installed on.

More Solorigate-related queries can be found listed under the [See-also](#see-also) section of this document.

## Query

```kusto
DeviceTvmSoftwareInventoryVulnerabilities
| where SoftwareVendor == 'solarwinds'
| where SoftwareName startswith 'orion'
| summarize dcount(DeviceName) by SoftwareName
| sort by dcount_DeviceName desc
```

## Category

This query can be used to detect the following attack techniques and tactics ([see MITRE ATT&CK framework](https://attack.mitre.org/)) or security configuration states.

| Technique, tactic, or state | Covered? (v=yes) | Notes |
|------------------------|----------|-------|
| Initial access |  |  |
| Execution |  |  |
| Persistence |  |  |
| Privilege escalation |  |  |
| Defense evasion |  |  |
| Credential Access |  |  |
| Discovery |  |  |
| Lateral movement |  |  |
| Collection |  |  |
| Command and control |  |  |
| Exfiltration |  |  |
| Impact | v | Not all instances of SolarWinds Orion may be affected by Solorigate. |
| Vulnerability |  |  |
| Misconfiguration |  |  |
| Malware, component |  |  |

## See also

* [Credentials were added to an Azure AD application after 'Admin Consent' permissions granted [Solorigate]](../Persistence/CredentialsAddAfterAdminConsentedToApp[Solorigate].md)
* [Locate Solorigate-related malicious DLLs loaded in memory](solorigate-locate-dll-loaded-in-memory.md)
* [Locate Solorigate-related malicious DLLs created in the system or locally](solorigate-locate-dll-created-locally.md)
* [Locate SolarWinds processes launching suspicious PowerShell commands](solorigate-launching-base64-powershell.md)
* [Locate SolarWinds processes launching command prompt with the echo command](solorigate-launching-cmd-echo.md)
* [Locate Solorigate attempting DNS lookup of command-and-control infrastructure](solorigate-c2-lookup-from-nonbrowser.md)
* [Locate Solorigate receiving DNS response](solorigate-c2-lookup-response.md)

## Contributor info

**Contributor:** Microsoft Threat Protection team
