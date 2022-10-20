# Ice Walkthrough

### Recon Walkthrough
running a basic nmap scan, checking all ports with min rate 10000
will furter run an sS sC sV scan, potentially a vuln script scan

noticed port 3389 is open (microsoft rdc is available)
also noticed that our host is running an icecast server

checking msfconsole for potential exploits
found one for icecast and exploited

while in meterpreter, attempt another connection using the suggested msfconsole search
`run post/multi/recon/local_exploit_suggester`

background our first session and ran the second exploit (requiring the session number to be inputted)

in the second meterpreter console, ran `getprivs` to see which privileges are allowed

notice that in our privileges we can take ownership of processes

migrating to spoolsv.exe