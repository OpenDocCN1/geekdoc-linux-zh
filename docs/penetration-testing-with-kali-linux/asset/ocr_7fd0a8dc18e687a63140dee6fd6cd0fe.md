# OffSec

Penetration Testing with Kali Linux

Although learning every detail of a Linux kernel exploit is outside the scope of this Module, we still need to understand the initial compilation. To do so, copy the code into your Kali home folder and then the first 20 lines of it to any spot compilation instructions.

```
kali@kali:-$ cp /usr/share/exploitdb/exploits/linux/local/45010.c
kali@kali:-$ head 45010.c -n 20
/
Credit @leidl, this is a slight modification to his original POC
https://github.com/brl/grhn/blob/master/get-rekt-linux-hardened.c.
```

For details on how the exploit works, please visit
https://riklarabee.blogspot.com/2018/07/ebpf-and-analysis-of-get-rekt-linux.html

Tested on Ubuntu 16.04 with the following Kernels

+   - 4.4.0-31-generic
- 4.4.0-26-generic
- 4.4.0-31-generic
- 4.4.11-generic
- 4.8.0-58-generic
- 4.10.0.42-generic
- 4.13.0-21-generic

Tested on Fedora 27

```
gcc cve-2017-16995.c -o cve-2017-16995
internet@client:~/cve-2017-16995 ./cve-2017-16995
```

> Listing 512 - Identifying the exploit code instructions.

Luckily, to compile the code into an executable, we need to use gcc and specify the C source code and the output filename. To simplify this process, we could rename the C source filename to match the one expected by the exploit's procedure. Once renamed, we can simply pass the exploit code's instructions to compile the C code.

```
kali@kali:-$ mv 45010.c cve-2017-16995.c
```

> Listing 513 - Renaming the Exploit

To make sure the compilation process goes as smooth as possible, we take advantage of the fact that our target is already shipped with GCC. For this reason we can compile and run the exploit on the target itself. This setup allows us to use the correct version of the libraries required by the target's architecture. This setup lowers the risks related to cross-compilation issues. To begin with, we transfer the exploit source code over the target machine via SCP.

```
kali@kali:-$ scp cve-2017-16995.c joe@192.168.1.236:
```

> Listing 514 - Transferring the source code to the target

Once transferred, we connect to the target machine and invoke GCC to compile the exploit, providing the source code as the first argument and the binary name as the output file to the -o

```
joe@ubuntu-privesc:-$ gcc cve-2017-16995.c -o cve-2017-16995
```

> Listing 515 - Compiling the exploit on the target machine

We can safely assume gcc compiled it correctly since did not output any errors.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

561