Ran an nmap scan using
`nmap -p- -T4 -Pn 10.10.10.63
`sudo nmap -sV -sC -O -p 80,135,445,50000 -oX nmap.xml 10.10.10.63
`xsltproc nmap.xml -o nmap.html
`rm nmap.xml
`xdg-open nmap.html

Notice we are running WINDOWS IIS 10.0 and running the Jetty 9.4.z snapshot

Upon checking the website there is a search bar. Inputting anything gives us an error but we find out we are running a `Microsoft SQL Server 2005 9.00.4053 x86` and `Windows NT 5.0 Build 2195: Service Pack 4`

also find out the source file of is located in `C:\webroot\Sock_Puppets\App_Code\Generic DataAccess.cs` 

We will see if we can use RPC to enumerate users
cannot connect using RPC client

Using searchsploit and we do not find anything other than a potential Jetty exploit
`/usr/share/exploitdb/exploits/java/webapps/50438.txt`

this requires port 8080 to be open, and since it isn't, we we're unable to exploit

Trying to ffuf site, don't get anything interesting
we will check the open 50000 port (that we notice also has http running)
used feroxbuster to find different `/askjeeves/`subdirectories
there is `/security /search /about /projects /computers`

attempted to add a user to the server and login with rpcclient
did not work

found you can add a job and set it to run a windows batch command
inserted a revshell from revshells.com using the base64 reverseshell and it connected!

was able to get the user flag

escalated privileges
[READ THIS](https://0xdf.gitlab.io/2022/04/14/htb-jeeves.html)


