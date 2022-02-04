# Useful commands and Modules



[Windows commands reference](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands) is very handy for performing manual enumeration tasks.

modules, cmdlets, resources :&#x20;

* [netstat](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/netstat) Displays active TCP connections, ports on which the computer is listening, Ethernet statistics, the IP routing table.
* [schtasks](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/schtasks) command to enumerate scheduled tasks on the system.
* also enumerate scheduled tasks using the [Get-ScheduledTask](https://docs.microsoft.com/en-us/powershell/module/scheduledtasks/get-scheduledtask?view=windowsserver2019-ps) PowerShell cmdlet.
* Windows binary used for handling certificates [certutil](https://lolbas-project.github.io/lolbas/Binaries/Certutil/).
* [rundll32](https://lolbas-project.github.io/lolbas/Binaries/Rundll32/) Used by Windows to execute dll files.
* enumerate the computer description field via PowerShell using the [Get-WmiObject](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1) cmdlet with the [Win32\_OperatingSystem](https://docs.microsoft.com/en-us/windows/win32/cimwin32prov/win32-operatingsystem) class.
* local users using the [Get-LocalUser](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.localaccounts/get-localuser?view=powershell-5.1) cmdlet.
* Windows [diskshadow](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/diskshadow) utility to create a shadow copy.
* [robocopy](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy) Copies file data from one location to another.
* [takeown](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/takeown) Windows binary to change ownership of the file.
* PowerShell to list named pipes using `gci` (`Get-ChildItem`).&#x20;
* [Accesschk](https://docs.microsoft.com/en-us/sysinternals/downloads/accesschk) AccessChk is a **console utility that reports effective permissions on securable objects, account rights for a user or group, or token details for a process.**
* [PipeList](https://docs.microsoft.com/en-us/sysinternals/downloads/pipelist) from the Sysinternals Suite to enumerate instances of named pipes.
* [Get-AppLockerPolicy](https://docs.microsoft.com/en-us/powershell/module/applocker/get-applockerpolicy?view=windowsserver2019-ps) (Gets the local, the effective, or a domain AppLocker policy).
* [Tasklist ](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist)(Displays a list of currently running processes on the local computer or on a remote computer. **Tasklist** replaces the **tlist** tool).
* [set](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/set\_1) (Displays, sets, or removes cmd.exe environment variables. If used without parameters, **set** displays the current environment variable settings).
* [Hotfixes](https://www.catalog.update.microsoft.com/Search.aspx?q=hotfix) (to get an idea of when the box has been patched).
* If `systeminfo` doesn't display hotfixes, we may use [WMI](https://docs.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page) with [QFE (Quick Fix Engineering)](https://docs.microsoft.com/en-us/windows/win32/cimwin32prov/win32-quickfixengineering) to display patches.
* &#x20;PowerShell as well using the [Get-Hotfix](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-hotfix?view=powershell-7.1) cmdlet.
* [ProcDump](https://docs.microsoft.com/en-us/sysinternals/downloads/procdump) from the [SysInternals](https://docs.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite) suite dump process memory.
* Microsoft reference [guide](https://download.microsoft.com/download/5/8/9/58911986-D4AD-4695-BF63-F734CD4DF8F2/ws-commands.pdf) for all built-in Windows commands.
* &#x20;[dnscmd](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/dnscmd) utility for managing DNS servers.
* query Windows events  using the [wevtutil](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil) utility and the [Get-WinEvent](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.1) PowerShell cmdlet.
* Other logs include [PowerShell Operational](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about\_logging\_windows?view=powershell-7.1) log,  may also contain sensitive information or credentials if script block or module logging is enabled. This log is accessible to unprivileged users.
* [PSSQLite module](https://github.com/RamblingCookieMonster/PSSQLite). to openand inspect sqllite files etc.
* The [cmdkey](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/cmdkey) command can be used to create, list, and delete stored usernames and passwords.

```powershell
ipocnfig /all #Get interface, IP address and DNS information
arp -a #Get arp table
route print #Review routing table
Get-MpComputerStatus #Check Windows Defender status
Get-AppLockerPolicy -Effective \| select -ExpandProperty RuleCollections
#List AppLocker rules
Get-AppLockerPolicy -Local \| Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone
#Test AppLocker policy
set #Display all environment variables
systeminfo #View detailed system configuration information
wmic qfe #Get patches and updates
wmic product get name	# get installed programs
tasklist /svc #Display running processes
query user #Get logged-in users
echo %USERNAME% #Get current user
whoami /priv #View current user privileges
whoami /groups #View current user group information
net user	#Get all system users
net localgroup	#Get all system groups
net localgroup #administrators	View details about a group
net accounts	#Get passsword policy
netstat -ano	#Display active network connections
pipelist.exe /accepteula	#List named pipes
gci \\.\pipe\	#List named pipes with PowerShell
accesschk.exe /accepteula \\.\Pipe\lsass -v	#Review permissions on a named pipe
```

