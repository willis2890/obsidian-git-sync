# Forest Walkthrough

going to be working with **Microsoft RPC, Kerebos, and Win-RM**

## Microsoft RPC
RPC creates distributed client/server programs and manages most network protocol and communications networks

## Kerberos
An authentication protocol used for verifying host/user identities

we will be attacking Kerberos with **AS-REP Roasting**

## Win-Rm
we will be using Win-RM to get access to a shell

# Process

### DISCOVERY
run nmap scans and notice that TCP/5985 is open, can possibly find credentials for a user and get a shell via WinRM

### DNS: UDP/TCP 53
attempt to resolve htb.local and forest.htb.local with dig
`dig @10.10.10.161 htb.local`
`dig @10.10.10.161 forest.htb.local`
`dig axfr @10.10.10.161 htb.local`

all return 10.10.10.161 and zone transfer doesnt work

### SMB: TCP 445
attempting smbclient to list out shares
[[SMBCLIENT]]

`smbclient -N -L 10.10.10.161`

no shares are listed, we get (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)

### RCP: TCP 445
[[RPCCLIENT]]
attempt to connect with `rpcclient -U "" -N 10.10.10.161`
we are in and we attempt to find information about systems users and groups

`$>enumdomusers, $>enumdomgroups, $>querygroup, $>queryuser`
note that there is only one admin group and it contains only one user




