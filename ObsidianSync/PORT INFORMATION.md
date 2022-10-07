135/TCP MSRPC
RPC Endpoint Mapper Service: allows other systems to discover what services are advertised on a machine and what port to find them on

139/TCP NetBIOS-SSN
NetBIOS Session Service connects two computer for transmitting heavy data traffic (mostly used for printer and file services)


53 UDP/TCP: 
Can attempt dig to resolve hostnames

445 TCP: 
Can attempt smbclient to attempt to list shares (will be listed as microsoft-ds)

can use RPC to attempt to enumerate users
[RPC Enumeration](https://www.blackhillsinfosec.com/password-spraying-other-fun-with-rpcclient/)
[[RPCCLIENT]]

Enumerate 139 and 445:
use [[ENUM4LINUX]]


3389 TCP: MS-WBT-SERVER
usually vulnerable (microsofts remote desktop protocol)


5985/TCP: 
Potential source to find credentials using a shell over WinRM

8500/FMTP
can netcat into
