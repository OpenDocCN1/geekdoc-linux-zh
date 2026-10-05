# OffSec

Penetration Testing with Kali Linux

We could use this technique to create a PowerShell script that enumerates all users and performs authentications according to the Lockout threshold and Lockout window observation.

This password spraying tactic is already implemented in the PowerShell script C:\Tools\Spray-Passwords.ps1$^{1102}$ on CLIENT75.

The Pass option allows us to set a single password, or we can spray a wordlist file using -File. We can also test accounts by adding the -Admin flag. The PowerShell script automatically identifies domain users and sprays a password against them

```
PS C:\Users\jeff cd C:\Tools

 C:\Tools> powershell -ep bypass
```

```
PS C:\Tools> \Spray-Passwords.ps1 -Pass Nexus123! -Admin
WARNING: also targeting admin accounts.
Forcing brute - press [q] to stop the process and print results...
Guessed for user: 'pete' = 'Nexus123!'
Guessed for user: 'jen' = 'Nexus123!'
```

> 'pete' with password: 'Nexus123!'
'jen' with password: 'Nexus123!'

Listing 801 - Using Password-spraying to attack user accounts

Nice! The password spraying was successful, providing us two valid sets of credentials with the password Nexus123!

The second kind of password attack against AD uses SMB. This is one of the traditional approaches of password attacks in AD and comes with some drawbacks. For every authentication attempt, a full SMB connection must be set up and terminated. As a result, this kind of password attack is very noisy due to the generated network traffic. It is also slow in comparison to other techniques.

We can use crackmapex$^{1103}$ on Kali to perform this kind of password spraying. We'll select smb as protocol and use the IP address of any domain joined system as CLIENT75 (192.168.50.75). Then, we can provide a list of single users and passwords to -u and -p . In addition, we will enter the domain name for -d and provide the option -continue-on-success to avoid stopping at the first valid credit. For this example, we will create a text file named users.txt containing a subset of the domain usernames dave, jen, and pete to spray the password against Nexus123!

1102 (Improsec, 2016), http://web.archive.org/web/20220225190046/https://github.com/Zilent-Jack/Spray-Passwords/blob/master/Spray-Passwords.ps1
1103 (Github, 2022), https://github.com/Porchetta-Industries/CrackMapEx

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

759