sys# LINUX (resolv.conf)
The three main configuration directives in resolv.conf
nameserver # DNS Server IP
	points to the IP address of a Name Server (only 3 can be listed)
domain # Domain Name of local host
	used for resolving short host-names
search # which domain name to search
	searchlist for hostname lookup (normally determined from local domain name)

### Using GUI

Just go to DNS on ipv4


### Using Resolvconf service
installing resolvconf service
`sudo apt install resolveconf`

bringing up the resolvconf service
`systemctl enable resolvconf.service
`systemctl start resolvconf.service
`systemctl status resolvconf.service`

checking the resolv.conf file **note, can not manually edit this file**

modifying resolvconf with new servers 
**file: /etc/resolvconf/resolv.conf.d/base**
`sudo nano /etc/resolvconf/resolv.conf.d/base`
add: `nameserver [serverIP]`
`sudo nano /etc/network/interfaces`
add: `dns-nameserver [serverIP]`

restart netork manager services
`systemctl restart NetworkManager`
`systemctl restart resolvconf.service`

check for additions to resolv.conf file
`cat /etc/resolv.conf`

## Windows

`[thm@thm]$ systemd-resolve --interface [interface-name] --set-dns [DomainController IP] --set-domain [domain name]`


