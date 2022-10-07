# Commands
`smbclient -N -L [host]`
**no pass login** `-N` and **list** hosts (sharenames) `-L`

list hosts with login (requires password)
`smbclient -L [host] -U ["accountname"]`

login to sharename (required password)
`smbclient \\\\[host]\\[sharename] -U ["accountname"]`


