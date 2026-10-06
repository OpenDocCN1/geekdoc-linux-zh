5. Which of the following alias commands will locate all program files on a computer on which the SUID bit is set?

+   A. find / -type SUID
B. find / -perm +4000 -type f
C. find / -perm +SUID -type f
D. find / -type +4000
E. find / -suid

6. The /etc/sudoers on a computer includes the following line. What is its effect?

```
%admin ALL=(ALL) ALL
```

+   A. Members of the admin group may run all programs with root privileges by using sudo.
B. Users in the admin user alias, defined earlier in the file, may run all programs with root privileges by using sudo.
C. The admin user alias is defined to include all users of the system.
D. The admin command alias is defined to include all commands.
E. The user admin may run all programs on the computer as root by using sudo.

7. Which command would you type, as root, to discover all the open network connections on a Linux computer?

+   A. lsof -c a
B. netstat -ap
C. ifconfig eth0
D. nmap -sT localhost
E. top -net

8. A server/computer combination appears in both hosts.allow and hosts.deny. What's the result of this configuration when TCP Wrappers runs?

+   A. TCP Wrappers refuses to run and logs an error in /var/log/messages.
B. The system administrator is paged to decide whether to allow access.
C. hosts.deny takes precedence; the client is denied access to the server.
D. hosts.allow takes precedence; the client is granted access to the server.
E. The client is granted access to the server if no other client is currently accessing it.

9. When is the bind option of xinetd most useful?

+   A. When you want to run two servers on one port
B. When you want to specify computers by name rather than IP address
C. When xinetd is running on a system with two network interfaces
D. When resolving conflicts between different servers
E. When xinetd manages a DNS server program