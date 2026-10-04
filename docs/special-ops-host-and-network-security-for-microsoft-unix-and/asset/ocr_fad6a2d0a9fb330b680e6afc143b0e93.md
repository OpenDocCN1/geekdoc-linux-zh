# Manual Password Guessing via Terminal Server GUI

One should never underestimate the value of some good guesswork. I have cracked many password using only my creativity and patience. Not to mention that an attacker does not need to use complicated exploits and scripts if the server has a blank password on the Administrator account.

# Automated Password Guessing via Windows (TCP 139,445)

A common step for an attacker who has access to TCP 139 or TCP 445 would be to enumerate users and then brute force the passwords for each account using a Windows brute force tool such WinLHF.This example builds on the information gathered in the previous sections.

```
C:\WinLHF.exe 10.0.6.36 -u NewUserAccount -p passwords.txt
WinLHF v1.0 - written by MattW 12-20-02
```

```
Checking 10.0.6.36 for blank or easily guessable passwords.
10.0.6.36 responded to ICMP.. Checking for easy passwords...
Checking if IPC connection can be made.
Checking 10.0.6.36 :: pwd pwd=> specialops
C:\
```

This attacker was able to guess the password for the NewUserAccount. Providing the account has Log Locally, RDP-Tcp and Allow Logon to Terminal Server permissions, the attacker can now use the account to log on to the TS system.The only one of these that is not default for users is the RDP-Tcp setting, however, if the server is in Application Server mode you will probably find that Users have been permitted.

# Automated Password Guessing via TCP 3389

At the time of writing, I am only aware of two techniques that can be used to perform automated password guessing against a Terminal Server via TCP 3389:

+   - TSGrinder (www.hammerofgod.com) The TSGrinder tool was created by Thor from the Hammer of God Co-Op.It had some difficulties out of the starting gate, but hopes are high for this exciting new tool. Although it has been a long time coming, I am assured that not only the tool will be released, but it will be released as version 2;