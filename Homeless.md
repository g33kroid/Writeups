## Homeless Machine by Vulnhub

so doing NMAP SCAN we have HTTP and SSH

Now lets do the NMAP Aggressive Scan

```shell
sudo nmap -A -O -sV -p 22,80 --script="http*.nse" 192.168.10.25
[sudo] password for shifra: 
Sorry, try again.
[sudo] password for shifra: 

Starting Nmap 7.60 ( https://nmap.org ) at 2018-02-11 00:33 PST
Stats: 0:00:07 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 50.00% done; ETC: 00:33 (0:00:06 remaining)
Nmap scan report for 192.168.10.25
Host is up (-0.046s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
80/tcp open  http    Apache httpd 2.4.25 ((Debian))
| http-brute:   
|_  Path "/" does not require authentication
|_http-chrono: Request times for /; avg: 419.39ms; min: 161.29ms; max: 1444.80ms
| http-comments-displayer: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.10.25
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 3360
|     Comment: 
|         /* Header */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2352
|     Comment: 
|         /* List */
|     
|     Path: http://192.168.10.25/assets/js/main.js
|     Line number: 1
|     Comment: 
|         /*
|         	Transitive by TEMPLATED
|         	templated.co @templatedco
|         	Released for free under the Creative Commons Attribution 3.0 license (templated.co/license)
|         */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 1552
|     Comment: 
|         /* Basic */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 52
|     Comment: 
|         /* Box Model */
|     
|     Path: http://192.168.10.25/assets/js/jquery.min.js
|     Line number: 1
|     Comment: 
|         /*! jQuery v1.11.3 | (c) 2005, 2015 jQuery Foundation, Inc. | jquery.org/license */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 84
|     Comment: 
|         <!-- Three -->
|     
|     Path: http://192.168.10.25/assets/js/skel.min.js
|     Line number: 1
|     Comment: 
|         /* skel.js v3.0.2-dev | (c) skel.io | MIT licensed */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 1797
|     Comment: 
|         /* Box */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 125
|     Comment: 
|         <!-- Four -->
|     
|     Path: http://192.168.10.25/#one
|     Line number: 15
|     Comment: 
|         <!--
|         			Please check carefull.... Good luck!..
|         		-->
|     
|     Path: http://192.168.10.25/assets/js/util.js
|     Line number: 3
|     Comment: 
|         /**
|         	 * Generate an indented list of links from a nav. Meant for use with panel().
|         	 * @return {jQuery} jQuery object.
|         	 */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 219
|     Comment: 
|         /* Grid */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2300
|     Comment: 
|         /* Image */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 49
|     Comment: 
|         <!-- Two -->
|     
|     Path: http://192.168.10.25/assets/js/util.js
|     Line number: 37
|     Comment: 
|         /**
|         	 * Panel-ify an element.
|         	 * @param {object} userConfig User config.
|         	 * @return {jQuery} jQuery object.
|         	 */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2015
|     Comment: 
|         /* Form */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 1832
|     Comment: 
|         /* Button */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 3855
|     Comment: 
|         /* Main */
|     
|     Path: http://192.168.10.25/assets/js/jquery.scrolly.min.js
|     Line number: 1
|     Comment: 
|         /* jquery.scrolly v1.0.0-dev | (c) @ajlkn | MIT licensed */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2529
|     Comment: 
|         /* Section/Article */
|     
|     Path: http://192.168.10.25/assets/js/jquery.scrollex.min.js
|     Line number: 1
|     Comment: 
|         /* jquery.scrollex v0.2.1 | (c) @ajlkn | github.com/ajlkn/jquery.scrollex | MIT licensed */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 5
|     Comment: 
|         /*
|         	Transitive by TEMPLATED
|         	templated.co @templatedco
|         	Released for free under the Creative Commons Attribution 3.0 license (templated.co/license)
|         */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 11
|     Comment: 
|         /* Reset */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 3892
|     Comment: 
|         /* Flexgrid */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 60
|     Comment: 
|         /* Containers */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2279
|     Comment: 
|         /* Icon */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 3869
|     Comment: 
|         /* Footer */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 14
|     Comment: 
|         <!-- Banner -->
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 3697
|     Comment: 
|         /* Banner */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 26
|     Comment: 
|         <!-- One -->
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 3569
|     Comment: 
|         /* Menu */
|     
|     Path: http://192.168.10.25/assets/js/util.js
|     Line number: 299
|     Comment: 
|         /**
|         	 * Apply "placeholder" attribute polyfill to one or more forms.
|         	 * @return {jQuery} jQuery object.
|         	 */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2561
|     Comment: 
|         /* Table */
|     
|     Path: http://192.168.10.25/assets/js/util.js
|     Line number: 521
|     Comment: 
|         /**
|         	 * Moves elements to/from the first positions of their respective parents.
|         	 * @param {jQuery} $elements Elements (or selector) to move.
|         	 * @param {bool} condition If true, moves elements to the top. Otherwise, moves elements back to their original locations.
|         	 */
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 2648
|     Comment: 
|         /* Wrapper */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 137
|     Comment: 
|         <!-- Footer -->
|     
|     Path: http://192.168.10.25/assets/css/main.css
|     Line number: 1585
|     Comment: 
|         /* Type */
|     
|     Path: http://192.168.10.25/#one
|     Line number: 146
|     Comment: 
|_        <!-- Scripts -->
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-date: Sun, 11 Feb 2018 08:33:14 GMT; -3s from local time.
|_http-devframework: Couldn't determine the underlying framework or CMS. Try increasing 'httpspider.maxpagecount' value to spider more pages.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|   /robots.txt: Robots file
|   /images/: Potentially interesting directory w/ listing on 'apache/2.4.25 (debian)'
|_  /manual/: Potentially interesting folder
|_http-errors: Couldn't find any error pages.
|_http-favicon: Unknown favicon MD5: 35C5F7F583E3A0D4947237506D4676B3
|_http-feed: Couldn't find any feeds.
|_http-fetch: Please enter the complete path of the directory to save data in.
| http-grep: 
|   (1) http://192.168.10.25/assets/js/#menu: 
|     (1) ip: 
|_      + 192.168.10.25
| http-headers: 
|   Date: Sun, 11 Feb 2018 08:40:12 GMT
|   Server: Apache/2.4.25 (Debian)
|   Connection: close
|   Content-Type: text/html; charset=UTF-8
|   
|_  (Request type: HEAD)
|_http-malware-host: Host appears to be clean
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-mobileversion-checker: No mobile version detected.
|_http-referer-checker: Couldn't find any cross-domain scripts.
| http-robots.txt: 1 disallowed entry 
|_Use Brain with Google
|_http-security-headers: 
|_http-server-header: Apache/2.4.25 (Debian)
| http-sitemap-generator: 
|   Directory structure:
|     /
|       Other: 1
|     /assets/css/
|       css: 1
|     /assets/js/
|       Other: 1; js: 6
|     /images/
|       jpg: 4
|   Longest directory structure:
|     Depth: 2
|     Dir: /assets/js/
|   Total files found (by extension):
|_    Other: 2; css: 1; jpg: 4; js: 6
|_http-slowloris: false
| http-sql-injection: 
|   Possible sqli for queries:
|     http://192.168.10.25/assets/js/?C=N%3bO%3dD%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=D%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=N%3bO%3dD%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=D%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=N%3bO%3dD%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=D%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/css/?C=D%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/css/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/css/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/css/?C=N%3bO%3dD%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=N%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=D%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/?C=D%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/?C=N%3bO%3dD%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=N%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=D%3bO%3dD%27%20OR%20sqlspider
|     http://192.168.10.25/assets/js/?C=M%3bO%3dA%27%20OR%20sqlspider
|_    http://192.168.10.25/assets/js/?C=S%3bO%3dA%27%20OR%20sqlspider
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-title: Transitive by TEMPLATED
| http-traceroute: 
|_  Possible reverse proxy detected.
| http-useragent-tester: 
|   Status for browser useragent: 200
|   Allowed User Agents: 
|     Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
|     libwww
|     lwp-trivial
|     libcurl-agent/1.0
|     PHP/
|     Python-urllib/2.5
|     GT::WWW
|     Snoopy
|     MFC_Tear_Sample
|     HTTP::Lite
|     PHPCrawl
|     URI::Fetch
|     Zend_Http_Client
|     http client
|     PECL::HTTP
|     Wget/1.13.4 (linux-gnu)
|_    WWW-Mechanize/1.34
| http-vhosts: 
|_127 names had status 200
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
|_http-xssed: No previously reported XSS vuln.
MAC Address: 08:00:27:D2:DB:E3 (Oracle VirtualBox virtual NIC)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.8
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT ADDRESS
1   --  192.168.10.25

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1835.19 seconds
```

