# Tricks

– Checks all results in Nmap’s XML output with service version

```
 nmap -p- -sV -oX new.xml 10.10.10.10; searchsploit --nmap new.xml
```

