---
description: Tools and some cheatsheets
---

# Tools

## Information Gathering

### Passive

* Whois
* VirusTotal
* Project Sonar
* [https://censys.io](https://censys.io)
* [https://crt.sh](https://crt.sh)
* Netcraft
* WayBack machine

### Active

* Curl
* Whatweb
* Wappalyzer ext
* wafwoof (WAF)
* Aquatone
* Zonetransfer ([https://hackertarget.com/zone-transfer/](https://hackertarget.com/zone-transfer/))
* Crawling web (ZAP)

## XSS

* ZAP
* [XSS Strike](https://github.com/s0md3v/XSStrike)
* [Brute XSS](https://github.com/rajeshmajumdar/BruteXSS)
* [XSSer](https://github.com/epsylon/xsser)
* [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/README.md)
* [PayloadBox](https://github.com/payloadbox/xss-payload-list)

## Sql Injection

* SqlMap

## Command Injections

* Windows : [DOSfuscation](https://github.com/danielbohannon/Invoke-DOSfuscation).
* LInux : [Bashfuscator](https://github.com/Bashfuscator/Bashfuscator)

## WebShells&#x20;



* Terminal like : [phpbash](https://github.com/Arrexel/phpbash)
* WebShells [SecLists](https://github.com/danielmiessler/SecLists/tree/master/Web-Shells)

## Credentials Theft&#x20;

* In an Active Directory environment, we can use a tool such as [Snaffler](https://github.com/SnaffCon/Snaffler) to crawl network share drives for interesting file extensions such as `.kdbx`, `.vmdk`, `.vdhx`, `.ppk`, etc
* We can search the file system or share drive(s) manually using the following commands from [this cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md#search-for-a-file-with-a-certain-filename).
* [DB Browser for SQLite](https://sqlitebrowser.org/dl/) open sqllite files for inspection.
* tool such as [SharpChrome](https://github.com/GhostPack/SharpDPAPI) to retrieve cookies and saved logins from Google Chrome.
* MailSniper is a penetration testing tool for searching through email in a Microsoft Exchange environment for specific terms (passwords, insider intel, network architecture information, etc.).  [MailSniper](https://github.com/dafthack/MailSniper).
* [LaZagne](https://github.com/AlessandroZ/LaZagne) tool  (Credentials recovery project).
* [SessionGopher](https://github.com/Arvanaghi/SessionGopher) to extract saved PuTTY, WinSCP, FileZilla, SuperPuTTY, and RDP credentials.
* tool [net-creds](https://github.com/DanMcInerney/net-creds) to sniff passwords and hashes from a live interface or a pcap file.
* [Responder](https://github.com/lgandx/Responder) Responder is a LLMNR, NBT-NS and MDNS poisoner, with built-in HTTP/SMB/MSSQL/FTP/LDAP rogue authentication server supporting NTLMv1/NTLMv2/LMv2, Extended Security NTLMSSP and Basic HTTP authentication.
* [Inveigh](https://github.com/Kevin-Robertson/Inveigh), or [InveighZero](https://github.com/Kevin-Robertson/InveighZero) .NET IPv4/IPv6 machine-in-the-middle tool for penetration testers.
*

## Kernel exploits, end of life systems

* This [site](https://msrc.microsoft.com/update-guide/vulnerability) is handy for searching out detailed information about Microsoft security vulnerabilities.
* For an older OS like Windows Server 2008, we can use an enumeration script like [Sherlock](https://github.com/rasta-mouse/Sherlock) to look for missing patches. We can also use something like [Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester).
* [local exploit suggester module](https://www.rapid7.com/blog/post/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/) which will help us quickly find any potential privilege escalation vectors and run them within Metasploit should any module exist.

## Miscellaneous

* Exiftool (for image manipulation)
* [tplmap SSI](https://github.com/epinna/tplmap) (Server Side Include)
* XXE Wonderful [Cheatsheet](https://salmonsec.com/cheatsheet/xxe\_injection).
* [SharpGPOAbuse](https://github.com/FSecureLABS/SharpGPOAbuse) is a .NET application written in C# that can be used to take advantage of a user's edit rights on a Group Policy Object (GPO) in order to compromise the objects that are controlled by that GPO.
