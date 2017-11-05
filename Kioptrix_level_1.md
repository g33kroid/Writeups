So The Machine IP is this "192.168.0.9"
NMAP Basic Scan 

```shell
┌─[micr0b0t@parrot]─[~/Downloads]
└──╼ $nmap 192.168.0.9

Starting Nmap 7.60 ( https://nmap.org ) at 2017-11-05 16:45 EST
Nmap scan report for 192.168.0.9
Host is up (0.0011s latency).
Not shown: 994 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
111/tcp   open  rpcbind
139/tcp   open  netbios-ssn
443/tcp   open  https
32768/tcp open  filenet-tms

Nmap done: 1 IP address (1 host up) scanned in 1.34 seconds
```
NMAP Aggressive SCAn 

```shell
┌─[micr0b0t@parrot]─[~/Downloads]
└──╼ $sudo nmap -A -O -sV -Pn -p22,80,111,139,443,32768 192.168.0.9

Starting Nmap 7.60 ( https://nmap.org ) at 2017-11-05 16:54 EST
Stats: 0:01:31 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.88% done; ETC: 16:56 (0:00:00 remaining)
Stats: 0:02:21 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.88% done; ETC: 16:57 (0:00:00 remaining)
Stats: 0:03:30 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.88% done; ETC: 16:58 (0:00:00 remaining)
Nmap scan report for 192.168.0.9
Host is up (0.00028s latency).

PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         OpenSSH 2.9p2 (protocol 1.99)
| ssh-hostkey: 
|   1024 b8:74:6c:db:fd:8b:e6:66:e9:2a:2b:df:5e:6f:64:86 (RSA1)
|   1024 8f:8e:5b:81:ed:21:ab:c1:80:e1:57:a3:3c:85:c4:71 (DSA)
|_  1024 ed:4e:a9:4a:06:14:ff:15:14:ce:da:3a:80:db:e2:81 (RSA)
|_sshv1: Server supports SSHv1
80/tcp    open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: Test Page for the Apache Web Server on Red Hat Linux
111/tcp   open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2            111/tcp  rpcbind
|   100000  2            111/udp  rpcbind
|   100024  1          32768/tcp  status
|_  100024  1          32768/udp  status
139/tcp   open  netbios-ssn Samba smbd (workgroup: MYGROUP)
443/tcp   open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: 400 Bad Request
|_ssl-date: 2017-11-06T02:55:13+00:00; +4h59m59s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC4_64_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|_    SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
32768/tcp open  status      1 (RPC #100024)
MAC Address: 08:00:27:4B:76:73 (Oracle VirtualBox virtual NIC)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 2.4.X
OS CPE: cpe:/o:linux:linux_kernel:2.4
OS details: Linux 2.4.9 - 2.4.18 (likely embedded)
Network Distance: 1 hop

Host script results:
|_clock-skew: mean: 4h59m58s, deviation: 0s, median: 4h59m58s
|_nbstat: NetBIOS name: KIOPTRIX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
|_smb2-time: Protocol negotiation failed (SMB2)

TRACEROUTE
HOP RTT     ADDRESS
1   0.28 ms 192.168.0.9

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 267.94 seconds
```
Go buster Scan
```shell
┌─[micr0b0t@parrot]─[~/Desktop]
└──╼ $gobuster -u http://192.168.0.9/ -w SecLists/Discovery/Web_Content/common.txt -s 200,203,301,302,403,500 -e -x .php

Gobuster v1.2                OJ Reeves (@TheColonial)
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://192.168.0.9/
[+] Threads      : 10
[+] Wordlist     : SecLists/Discovery/Web_Content/common.txt
[+] Status codes : 302,403,500,200,203,301
[+] Extensions   : .php
[+] Expanded     : true
=====================================================
http://192.168.0.9/.hta (Status: 403)
http://192.168.0.9/.hta.php (Status: 403)
http://192.168.0.9/.htaccess (Status: 403)
http://192.168.0.9/.htpasswd (Status: 403)
http://192.168.0.9/.htaccess.php (Status: 403)
http://192.168.0.9/.htpasswd.php (Status: 403)
http://192.168.0.9/cgi-bin/ (Status: 403)
http://192.168.0.9/index.html (Status: 200)
http://192.168.0.9/manual (Status: 301)
http://192.168.0.9/mrtg (Status: 301)
http://192.168.0.9/test.php (Status: 200)
http://192.168.0.9/usage (Status: 301)
http://192.168.0.9/~operator (Status: 403)
http://192.168.0.9/~root (Status: 403)
=====================================================
```
Until we Explore what is this lets give it a **Nikto** Scan
```shell
┌─[micr0b0t@parrot]─[~/Downloads]
└──╼ $nikto -host 192.168.0.9
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.0.9
+ Target Hostname:    192.168.0.9
+ Target Port:        80
+ Start Time:         2017-11-05 17:19:08 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
+ Server leaks inodes via ETags, header found with file /, inode: 34821, size: 2890, mtime: Wed Sep  5 23:12:46 2001
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ OpenSSL/0.9.6b appears to be outdated (current is at least 1.0.1j). OpenSSL 1.0.0o and 0.9.8zc are also current.
+ Apache/1.3.20 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ mod_ssl/2.8.4 appears to be outdated (current is at least 2.8.31) (may depend on server version)
+ OSVDB-27487: Apache is vulnerable to XSS via the Expect header
+ Allowed HTTP Methods: GET, HEAD, OPTIONS, TRACE 
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ OSVDB-838: Apache/1.3.20 - Apache 1.x up 1.2.34 are vulnerable to a remote DoS and possible code execution. CAN-2002-0392.
+ OSVDB-4552: Apache/1.3.20 - Apache 1.3 below 1.3.27 are vulnerable to a local buffer overflow which allows attackers to kill any process on the system. CAN-2002-0839.
+ OSVDB-2733: Apache/1.3.20 - Apache 1.3 below 1.3.29 are vulnerable to overflows in mod_rewrite and mod_cgi. CAN-2003-0542.
+ mod_ssl/2.8.4 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2002-0082, OSVDB-756.
+ ///etc/hosts: The server install allows reading of any system file by adding an extra '/' to the URL.
+ OSVDB-682: /usage/: Webalizer may be installed. Versions lower than 2.01-09 vulnerable to Cross Site Scripting (XSS). http://www.cert.org/advisories/CA-2000-02.html.
+ OSVDB-3268: /manual/: Directory indexing found.
+ OSVDB-3092: /manual/: Web server manual found.
+ OSVDB-3268: /icons/: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
+ OSVDB-3092: /test.php: This might be interesting...
+ 8345 requests: 0 error(s) and 21 item(s) reported on remote host
+ End Time:           2017-11-05 17:19:16 (GMT-5) (8 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```
So we have a lead now **mod_cgi** is vulnerable to **shellshock**
```shell
┌─[micr0b0t@parrot]─[~/Downloads]
└──╼ $searchsploit mod_cgi
--------------------------------------------- ----------------------------------
 Exploit Title                               |  Path
                                             | (/usr/share/exploitdb/platforms/)
--------------------------------------------- ----------------------------------
Apache mod_cgi - Remote Exploit (Shellshock) | linux/remote/34900.py
--------------------------------------------- ----------------------------------
```
Lets see what else can we have before testing the exploits
