Attempts to connect client side MS-RPC functions

### Terminal Commands (#)

`rpcclient -U "" -N [host]
attempts login with unlisted user `-U` and no password `-N

`# rpcclient -U "jdoe%[pass]" -c "getusername;quit" [host]`
attempts login with user and pass `-U "[user]%[pass]"` and executes the following commands with `-c`

### RPC Client Commands ($>)

`$> enumdomusers`
enumerate domain users

`$>enumdomgroups`
enumerate domain groups

`$>querygroup [0x204]`
query group information

`$>querygroupmem [0x204]`
query group membership

`$>queryuser [0x308]`
query user information

`$>getdompwinfo`
get domain password info

`$>getuserdompwinfo
get user domain password info

### Password Spraying with RPC Client
after getting the list of domain users using `$>enumdomusers` we can write a [[SHELL SCRIPT]] to password spray (test one password per user ) until success
