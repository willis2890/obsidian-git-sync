# Common Switches
`-p-`
scan all ports
`-sC
scan with default NSE scripts (safe)
`-T4`
scan hella fast
`-sV
determine versions of services
`-sT`
TCP connect port scan
`-O`
os detection

`-sU`
UDP scan

`-sS`
SYN scan

`-oN, -oX, -append-output
output to normal format, xml format, append to file

`--min-rate 10000
send packets no slower than 10000 per second

# Good Practice
scan all ports with min rate
`nmap -p- --min-rate 10000 [host]

complete a further scan of said ports with `sC` and `sV`

`nmap -sC -sV -p [list ports] -oX [filename.xml] [hosts]`

convert xml script to html
`xsltproc [filename.xml] -o [filename.html]`

