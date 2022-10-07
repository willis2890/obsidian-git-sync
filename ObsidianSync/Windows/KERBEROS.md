## Kerberos
the default authentication service for Microsoft Windows domains
(more secure than NTLM)

### Terminology
Ticket Granting Ticket (TGT): authentication ticket used to request service tickets from the TGS for specific resources from the domain

Key Distribution Center (KDC=AS+TGS): Service for issuing TGTs and service tickets from (AS) and (TGS)

Authentication Service (AS): issues TGTs to be used by the TGS in the domain

Ticket Granting Service (TGS): takes TGT and returns a ticket to the machine on the domain

## AS-REQ w/ Pre-Authentication
the Authentication Service request starts when 
1. user requests a `Ticket Granting Ticket (TGT)` from the `Key Distribution Center (KDC)`
2. The KDC will request the following
	1. User encrypts a timestamp NT hash and sends it to the `Authentication Service (AS)`
	2. The KDC attempts to decrypt the timestamp using the NT hash (sent from the user)
	3. If successful, the `Key Distribution Center (KDC)` wiil issue a `Ticket Granting Ticket (TGT)` and a session key for the user
3. User sends encrypted `Ticket Granting Ticket` to the `Ticket Granting Server`
4. The `Key Distribution Center` verifies the TGT and if the user has access to the service it send a `valid session key` for the service to the User
5. User requests the service **from the server** and sends the valid `session key `
6. Server grants access

## Kerberos Ticket 
main forms are:
	.kirbi : Rubeus
	.ccache : Impacket

## Attack Privilege Requirements
[[RUBEUS]]
CRACK MAP EXEC

	Kerbrute Enumeration: No Domain Access Required
	Pass the Ticket: Access as a user to the domain required
	Kerberoasting: Access as any user required
	AS-REP Roasting: Access as any user required
	Golden Ticket: Full domain compromise (domain admin) required
	Silver Ticket: Service hash required
	Skeleton Key: Full domain compromise (domain admin) required




## Ticket Granting Ticket contents
The TGT is requested by the users to the  `Key Distribution Center` and the KDC will validate the TGT and return a service ticket

## Service Ticket Contents
There are two sections: the service provided portion and user-provided portion

User Portion: Timestamp, session key, encryption with the TGT session key
Service Portion: User details, Session Key, Encryption with the NTLM hash


Kerberos: key authentication service within Active Directory
	can use [[KERBRUTE]] to brute force discovery of users, passwords, and even password spraying

After you enumerate user accounts with [[KERBRUTE]], you can continue your attack with [[ASREPRosating]]. This can only occur when users has the account privilege "Does not require Pre-Authentication" set. This esentially means that the account does not have to provide valid identification before requesting a Kerberos Ticket

