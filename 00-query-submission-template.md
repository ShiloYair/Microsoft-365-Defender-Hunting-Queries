# < Insert query name >
 BlueCape Study Case - Throttling of MailItemsAccessed :
If more than 1,000 MailItemsAccessed audit records are generated in less than 24 hours, Exchange Online will
stop generating auditing records for MailItemsAccessed activity. When a mailbox is throttled, MailItemsAccessed
activity will not be logged for 24 hours after the mailbox was throttled. If this occurs, there's a potential that
mailbox could have been compromised during this period. The recording of MailItemsAccessed activity will be resumed following a 24-hour period.
## Query
let starttime = 60d;
let endtime = 1d;
CloudAppEvents
| where Timestamp between (startofday(ago(starttime))..startofday(ago(endtime)))
| where   ActionType == "MailItemsAccessed"
| where isnotempty(RawEventData['ClientAppId'] ) and RawEventData['OperationProperties'][1] has "True" 
| project Timestamp, RawEventData['OrganizationId'],AccountObjectId,UserAgent< Insert query string here >
## Category
This query can be used to detect the following attack techniques and tactics ([see MITRE ATT&CK framework](https://attack.mitre.org/)) or security configuration states.
| Technique, tactic, or state | Covered? (v=yes) | Notes |
|------------------------|----------|-------|
| Initial access |  |  |
| Execution |  |  |
| Persistence | ✔ |  | 
| Privilege escalation |  |  |
| Defense evasion |  |  | 
| Credential Access |  |  | 
| Discovery |  |  | 
| Lateral movement |  |  | 
| Collection |  |  | 
| Command and control |  |  | 
| Exfiltration |  |  | 
| Impact |  |  |
| Vulnerability |  |  |
| Misconfiguration |  |  |
| Malware, component |  |  |

## Contributor info
**Contributor:** Shilo Yair
**GitHub alias:** shilo.yair
**Organization:** Microsoft 365 Defender
**Contact info:** shyair@microsoft.com
