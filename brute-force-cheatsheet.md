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

Please Refer to \[dada]\([#creating-wordlists](general-tools/hashcat.md#creating-wordlists "mention"))&#x20;

