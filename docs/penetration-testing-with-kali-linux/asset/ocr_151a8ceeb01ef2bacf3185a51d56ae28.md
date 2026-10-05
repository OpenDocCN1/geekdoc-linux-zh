# # OffSec Penetration Testing with Kali Linux

| SMB | 192.168.50.75 | 445 | CLIENT75 | [*] Windows 10.0 Build 22000 x64 |
| (name:CLIENT75) (domain:corp.com) | | | (signing:False) | [-] mbV:Nexus123! |
| SMB | 192.168.50.75 | 445 | CLIENT75 | [-] corp:dave:Nexus123! |
| STATUS_LOGON_FAILURE | 192.168.50.75 | 445 | CLIENT75 | [+] corp:jen:Nexus123! |
| SMB | 192.168.50.75 | 445 | CLIENT75 | [+] corp:pete:Nexus123! |

List 802 - Using crackmaxec to attack user accounts

List 802 shows that crackmaxec identified the two valid sets of credentials as Spray-Passwords.ps1 did. By preempting the attempted credentials with a plus or minus, crackmaxec indicates whether or not each is valid.

We should note that crackmaxec does not examine the password policy of the domain before starting the password spraying. As a result, we should be cautious about logging out users with this method.

As a bonus, the output of crackmaxec not only displays if credentials are valid, but also if the user has administrative privileges on the target system. For example, dave is a local admin on CLIENT75. Let's use crackmaxec with the password Flowers1 trending marked.

```
kali:$ crackmaxec smb 192.168.50.75 -u dave -p 'Flowers1' -d corp.com
SMB 192.168.50.75 445 CLIENT75 [+] Windows 10.0 Build 22000 x64
(name:CLIENT75) (domain:corp.com) (signing:False) [-] mbV:False
SMB 192.168.50.75 445 CLIENT75 [+] corp:dave:Flowers1
(Pwn3!)$
```

List 803 - Crackmaxec outputting that the valid credentials have administrative privileges on the target

List 803 shows that crackmaxec attacked Pwn3! to the output, indicating that have administrative privileges on the target system. In an assessment, this is an excellent feature to determine the level of access we have without performing additional enumeration.

The third kind of password spraying attack we will discuss is based on obtaining a TGT. For example, using kini¹¹¹⁰⁴ on a Linux system, we can obtain and cache Kerberos TGT. We need to provide a username and password to do this. If the credentials are valid, we will obtain a TGT. The advantage of this technique is that it uses two UDP packets to determine whether the password is valid, as it sends only an AS-REQ and examines the response.

We could use Bash scripting or a programming language of our choice to automate this method. Fortunately, we can use the tool kerbrute¹¹¹⁰⁴ implementing this technique to spray passwords. Since this tool is cross-platform, we can use it on Windows and Linux.

Let's use the Windows version in C\Tools to perform this attack. To conduct password spraying, we need to specify the passwordcommand as an argument with a list of users and the password to spray. We also need to enter the domain corp as an argument -d. For previously, we will create a file named usernames.txt in C\Tools containing the usernames, dave, and jane.

> ¹¹⁰⁴ (Mit Kerberos Documentation, 2022), https://web.mit.edu/kerberos/krb5-1.12/doc/user_commands/kinit.html
¹¹⁰⁵ (Github, 2020), https://github.com/ropnop/kerbrute

PWK - Copyright © 2023 OffSec Securities Limited. All rights reserved.