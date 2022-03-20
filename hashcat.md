# Hashcat

* [Website](https://hashcat.net/wiki/).
* Hack the box  [academy](https://academy.hackthebox.com) Hashcat course on using Hashcat rocks!
* Here is  [example hashes](https://hashcat.net/wiki/doku.php?id=example\_hashes) most hash modes that `Hashcat` supports.
* &#x20;[hashid](https://github.com/psypanda/hashID) Software to identify the different types of hashes&#x20;
* [CeWL](https://github.com/digininja/CeWL) to scan potential words from the company's website and save them in a separate list.

### Cracking Miscellaneous Files & Hashes

* The password cracking tool JohnTheRipper help us extract the password hashes from files etc, can be viewed [here](https://github.com/magnumripper/JohnTheRipper/tree/bleeding-jumbo/src).

```python
Staphy$ sudo git clone https://github.com/magnumripper/JohnTheRipper.git
Staphy$ cd JohnTheRipper/src
Staphy$ sudo she./configure && make
```

There are also Python ports of most of these tools available that are very easy to work with. The majority of them are contained in the `JohnTheRipper` jumbo GitHub repo [here](https://github.com/magnumripper/JohnTheRipper/tree/bleeding-jumbo/run).

One additional tool ported to Python is  [keepass2john.py](https://gist.github.com/HarmJ0y/116fa1b559372804877e604d7d367bbc#file-keepass2john-py) tool for extracting a crackable hashes.

* `Hashcat` can be used to attempt to crack password hashes extracted from some Microsoft Office documents using the [office2john.py](https://raw.githubusercontent.com/magnumripper/JohnTheRipper/bleeding-jumbo/run/office2john.py) tool.

```python
Staphy$ python office2john.py file.docx 
```

**Hashcat - Cracking MS Office Passwords**

```shell
Staph$ hashcat -m 9600 file_hash /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt
```

### Cracking Password Protected Zip Files

we may find an interesting zip file password protected! We can extract these hashes using the compiled version of the [zip2john](https://github.com/magnumripper/JohnTheRipper/blob/bleeding-jumbo/src/zip2john.c) tool.



**Extract Hash**

```shell
Staphy$ zip2john file.zip 
```

**Hashcat - Cracking ZIP Files**

```shell
Staphy$ hashcat -a 0 -m 17200 pdf_hash_to_crack /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt
```

### Cracking Password Protected KeePass Files

* We can extract these hashes using the compiled version of the [keepass2john](https://github.com/magnumripper/JohnTheRipper/blob/bleeding-jumbo/src/keepass2john.c) tool or using the Python port done by [HarmJ0y](https://gist.github.com/HarmJ0y), [keepass2john.py](https://gist.githubusercontent.com/HarmJ0y/116fa1b559372804877e604d7d367bbc/raw/c0c6f45ad89310e61ec0363a69913e966fe17633/keepass2john.py).

We can use `keepass2john.py` to extract the hash:

```shell
Staphy$ python keepass2john.py file.kdbx 
```

### Cracking Protected PDF Files

We can extract the hash of the passphrase using [pdf2john.py](https://raw.githubusercontent.com/truongkma/ctf-tools/master/John/run/pdf2john.py). The following command will extract the hash into a format that `Hashcat` can use.

**Extract Hash**

```shell
Staphy$ python pdf2john.py inventory.pdf | awk -F":" '{ print $2}'
```

* Cracking Wireless (WPA and WPA2) Handshakes with Hashcat

### Cracking MIC

To perform this type of offline cracking attack, we need to capture a valid 4-way handshake, by sending de-authentication frames to force a client (user) to disconnect from an AP. When the client reauthenticates (usually automatically), the attacker can attempt to sniff out the WPA 4-way handshake without their knowledge.

Once we have successfully captured a 4-way handshake with a tool such as [airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng), we need to convert it to a format that can be supplied to `Hashcat` for cracking, he format required is `hccapx`and `Hashcat` hosts an online service to convert to this format (not recommended for actual client data but fine for lab/practice exercises): [https://hashcat.net/cap2hccapx](https://hashcat.net/cap2hccapx). To perform the conversion offline, we need the `hashcat-utils` repo from GitHub.

```shell
Staphy$ git clone https://github.com/hashcat/hashcat-utils.git
Staphy$ cd hashcat-utils/src
Staphy$ make
```

**Hashcat-Utils - Installation**

```shell
Staphy$ git clone https://github.com/hashcat/hashcat-utils.git
Staphy$ cd hashcat-utils/src
Staphy$ make
```

**Cap2hccapx - Convert To Crackable File**

```shell
Staphy$ ./cap2hccapx.bin corp_capture1-01.cap mic_to_crack.hccapx
```

**Hashcat - Cracking WPA Handshakes**

```shell
Staphy$ hashcat -a 0 -m 2500 mic_to_crack.hccapx /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt
```

### Cracking PMKID

This attack can be performed against wireless networks that use WPA/WPA2-PSK (pre-shared key) and allows us to obtain the PSK being used by the targeted wireless network by attacking the AP directly. The attack does not require deauthentication (deauth) of any users from the target AP. The PMK is the same as in the MIC (4-way handshake) attack but can generally be obtained faster and without interrupting any users.

```shell
Staphy$ git clone https://github.com/ZerBea/hcxtools.git
Staphy$ cd hcxtools
Staphy$ make && make install
```

**Hcxtools - Installation**

To perform PMKID cracking, we need to obtain the pmkid hash. The first step is extracting it from the capture (.cap) file using the tool `hcxpcaptool` from the `hcxtools` GitHub repo.&#x20;

We may run into compilation errors which can be solved as follows:

**Missing Dependency - openssl/sha.h**

```shell-session
hcxpcapngtool.c:20:10: fatal error: openssl/sha.h: No such file or directory
```

**Installation of Dependencies**

Installation of Dependencies

```shell-session
Staphy@htb[/htb]$ sudo apt install libssl-dev
```

**Missing Dependency - curl/curl.h**

Missing Dependency - curl/curl.h

```shell-session
hcxhashtool.c:19:10: fatal error: curl/curl.h: No such file or directory
```

**Installation of Dependencies**

```shell-session
Staphy@htb[/htb]$ sudo apt install libcurl4-openssl-dev
```

**Extract PMKID**

```shell-session
Staphy$ hcxpcaptool -z pmkidhash_corp cracking_pmkid.cap 
```

There is as Change in Hash mode Hashcat 16800\
So what are the benefits of hash mode 22000?

* The hash mode 22000 hash line combines PMKIDs and EAPOL MESSAGE PAIRs in a single file
* Having all the different handshake types in a single file allows for efficient reuse of PBKDF2 to save GPU cycles
* It is no longer a binary format that allows various standard tools to be used to filter or process the hashes
* It is no longer a binary format which makes it easier to copy / paste anywhere as it is just text
*   The best tools for capturing and filtering WPA handshake output in hash mode 22000 format (see tools below)

    ```
    In order to be able to use the hash mode 22000 to the full extent, you need the following tools:  
    ```
* hcxdumptool v6.0.0 or higher: [https://github.com/ZerBea/hcxdumptool](https://github.com/ZerBea/hcxdumptool)
* hcxpcapngtool from hcxtools v6.0.0 or higher: [https://github.com/ZerBea/hcxtools](https://github.com/ZerBea/hcxtools)
*   hashcat v6.0.0 or higher: [https://github.com/hashcat/hashcat](https://github.com/hashcat/hashcat)

    Optionally there is hcxlabtool, which you can use as an experienced user or in headless operation instead of hcxdumptool: [https://github.com/ZerBea/wifi\_laboratory](https://github.com/ZerBea/wifi\_laboratory)

For users who don't want to struggle with compiling hcxtools from sources there is an online converter: [https://hashcat.net/cap2hashcat/](https://hashcat.net/cap2hashcat/)

If you choose the online converter, you may need to remove some data from your dump file if the file size is too large. Most of the time, this happens when data traffic is also being recorded.

For more information Visit this thread in Hashcat site ([https://hashcat.net/forum/thread-10253.html](https://hashcat.net/forum/thread-10253.html)).

## Optimization

* Optimized Kernels:\
  This is the `-O` flag, which according to the documentation, means `Enable optimized kernels (limits password length)`. The magical password length number is generally 32, with most wordlists won't even hit that number. This can take the estimated time from days to hours, so it is always recommended to run with `-O` first and then rerun after without the `-O` if your GPU is idle.
* Workload:\
  This is the `-w` flag, which, according to the documentation, means `Enable a specific workload profile`. The default number is `2`, but if you want to use your computer while Hashcat is running, set this to `1`. If you plan on the computer only running Hashcat, this can be set to `3`.

## Mask Attack

* Mask attacks are used to generate words matching a specific pattern [Link](https://hashcat.net/wiki/doku.php?id=mask\_attack).

## Hybrid Mode&#x20;

* Hybrid mode is a variation of the combinator attack, wherein multiple modes can be used together for a fine-tuned wordlist creation.

Mode 6 to append mask.

```shell
Staphy$ hashcat -a 6 -m 0 hybrid_hash /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt '?d?s'
```

Mode 7 to prepend mask.\


```python
Staphy$ hashcat -a 7 -m 0 hybrid_hash_prefix -1 01 '20?1?d' /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt
```

## Creating Wordlists

Tools :

* Common User Passwords Profiler ([CUPP](https://github.com/Mebus/cupp)).
* Advanced keyboard-walk [generator](https://github.com/hashcat/kwprocessor#routes) with configureable basechars, keymap and routes.
* Standalone password candidate generator using the PRINCE algorithm [princeprocessor](https://github.com/hashcat/princeprocessor).
* [CeWL](https://github.com/digininja/CeWL) is a Custom Word List Generator.
* Small utilities that are useful in advanced password cracking [Hashcat-utils](https://github.com/hashcat/hashcat-utils).
* [Crunch](https://sourceforge.net/projects/crunch-wordlist/) wordlist generator.

## Rules&#x20;

* The [rule-based](https://hashcat.net/wiki/doku.php?id=rule\_based\_attack#implemented\_compatible\_functions) attack is one of the most complicated of all the attack modes. The reason for this is very simple. The rule-based attack is like a **programming language** designed for password candidate generation. It has functions to modify, cut or extend words and has conditional operators to skip some, etc. That makes it the most flexible, accurate and efficient attack.

### Hashcat debugging Rules

```shell
Staphy$ hashcat -r rule.txt test.txt --stdoutHashcat 
```

### Hashcat - Cracking Passwords Using Wordlists and Rule

```shell
Staphy$ hashcat -a 0 -m 100 hash /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt -r rule.txt
```

### **Hashcat - Default Rules**

```shell
Staphy$ ls -l /usr/share/hashcat/rules/
```

Hashcat provides an option to generate random rules on the fly and apply them to the input wordlist. The following command will generate 1000 random rules and apply them to each word from rockyou.txt by specifying the "-g" flag. There is no certainty to the success rate of this attack as the generated rules are not constant

There are a variety of publicly available rules as well, such as the [nsa-rules](https://github.com/NSAKEY/nsa-rules), [Hob0Rules](https://github.com/praetorian-code/Hob0Rules), and the [corporate.rule](https://github.com/HackLikeAPornstar/StratJumbo/blob/master/chap3/corporate.rule) which is featured in the book [How to Hack Like a Legend](https://www.hacklikeapornstar.com/new-release-hack-like-legend/). These are curated rulesets generally targeted at common corporate Windows password policies or based on statistics and probably industry password patterns.

\


