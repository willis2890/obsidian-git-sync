crack a password, include file, format, and wordlist (use --show)

`john JohnHash.hash --format=NT --wordlist=/usr/share/wordlists/rockyou.txt --show`


CYBERCHEF: CHECKS HASH PROBABILITY
[cyberchef](https://gchq.github.io/CyberChef/)


hashcat -m18200 hash.txt passwordlist.txt --show
`hashcat -m[mode#] [hash file] [passwordlist file] --show`