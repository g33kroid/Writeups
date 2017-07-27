# Walkthrough for Machine "FristiLeak 1" on Vulnhub

NMAP Basic Scan 

```shell
root@kali:~# nmap 192.168.1.115

Starting Nmap 7.50 ( https://nmap.org ) at 2017-07-27 13:10 +04
Nmap scan report for 192.168.1.115
Host is up (0.00015s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 08:00:27:A5:A6:76 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 6.00 seconds
```

NMAP Aggressive Scan 

```shell
root@kali:~# nmap -A -O -sV -p80 192.168.1.115

Starting Nmap 7.50 ( https://nmap.org ) at 2017-07-27 13:11 +04
Nmap scan report for 192.168.1.115
Host is up (0.00015s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.2.15 ((CentOS) DAV/2 PHP/5.3.3)
| http-methods: 
|_  Potentially risky methods: TRACE
| http-robots.txt: 3 disallowed entries 
|_/cola /sisi /beer
|_http-server-header: Apache/2.2.15 (CentOS) DAV/2 PHP/5.3.3
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
MAC Address: 08:00:27:A5:A6:76 (Oracle VirtualBox virtual NIC)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 2.6.X|3.X
OS CPE: cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:3
OS details: Linux 2.6.32 - 3.10, Linux 2.6.32 - 3.13
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   0.15 ms 192.168.1.115

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.89 seconds
```
Lets Do Dir Busting 

```shell
```

Nikto Scan 

```shell
```

