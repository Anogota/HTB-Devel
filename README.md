![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/de0f1e26-120f-4489-a162-9aec23416994)

1.What is the name of the service is running on TCP port 21 on the target machine?
First i need to use nmap, here is the switch i used: nmap -sCV <IP> results:

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/5e6337fa-7500-42b1-a02f-9f69688731fb)

That how we see, port 21 is Microsoft ftpd, we also see in this scan that we can login as Anonymous

2.Which basic FTP command can be used to upload a single file onto the server?
We can check this by man ftp.

![obraz](https://github.com/Anogota/HTB-Devel/assets/143951834/242e59e5-15d3-4450-95bf-90b4db1b936b)

3.Are files put into the FTP root available via the webserver?
