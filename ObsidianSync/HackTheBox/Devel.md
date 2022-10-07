Ran an nmap scan and discovered port 21 and 80 open

trying to login anonymously on the ftp server
anonymous and anonymous@anonymous.gmail.com works

found pea.txt in main directory
`get pea.txt`
information might be useful later

when observing burp suite im noticing ASP.net which means the server will accept aspx files

looking up microsoft-iis/7.5 on google shows a potential vulnerability
does not further there

yao told me aspx can use remote code execution