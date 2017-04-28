﻿## Netro

![Screenshot 1.0.1](http://eirikb.github.io/Netro/1.0.1/screenshot.png)

Reverse tunneling in Windows. 

Try it out: http://eirikb.github.io/Netro/1.0.1/Netro.exe  
Warning: Executable, use at your own risk!  
Netro works perfectly with mono for Linux / OSX.

I usually fire up `ssh -R` when I need some reverse tunneling, on any platform.
But sometimes I have to tunnel from Windows to Windows, and this is a bit more difficult, as I usually don't have sshd running on Windows servers.  
Netro, a bad play on "Metro" is here to help me and others that must do some quick, dirty and simple tunneling on Windows.


Here is an example:
The right side in the following figure is behind a firewall, the left side is publicly accessible.

1.  Netro A listens for incoming connections, and listens for reverse tunneling.
2.  Netro B connects to A for tunneling.
3.  When a client connects to A the data will be transferred through the link between A and B.
4.  Connection is made on B to desired host:port.
5.  Data can now flow both ways.

Figure:

                        ┊
        u               ┆               O
        │               ┆               │ 
    ┌───┴───┐           ┆           ┌───┴───┐
    │       │           ┆           │       │
    │   A   ├───ᑕO──────┆───────────┤   B   │
    │       │           ┆           │       │
    └───────┘           ┆           └───────┘
                        ┆

 
### Tunneling types
 
 `Netro.exe 5000 localhost:80`  
 Listen on port 5000, send connections/data to localhost on port 80.
 No reverse tunneling involved (Proxy).
 
 
        ┌─────┐
    ᑐ───┤     ├───O
        └─────┘


`Netro.exe 5000 5001`  
Listen on port 5000 for normal connections. Listen on port 5001 for reverse tunneling connection.


           u
           │
        ┌──┴──┐
    ᑐ───┤     │
        └─────┘


`Netro.exe localhost:80 example.com:5001`  
Open reverse tunneling cunnection against example.com on port 5001.
On reverse connections, open connection against localhost on port 80.


       O
       │
    ┌──┴──┐
    │     ├───O
    └─────┘
