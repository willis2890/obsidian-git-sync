# Reconissance
nmap scan revealed ports 135,139, and 445 open

# Discovery
smbclient does not work (shares not listed)

rpcclient works but most information is not allowed due to NT_STATUS_ACCESS_DENIED

trying to use `windows/smb/ms17_010_eternalblue` exploit
	exploit failed due to module only support x64(64-bit targets)

trying to use `admin/smb/ms17_010_command` exploit failed

ran another nmap with `--script vuln` and found `windows/smb/ms08_067_netapi`; ran the metasploit and it worked

`getuid` shows I am in `NT AUTHORITY\SYSTEM`

ran a search for txt files using
`search -f *.txt`

decided to just search for root and user using
`search -f root.txt`
`search -f user.txt`

found both flags 
BOX DONE

