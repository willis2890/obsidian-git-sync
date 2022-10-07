davtest is used to test which files you can send to a server
`davtest -url http://[domain]`

Curl is used to transfer a URL

however, you can also use it to transfer files

`curl -X [METHOD] http://[domain]/[filename] -d @[filename]`
upload a file, using `-X PUT` which changes the method string in the http request,
`-d` specifies the contents of the file i want to be uploaded

instead of `-d`, we can specify the way content is sent. 
`--data-binary` will ensure the data is sent in binary
`curl -X MOVE -H 'Destination: http://[domain]/[filename]' [domain]/[filename]`
once again, `-X MOVE` changes the get method to MOVE and this can be used to rename/move a file on a server

