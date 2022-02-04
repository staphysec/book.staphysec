---
description: >-
  here is where i store all the useful  or interesting blogs i read. use CTRL+F
  to navigate
---

# Miscellaneous resources

## Splunk Universal Forwarder

EOP:

* The default configuration of Splunk did not have any authentication on the software [Splunk Universal Forwarder Hijacking](https://airman604.medium.com/splunk-universal-forwarder-hijacking-5899c3e0e6b2) and [SplunkWhisperer2](https://clement.notin.org/blog/2019/02/25/Splunk-Universal-Forwarder-Hijacking-2-SplunkWhisperer2/).

## Erlang&#x20;

EOP:

* more information check out the [Erlang-arce blogpost from Mubix](https://malicious.link/post/2018/erlang-arce/)

## &#x20;Windows Named Pipes

* [WindscribeService Named Pipe Privilege Escalation](https://www.exploit-db.com/exploits/48021)

## **Windows User Privileges**&#x20;

## Token privileges, Windows privileges

* Adjusting Token Privileges in [PowerShell](https://www.leeholmes.com/adjusting-token-privileges-in-powershell/)
* Script to enable certain [privileges](https://www.powershellgallery.com/packages/PoshPrivilege/0.3.0.0/Content/Scripts/Enable-Privilege.ps1).
* [Windows Privilege Abuse: Auditing, Detection, and Defense](https://blog.palantir.com/windows-privilege-abuse-auditing-detection-and-defense-3078a403d74e).
* token impersonation attacks [paper](https://github.com/hatRiot/token-priv/blob/master/abusing\_token\_eop\_1.0.txt).
* This [blog post](https://itm4n.github.io/printspoofer-abusing-impersonate-privileges/) goes in-depth on the `PrintSpoofer` tool.
* GOP Abuse SharpGPOAbuse[ **** blog](https://labs.f-secure.com/tools/sharpgpoabuse).
* Enable all token privileges [blog](https://medium.com/@markmotig/enable-all-token-privileges-a7d21b1a4a77).

## Windows Group Privileges

* [Here](https://ss64.com/nt/syntax-security\_groups.html) is a listing of all built-in Windows groups along with a detailed description of each.
* This [page](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/appendix-b--privileged-accounts-and-groups-in-active-directory) has a detailed listing of privileged accounts and groups in Active Directory.
* [PoC](https://github.com/giuliano108/SeBackupPrivilege) to exploit the `SeBackupPrivilege`**.**
* From DNSAdmins to Domain Admin, When DNSAdmins is More than Just DNS Administration [blog](https://adsecurity.org/?p=4064).
* Abusing DNSAdmins privilege for escalation in Active Directory [blog](http://www.labofapenetrationtester.com/2017/05/abusing-dnsadmins-privilege-for-escalation-in-active-directory.html).
* Poc’ing Beyond Domain Admin DNS [blog](https://cube0x0.github.io/Pocing-Beyond-DA/) active directory.
* Escalating Privileges with DNSAdmins Group [blog](https://medium.com/r3d-buck3t/escalating-privileges-with-dnsadmins-group-active-directory-6f7adbc7005b).
* Abusing SeLoadDriverPrivilege for privilege escalation [blog](https://www.tarlogic.com/blog/abusing-seloaddriverprivilege-for-privilege-escalation/).
* Hyper-V Administrators [blog](https://decoder.cloud/2020/01/20/from-hyper-v-admin-to-system/) from-hyper-v-admin-to-system.
* Small POC in powershell exploiting hardlinks during the VM deletion process [poc](https://github.com/decoder-it/Hyper-V-admin-EOP).
* Proof of concept for abusing SeLoadDriverPrivilege (Privilege Escalation in Windows) [tool](https://github.com/TarlogicSecurity/EoPLoadDriver/).
* standalone [exploit](https://github.com/tandasat/ExploitCapcom) for a vulnerable feature in Capcom.sys.



## Windows Credentials Theft

* Dumping the contents of ntds.dit files using PowerShell [blog](https://www.dsinternals.com/en/dumping-ntds-dit-files-using-powershell/).

## Credentials Theft

* How to Extract Content from VMDK Files: A Step-By-Step GuideHow to Extract Content from VMDK Files: A Step-By-Step Guide [blog](https://www.nakivo.com/blog/extract-content-vmdk-files-step-step-guide/).

## User Acess Control UAC

* This [page](https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-control-works) discusses how UAC works in great depth and includes the logon process etc.
* User Account Control security policy settings [page](https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/user-account-control-security-policy-settings).
* [this](https://egre55.github.io/system-properties-uac-bypass) blog post showshSystemPropertiesAdvanced.exe DLL Hijacking UAC Bypass .

## Kernel exploits, end of life systems Windows

*



## Miscellaneous

* Privilege Escalation with Autoruns [blog](https://book.hacktricks.xyz/windows/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries).
* [this site](https://www.microsoftpressstore.com/articles/article.aspx?p=2762082\&seqNum=2) detail many potential autorun locations on Windows systems.
* ALPC Task Scheduler 0-Day  An-depth writeup is available [here](https://blog.grimm-co.com/2020/05/alpc-task-scheduler-0-day.html).
* CVE-2021-36934 HiveNightmare, aka SeriousSam More information about this flaw can be found [here](https://doublepulsar.com/hivenightmare-aka-serioussam-anybody-can-read-the-registry-in-windows-10-7a871c465fa5) and [this](https://github.com/GossiTheDog/HiveNightmare/raw/master/Release/HiveNightmare.exe) exploit binary can be used to create copies of the three files to our working directory. This [script](https://github.com/GossiTheDog/HiveNightmare/blob/master/Mitigation.ps1) can be used to detect the flaw and also fix the ACL issue. Let's take a look.
* [PoC](https://github.com/cube0x0/CVE-2021-36934) by [@cube0x0](https://twitter.com/cube0x0) C# PoC for CVE-2021-36934/HiveNightmare/SeriousSAM.
* CVE-2021-1675/CVE-2021-34527 PrintNightmare[This](https://github.com/cube0x0/CVE-2021-1675) version by [@cube0x0](https://twitter.com/cube0x0) can be used to execute a malicious DLL remotely or locally using a modified version of Impacket.
* ([CVE-2020-5752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-5752))  [blog post](https://www.matteomalvica.com/blog/2020/05/21/lpe-path-traversal/)  initial discovery of the flaw.
* This [page](https://michaelspice.net/windows/end-of-life-microsoft-windows-and-office/) has detailed listing of the end-of-life dates for Microsoft Windows and other products such as Exchange, SQL Server, and Microsoft Office.
* MS16-032. A detailed explanation of this bug can be found in this [Project Zero blog post](https://googleprojectzero.blogspot.com/2016/03/exploiting-leaked-thread-handle.html)
