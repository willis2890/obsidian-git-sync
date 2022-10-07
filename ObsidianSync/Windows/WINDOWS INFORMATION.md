# Notes
windows root: 
`C:\

where passwords are stored:
`C:\Windows\System32\config

where Windows OS is stored:
`C:\Windows`
	can be accessed with `%windir%`



should check user files such as `C:\Users\[user]\Documents`

windows file system:
NTFS (New Technology File System) 
	supports files > 4GB
	sets permissions on foldiers/files
	allows compressions
	EFS (Encryption File System)
		`RClick > Properties > Security > See permissions for different groups/users`
ADS (Alternate Data Streams)
	only found on NTFS
	ex: data stream of a text file is its text

FAT16/32 (generally used in USB/MicroSD Partitions)

Access user info through **Local User and Group Management** with `lusrmgr.msc`

Mircosoft User Account Control (UAC)
When an admin logs into a system, the system isn't run with elevated permissions. However, when a higher-level privilege needs to be executed, the admin will receieve a confirmation prompt on if they permit the operation to run. (i get this all the time)
	shown by the SHIELD ICON
`RClick > Properties > Security Tab > see permissions for groups/users`

Microsoft System Configuration: used for advanced troubleshooting and diagnosing startup issues
`msconfig`

Computer Management tool: has system tools, storage, and Services and Application
`compmgmt`

Local Users and Groups
`lusrmgr.msc`

System Information Tool: Hardware Resources, Components, and Software Environment
`msinfo32`

Resource Monitor:
`resmon`

Registry Editor
`regedit`

Windows Defender Firewall
`WF.msc`

Volume Shadow Copy Service (VSS): create shadow copy for restoration points