
# Cracking Linux Credentials

## tool: unshadow
Once we have root access on a Linux machine, we can gather user password hashes and attempt to crack them using various methods to recover the plaintext passwords. To do this, we can use a tool called unshadow, which is included with John the Ripper (JtR). It works by combining the passwd and shadow files into a single file suitable for cracking.

## unshadow and crack with jtr or hashcat
```
unshadow passwd shadow > unshadowed.hashes

sudo gunzip /usr/share/wordlists/rockyou.txt.gz

hashcat -m 1800 -a 0 unshadowed.hashes /usr/share/wordlists/rockyou.txt -o unshadowed.cracked
```
