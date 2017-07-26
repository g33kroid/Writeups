# This is my Walkthough for Machine "DoNot5top" on Vulnhub

Starting with NMAP Basic Scan 

```shell
root@kali:~# nmap 192.168.1.106

Starting Nmap 7.50 ( https://nmap.org ) at 2017-07-26 17:05 +04
Nmap scan report for D0Not5top (192.168.1.106)
Host is up (0.00039s latency).
Not shown: 995 closed ports
PORT    STATE SERVICE
22/tcp  open  ssh
25/tcp  open  smtp
53/tcp  open  domain
80/tcp  open  http
111/tcp open  rpcbind
MAC Address: 08:00:27:58:A4:C4 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 1.71 seconds
```

Followed by NMAP Aggressive Scan 

```shell
root@kali:~# nmap -A -sV -O -p22,25,53,80,111 -T4 192.168.1.106

Starting Nmap 7.50 ( https://nmap.org ) at 2017-07-26 17:06 +04
Nmap scan report for D0Not5top (192.168.1.106)
Host is up (0.00021s latency).

PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 6.7p1 Debian 5+deb8u3 (protocol 2.0)
| ssh-hostkey: 
|   1024 a7:52:df:39:80:7c:66:16:2f:fd:f7:7b:80:13:09:85 (DSA)
|   2048 bf:d9:5a:22:54:91:cc:36:40:3c:e6:35:4f:8e:0c:78 (RSA)
|   256 16:e6:84:e1:5f:80:bc:27:6a:50:01:55:f0:c0:cc:72 (ECDSA)
|_  256 99:5e:64:00:6d:1d:60:62:73:55:1a:19:9c:59:21:ca (EdDSA)
25/tcp  open  smtp    Exim smtpd
| smtp-commands: D0Not5top Hello kali [192.168.1.193], SIZE 52428800, 8BITMIME, PIPELINING, HELP, 
|_ Commands supported: AUTH HELO EHLO MAIL RCPT DATA NOOP QUIT RSET HELP 
53/tcp  open  domain  PowerDNS 3.4.1
| dns-nsid: 
|   NSID: D0Not5top (44304e6f7435746f70)
|   id.server: D0Not5top
|_  bind.version: PowerDNS Authoritative Server 3.4.1 (jenkins@autotest.powerdns.com built 20170111224403 root@x86-csail-01.debian.org)
80/tcp  open  http    Apache httpd
| http-robots.txt: 22 disallowed entries (15 shown)
| /games /dropbox /contact /blog/wp-login.php 
| /blog/wp-admin /search /support/search.php 
| /extend/plugins/search.php /plugins/search.php /extend/themes/search.php 
|_/themes/search.php /support/rss /archive/ /wp-admin/ /wp-content/
|_http-server-header: Apache
|_http-title: Site doesn't have a title (text/html).
111/tcp open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100024  1          54157/udp  status
|_  100024  1          55828/tcp  status
MAC Address: 08:00:27:58:A4:C4 (Oracle VirtualBox virtual NIC)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.8
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.21 ms D0Not5top (192.168.1.106)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.83 seconds
```

it has a HTTP Port 

Lets Go ahead and do Dirbusting 

```shell
root@kali:~# gobuster -u http://192.168.1.106 -w Desktop/SecList/SecLists/Discovery/Web_Content/big.txt -s '200,204,301,302,307,403,500' -e

Gobuster v1.2                OJ Reeves (@TheColonial)
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://192.168.1.106/
[+] Threads      : 10
[+] Wordlist     : Desktop/SecList/SecLists/Discovery/Web_Content/big.txt
[+] Status codes : 200,204,301,302,307,403,500
[+] Expanded     : true
=====================================================
http://192.168.1.106/.htaccess (Status: 403)
http://192.168.1.106/.htpasswd (Status: 403)
http://192.168.1.106/archive (Status: 301)
http://192.168.1.106/blackhole (Status: 301)
http://192.168.1.106/blog (Status: 301)
http://192.168.1.106/contact (Status: 301)
http://192.168.1.106/control (Status: 301)
http://192.168.1.106/dropbox (Status: 301)
http://192.168.1.106/extend (Status: 301)
http://192.168.1.106/feed (Status: 301)
http://192.168.1.106/games (Status: 301)
http://192.168.1.106/manual (Status: 301)
http://192.168.1.106/mint (Status: 301)
http://192.168.1.106/phpmyadmin (Status: 301)
http://192.168.1.106/plugins (Status: 301)
http://192.168.1.106/robots.txt (Status: 200)
http://192.168.1.106/search (Status: 301)
http://192.168.1.106/server-status (Status: 403)
http://192.168.1.106/support (Status: 301)
http://192.168.1.106/tag (Status: 301)
http://192.168.1.106/themes (Status: 301)
http://192.168.1.106/trackback (Status: 301)
http://192.168.1.106/wp-admin (Status: 301)
http://192.168.1.106/wp-content (Status: 301)
http://192.168.1.106/wp-includes (Status: 301)
=====================================================
```
Lets Explore these Directores 

Checking Robots.txt we have the Following 

```text
User-agent: *
Disallow: /games
Disallow: /dropbox
Disallow: /contact
Disallow: /blog/wp-login.php
Disallow: /blog/wp-admin
Disallow: /search
Disallow: /support/search.php
Disallow: /extend/plugins/search.php
Disallow: /plugins/search.php
Disallow: /extend/themes/search.php
Disallow: /themes/search.php
Disallow: /support/rss
Disallow: /archive/
Disallow: /wp-admin/
Disallow: /wp-content/
Disallow: /wp-includes/
Disallow: /comment-page-
Disallow: /trackback/
Disallow: /xmlrpc.php
Disallow: /blackhole/
Disallow: /mint/
Disallow: /feed/
Allow: /tag/mint/
Allow: /tag/feed/
Allow: /wp-content/images/
Allow: /wp-content/online/

# terminal knows where to go.
User-agent: GameTerminal
Disallow:
```


