# Brute Force - CheatSheet

[Hacktricks](https://book.hacktricks.xyz/brute-force)

## List supported Services

```
hydra -h | grep "Supported services" | tr ":" "\n" | tr " " "\n" | column -e
```

To find out how to use the `http-post-form` module, we can use the "`-U`" flag to list the parameters it requires and examples of usage:

```
hydra http-post-form -U

<...SNIP...>
Syntax:   <url>:<form parameters>:<condition string>[:<optional>[:<optional>]
First is the page on the server to GET or POST to (URL).
Second is the POST/GET variables ...SNIP... usernames and passwords being replaced in the
 "^USER^" and "^PASS^" placeholders
The third is the string that it checks for an *invalid* login (by default)
 Invalid condition login check can be preceded by "F=", successful condition
 login check must be preceded by "S=".

<...SNIP...>

Examples:
 "/login.php:user=^USER^&pass=^PASS^:incorrect"
```

### Custom Wordlist with hydra

Please refer to Hashcat section for creating wordlists

```bash
sed -ri '/^.{,7}$/d' william.txt            # remove shorter than 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' william.txt # remove no special chars
sed -ri '/[0-9]+/!d' william.txt            # remove no numbers
```

&#x20;for omangling and case permutation quickly and easily, like [rsmangler](https://github.com/digininja/RSMangler) or [The Mentalist](https://github.com/sc0tfree/mentalist.git).

### Custom Username List

One such tool we can use is [Username Anarchy](https://github.com/urbanadventurer/username-anarchy).

## Random CheatSheet

```
hydra -h 	hydra help
hydra -C wordlist.txt SERVER_IP -s PORT http-get / 	Basic Auth Brute Force - Combined Wordlist
hydra -L wordlist.txt -P wordlist.txt -u -f SERVER_IP -s PORT http-get / 	Basic Auth Brute Force - User/Pass Wordlists
hydra -l admin -P wordlist.txt -f SERVER_IP -s PORT http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'" 	Login Form Brute Force - Static User, Pass Wordlist
hydra -L bill.txt -P william.txt -u -f ssh://SERVER_IP:PORT -t 4 	SSH Brute Force - User/Pass Wordlists
hydra -l m.gates -P rockyou-10.txt ftp://127.0.0.1 	FTP Brute Force - Static User, Pass Wordlist
```

