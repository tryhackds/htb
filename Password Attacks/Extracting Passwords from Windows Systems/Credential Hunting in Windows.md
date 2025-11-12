## windows native search for these keywords
```
Passwords
Passphrases
Keys
Username
User account
Creds
Users
Passkeys
configuration
dbcredential
dbpassword
pwd
Login
Credentials
```

## LaZagne

We can also take advantage of third-party tools like LaZagne to quickly discover credentials that web browsers or other installed applications may insecurely store

download standalone and deliver to targetpc
https://github.com/AlessandroZ/LaZagne/releases/

##  i use xfreerdp with share to download it
```
xfreerdp /v:10.129.202.99 /u:Bob /p:HTB_@cademy_stdnt! /drive:Shared,/home/htb-ac-1272997
```

## another thing to search the target is findstr native in windows
```
C:\> findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml
```