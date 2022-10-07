ran an nmap scan, attempting to exploit ports 139 and 445 with [[ENUM4LINUX]]

next used impacket's [[KERBRUTE]] to brute force the username list with a set username list found in [this github repository](https://github.com/Sq00ky/attacktive-directory-tools)

found svc-admin and backup

used impacket's GetNPUsers.py to find the hash for svc-admin [[IMPACKET]]

used hashcat to crack the hash (kerberos hash) [[JOHNRIPPER & HASHCAT]]

attempted to see shares with login credentials [[SMBCLIENT]]

found the backup share and logged in with svc-admin credentials

found a text filed and decrypted it using CyberChef

moved on to use another impacket file `secretdump.py` to obtain all the hashes

found the administrator account hash and am using [[EVIL-WINRM]] to pass the hash