Lets use NIKTO Web Vulnerability Scanner 

```shell
nikto -h 192.168.10.25
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.10.25
+ Target Hostname:    192.168.10.25
+ Target Port:        80
+ Start Time:         2018-02-11 01:15:11 (GMT-8)
---------------------------------------------------------------------------
+ Server: Apache/2.4.25 (Debian)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Server leaks inodes via ETags, header found with file /robots.txt, fields: 0x58 0x55faa230ab0d9 
+ "robots.txt" contains 1 entry which should be manually viewed.
+ OSVDB-112004: /: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271).
+ OSVDB-112004: /index.php: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271).
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ DEBUG HTTP verb may show server debugging information. See http://msdn.microsoft.com/en-us/library/e8z01xdh%28VS.80%29.aspx for details.
+ OSVDB-3092: /manual/: Web server manual found.
+ OSVDB-3268: /manual/images/: Directory indexing found.
+ OSVDB-3268: /images/: Directory indexing found.
+ OSVDB-3268: /images/?pattern=/etc/*&sort=name: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7536 requests: 0 error(s) and 14 item(s) reported on remote host
+ End Time:           2018-02-11 01:15:22 (GMT-8) (11 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```
In Robots.txt it says **Remember rockyou** so lets do Directory Scanning using *RockYou.txt*

