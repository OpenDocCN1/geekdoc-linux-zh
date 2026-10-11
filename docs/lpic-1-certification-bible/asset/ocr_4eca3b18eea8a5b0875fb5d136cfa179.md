```
server: process in.ftpd
matched: /etc/hosts.allow line 7
access: granted
```

```
[root@redhat /etc]# /usr/sbin/tcpdmatch in.telnetd
jason@norbert.the-nashes.net
client: hostname norbert.the-nashes.net
client: address 216.254.90.133
client: username jason
server: process in.telnetd
matched: /etc/hosts.deny line 9
access: denied
```

![](bbox=[0.13, 0.32, 0.19, 0.38])

> TCP wrappers cannot be used with applications that use the UDP.

# SUID security issues

Applications that are set as SUID root can be used to gain root access to the system. Only applications that require SUID should be set so. If the application does not have to run as root, you can create a separate account for just that application and assign rights only where needed. This way if someone uses the application to gain access to the system, they have only the account’s permissions and cannot do harm to the rest of the system.

It is useful to occasionally check to see which files are SUID on the system. It is an even better idea to set up a *cron job* to do this periodically and have it mail you the results. The following command would accomplish this:

```
/usr/bin/find / -user root -perm -4000 -print | /bin/mail -s
"Files that are SUID root" <mail address>
```

If you know that a file system has no applications that need to be SUID, consider mounting it with the `-o nosuid` option. This way an application cannot be accidentally installed SUID without your knowledge.

![](bbox=[0.13, 0.7, 0.2, 0.77])

Some systems automatically remove the SUID status of a shell script when it is run to reduce the security risk.

# Managing packages

Many administrators and users now download precompiled binary packages for software. Downloading these packages is much more convenient than downloading source code and having to compile it. The problem is that unlike source code, which can be manually verified for backdoors or other security problems, binary files must be taken as is. To minimize this risk, you should get binary packages only from the creator’s Web site and check them for validity.