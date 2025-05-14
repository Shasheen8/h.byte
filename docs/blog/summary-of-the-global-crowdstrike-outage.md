---
title: Summary of the Global Crowdstrike-Microsoft Outage
date: Mon, 22 Jul 2024 07:00:00 +0000
---
OverviewOn July 19, 2024, CrowdStrike and Microsoft experienced a significant global outage that lasted multiple hours and impacted vital services. The disruption, from a configuration error during routine maintenance, affected authentication and data processing systems. The sensor configuration update that caused the system crash was remediated on Friday, July 19, 2024, 05:27 UTC. The impact was felt by customers running Falcon sensor for Windows version 7.11 and above online between Friday, July 19, 2024, 04:09 UTC and Friday, July 19, 2024, 05:27 UTC. Systems running Falcon sensors for Windows 7.11 and above were susceptible to a system crash.DetailsThe outage's root cause was identified as a misconfiguration resulting from a system update error. The configuration files mentioned above are referred to as “Channel Files” and are part of the behavioural protection mechanisms used by the Falcon sensor. Updates to Channel Files are a normal part of the sensor’s operation and occur several times daily in response to novel tactics, techniques, and procedures discovered by CrowdStrike.AnalysisOn Windows systems, Channel Files reside in the following directory:C:\Windows\System32\drivers\CrowdStrike\It has a file name that starts with “C-”. Each channel file is assigned a number as a unique identifier. The impacted Channel File in this event is 291 and will have a filename that starts with “C-00000291-” and ends with a .sys extension. Although Channel Files end with the SYS extension, they are not kernel drivers.Triage & Remediation StepsPer CrowStrike, here are the recommendations for workarounds -Reboot the host to allow it to download the reverted channel file. We strongly recommend putting the host on a wired network (as opposed to WiFi) before rebooting, as the host will acquire internet connectivity considerably faster via ethernet.If the host crashes again, then:Boot Windows into Safe Mode or the Windows Recovery EnvironmentNOTE: Putting the host on a wired network (as opposed to WiFi) and using Safe Mode with Networking can help remediation.Navigate to the %WINDIR%\System32\drivers\CrowdStrike directoryWindows Recovery defaults to X:\windows\system32Navigate to the appropriate partition first (default is C:\), and navigate to the crowd strike directory:C:cd windows\system32\drivers\crowdstrikeNote: On WinRE/WinPE, navigate to the Windows\System32\drivers\CrowdStrike directory of the OS volumeLocate the file matching “C-00000291*.sys” and delete it.Do not delete or change any other files or foldersCold Boot, the hostShut down the host.Start host from the off-state.Note: Bitlocker-encrypted hosts may require a recovery keyAdvanced Search Query for Crowdstrike Affected Hosts

// Get ConfigStateUpdate and SensorHeartbeat events
#event_simpleName=/^(ConfigStateUpdate|SensorHeartbeat)$/ event_platform=Win 
// Narrow search to Channel File 291 and extract version number; accept all SensorHeartbeat events within impact window
| case{
    #event_simpleName=ConfigStateUpdate | regex("\|1,123,(?<CFVersion>.*?)\|", field=ConfigStateData, strict=false) | parseInt(CFVersion, radix=16);
    #event_simpleName=SensorHeartbeat | rename([[@timestamp, LastSeen]]);
}| case{
    #event_simpleName=ConfigStateUpdate | @timestamp>1721362140000 AND @timestamp < 1721366820000 | CSUcounter:=1;
    #event_simpleName=SensorHeartbeat | LastSeen>1721362140000 AND LastSeen<1721366820000 | SHBcounter:=1;
    *;
}
| default(value="0", field=[CSUcounter, SHBcounter])
// Make sure both ConfigState update and SensorHeartbeat have happened
| selfJoinFilter(field=[cid, aid, ComputerName], where=[{ConfigStateUpdate}, {SensorHeartbeat}])
// Aggregate results
| groupBy([cid, aid], function=([{selectFromMax(field="@timestamp", include=[CFVersion])}, {selectFromMax(field="@timestamp", include=[@timestamp]) | rename(field="@timestamp", as="LastSeen")}, max(CSUcounter, as=CSUcounter), max(SHBcounter, as=SHBcounter)]), limit=max)
// Perform check on selfJoinFilter
| CFVersion=* LastSeen=*
// Calculate time between last seen and now
| LastSeenDelta:=now()-LastSeen
// Optional threshold; 3600000 is one hour
| LastSeenDelta>3600000
// Calculate duration between last seen and now
| LastSeenDelta:=formatDuration("LastSeenDelta", precision=2)
// Convert LastSeen time to human-readable format
| LastSeen:=formatTime(format="%F %T", field="LastSeen")
// Enrich aggregation with aid_master details
| aid=~match(file="aid_master_main.csv", column=[aid])
| aid=~match(file="aid_master_details.csv", column=[aid], include=[FalconGroupingTags, SensorGroupingTags])
// Convert FirstSeen time to human-readable format
| FirstSeen:=formatTime(format="%F %T", field="FirstSeen")// Move ProductType to human-readable format and add formatting
| $falcon/helper:enrich(field=ProductType)
| drop([Time])
| default(value="-", field=[MachineDomain, OU, SiteName, FalconGroupingTags, SensorGroupingTags], replaceEmpty=true)
| case{
    CSUcounter=0 AND SHBcounter=0 | Details:="OK: Endpoint did not receive channel file during impacted window. Endpoint was offline.";
    CSUcounter=0 AND SHBcounter=1 | Details:="OK: Endpoint did not receive channel file during impacted window. Endpoint was online.";
    CSUcounter=1 AND SHBcounter=1 | Details:="CHECK: Endpoint received channel file during impacted window. Endpoint was online. Endpoint has not been seen online in past hour.";

Lessons LearnedThis outage underscored the importance of robust contingency planning, rigorous testing of system changes, and transparent customer communication during disruptions. In response, CrowdStrike and Microsoft are enhancing monitoring capabilities and reinforcing change management procedures to reduce the risk of similar incidents.Watch for malicious actors leveraging the ongoing CrowdStrike-related event to phish organizations. Example → https://www.virustotal.com/gui/domain/crowdstrike-bsod.com References:https://www.crowdstrike.com/blog/statement-on-falcon-content-update-for-windows-hosts/ https://support.hp.com/lv-en/document/ish_5000477-5000532-16 https://www.reddit.com/r/crowdstrike/comments/1e6vmkf/bsod_error_in_latest_crowdstrike_update/ https://azure.status.microsoft/en-gb/status