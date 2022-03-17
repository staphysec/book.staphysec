# EOP  Windows Tools and Resources

Hacktricks [Checklist](https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation).

Best tool to look for privilege escalation [WinPEASS](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS).

[PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md#windows-version-and-configuration) EOP.

Compiled [binaries](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries)

### Useful Tools :&#x20;

* [Seatbelt](https://github.com/GhostPack/Seatbelt)  is a C# project that performs a number of security oriented host-survey "safety checks" relevant from both offensive and defensive security perspectives.
* [PowerUp](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1) PowerShell script  Windows privilege escalation vectors that rely on misconfigurations. It can also be used to exploit some of the issues found.
* [SharpUp](https://github.com/GhostPack/SharpUp) SharpUp is a C# port of various PowerUp functionality
* [JAWS](https://github.com/411Hall/JAWS) Just Another Windows (Enum) Script.
* [SessionGopher](https://github.com/Arvanaghi/SessionGopher) SessionGopher is a PowerShell tool that uses WMI to extract saved session information for remote access tools such as WinSCP, PuTTY, SuperPuTTY, FileZilla, and Microsoft Remote Desktop.
* [Watson](https://github.com/rasta-mouse/Watson) Enumerate missing KBs and suggest exploits for useful Privilege Escalation vulnerabilities.
* [LaZagne](https://github.com/AlessandroZ/LaZagne)  Tool used for retrieving passwords stored on a local machine from web browsers, chat tools, databases, Git, email, memory dumps, PHP, sysadmin tools, wireless network configurations, internal Windows password storage mechanisms, and more.
* Windows Exploit [Suggester ](https://github.com/bitsadmin/wesng)- Next Generation : WES-NG is a tool based on the output of Windows' `systeminfo` utility which provides the list of vulnerabilities the OS is vulnerable to, including any exploits for these vulnerabilities.
* enumeration script like [Sherlock](https://github.com/rasta-mouse/Sherlock) to look for missing patches
* [SharpGPOAbuse](https://github.com/FSecureLABS/SharpGPOAbuse) is a .NET application written in C# that can be used to take advantage of a user's edit rights on a Group Policy Object (GPO) in order to compromise the objects that are controlled by that GPO.

### Kernel exploits, end of life systems

* This [site](https://msrc.microsoft.com/update-guide/vulnerability) is handy for searching out detailed information about Microsoft security vulnerabilities.
* For an older OS like Windows Server 2008, we can use an enumeration script like [Sherlock](https://github.com/rasta-mouse/Sherlock) to look for missing patches. We can also use something like [Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester).
* [local exploit suggester module](https://www.rapid7.com/blog/post/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/) which will help us quickly find any potential privilege escalation vectors and run them within Metasploit should any module exist.

### Websites :&#x20;

* This [page](https://michaelspice.net/windows/end-of-life-microsoft-windows-and-office/) has a more detailed listing of the end-of-life dates for Microsoft Windows and other products



