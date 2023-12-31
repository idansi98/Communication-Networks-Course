# TCP-Server
# TCP Server
## Part 1
In this part, we will run some code snippets, and analyze the received traffic using [Wireshark](https://en.wikipedia.org/wiki/Wireshark).  
Each piece of code is a particular implementation of a client-server in the [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) protocol.  
For each version, you should look at the code and briefly explain. Run the code and capture the traffic in wireshark and explain it.  
  
## Part 2
In this section we will implement a TCP server that will do as follows:  
The client sends the server the name of a file it wants to get. The files sit in a folder called `files` which is in the same folder as the server. The file name can also be a path, and in this case the server searches for the file according to the path inside the files folder.  
The client sends the server messages in the following format: `Get [file] HTTP/1.1`, where `[file]` is the name of the wanted file. The client sends additional lines in the message (as it appears in the standard form), but the server have to ignore them. The end of the message from the client is two new lines, i.e. `\r\n\r\n`.  
If the file exists the server will return:  

    HTTP/1.1 200 OK
    Connection: [conn]
    Content-Length: [length]
Then a blank line and then the contents of the file. Instead of `[conn]`, the value of the connection will appear (`close` or `keep-alive`), and instead of `[length]`, the number of bytes sent will appear.  
If the value of the connection field is `close`, the connection will be closed and the server will handle the next client. On the other hand, if the value is `keep-alive`, the connection with the current client should be left open - and the next request from it should be read as part of the same connection.  
If the client does not send a request to the server within 1 second or an empty request is received, we will close the current connection and handle the next client.  
If the client requested jpg or ico files, the content of the file must be read and sent from the server in binary form.  
If the file does not exist, the server will return:  

    HTTP/1.1 404 Not Found
    Connection: close
In addition, the server will print to the screen the request it received from the client.  

We do not implement a client, but we will use an existing one - our [Chrome](https://www.google.com/chrome/?brand=YTUH&gclid=Cj0KCQjw_r6hBhDdARIsAMIDhV_Azw-IKT2ETT49-_xAcp6Oq1n6ue39mFZsHFbnTwrWPg_GGvsggCUaAiwfEALw_wcB&gclsrc=aw.ds) browser. To send a request to the server, type the following in the Chrome address bar: `http://[Server IP]:[Server port][Path]`. For example: `http://1.2.3.4:80/bugsbunny.jpg`.  
Our server will receive only one argument to main - the port to which it is listening.  
In addition to the code, we sniff its traffic in wireshark and explain it.
