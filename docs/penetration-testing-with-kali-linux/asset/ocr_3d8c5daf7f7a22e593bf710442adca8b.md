# OffSec

Once the scheduled task is executed again, dave2 should be created and added to the local Administrators group. Waiting a minute, we can check if our privilege escalation attack was successful.

```
PS C:\users\steve> net user

User accounts for \CLIENTWK220
```

```
Administrator        BackupAdmin      dave
dave2               DefaultAccount
Guest               ofsec           steve
MDAGILITYAccount
The command completed successfully.
```

```
PS C:\users\steve> net localgroup administrators
Alias name           administrators
Comment             Administrators have complete and unrestricted access to the
computer/domain
```

```
Members

Administrator
BackupAdmin
dave2
daveadmin
offsec
The command completed successfully.
```

Listing 451 shows that we replaced the executable file by the scheduled task to create an administrator whose credentials we control. Great!

> Listing 451 - Display permissions on the executable file BackendCacheCleanup.exe

In this section, we leveraged a similar privilege escalation attack as we did in the "Service Binary Hijacking.\ This time we focused on scheduled tasks instead of Windows services. We learned how to effectively enumerate scheduled tasks and which properties may be of interest to us. We concluded the section by replacing the executable file and creating the user dave2, which is a member of the local Administrators group.

# 16.3.2 Using Exploits

In the previous section, we attempted to elevate our privileges by searching for sensitive information on a system or abusing Windows components such as Windows services or scheduled tasks. In this section, we will discuss three kinds of exploits leading to privilege escalation and then show one of them in an example.

The first kind is to exploit application-based vulnerabilities. Installed applications on a Windows system may contain different types of vulnerabilities as we learned in the Module "Locating Public Exploits". If these applications run with administrative permissions and we can exploit a vulnerability that leads to code execution, we can also successfully elevate our privileges.