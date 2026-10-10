USER: On display :0
PASS:

```
Server Challenge: 612b8f9e6dfe71ba27abff77ff99c106 Client 3DES:
4e2568a12e5e7825addbdf4d5190d6
```

Now, use the vncrack tool discussed previously to crack the obtained hash:

```
[bash]$ vncrack -v -c 612b8f9e6dfe71ba27abff77ff99c106 -r
4e2568a12e5e7825addbdf4d5190d6 -w passwords.txt
VncCrank - by Phenoelit (http://www.phenoelit.de/)
$Revision: 1.17 $
```

```
Challenge: 612b8f9e6dfe71ba27abff77ff99c16
Response : 4e2568a12e5e7825addbdf4d519d6

>>>>>>>>>>>>
Password: test123
```

Active traffic between the VNC viewer and the VNC server is unencrypted and can be sniffed by someone on a network segment. However, at this time, no known tools exist that enable deciphering active VNC traffic being transmitted across a network.

# Tunnel VNC Traffic Securely via SSH

Use SSH to tunnel VNC traffic securely. Please see [http://www.uk .research.att.com/vnc/sshvnc.html](http://www.uk .research.att.com/vnc/sshvnc.html) for details.

# VNC Misconfigurations

It is possible to set a null password for VNC authentication. Many users choose to set null passwords, and this allows an intruder to gain complete control of their desktop.

# Software Vulnerabilities

VNC software has been known to suffer a few vulnerabilities. What follows is a list of some of a few recently announced vulnerabilities.

+   TightVNC Server Authentication Cookie Predictability Vulnerability The vncserver program is itself a PERL script that is responsible for generating random X server authentication cookies. A vulnerability was found in TightVNC's vncserver implementation that caused it to generate predictable authentication cookies. This condition caused the possibility for an attacker to predict the necessary