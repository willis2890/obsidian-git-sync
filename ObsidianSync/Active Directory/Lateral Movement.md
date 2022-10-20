# Spawning Processes Remotely
### Psexec (Windows CLI Utility)

allows administrator user to run commands reomtely on any PC 
[Psexec LINK](https://learn.microsoft.com/en-us/sysinternals/downloads/psexec)

Ports: 
	445/TCB (SMB)
Required Group Memberships: 
	Administrator

#### Psexec steps
1. Conncets to the Admin$ share and uploads a service binary (psexesvc.exe).
2. Connects to service control manager to create/run PSEXESVC service and associates the service binary with `C:\WINDOWS\psexesvc.exe`
3. Creates named pipes to handle stdin/stdout/stderr communicating through `\.\pipe\psexesvc\`

To use psexec we have to supply admin credentials for the remote host
`psexec64.exe \\[MACHINE_IP] -u Administator -p [password] -i cmd.exe`

### Remote Process Creation  (WinRM)

Ports: 
	5985/TCP (WinRM HTTP) or 
	5986/TCP (WinRM HTTPS)
Required Group Memberships: 
	Remote Management Users

WinRM sends powershell commands to windows hosts remotely

`winrs.exe -u:[USERNAME] -p:[PASSWORD] -r:[target] cmd`

### Remotely Creating Services Using sc


Ports: 
	135/TCP, 49152-65535/TCP (DCE/RPC)
	445/TCP (RPC over SMB Named Pipes)
	139/TCP (RPC over SMB Named Pipes)
Reuired Group Memberships:
	Administrators

Windows services can be leveraged to run arbitrary commands. Service can be created on a remote host with `sc.exe`. 
`sc.exe` will connect to the `Service Control Manager (SVCCTL)` remote service program through RCP in several ways:

