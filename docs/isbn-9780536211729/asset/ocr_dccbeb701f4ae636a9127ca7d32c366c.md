# 2.12 Replace These Weak Doors with Brick

On Red Hat, Mandrake, and other distributions that use the System V style of startup scripts and RPM, it may be shut down and permanently disabled via

```
/etc/rc.d/init.d/nfs stop
/etc/rc.d/init.d/nfslock stop
/etc/rc.d/init.d/portmap stop
chkconfig --del nfs
chkconfig --del nfslock
chkconfig --del portmap
```

While Red Hat's security in the 7.3 release is much improved over that of the 6.x series, it still enables portmap and rpc.stat. Be sure to turn these off.

Alternatively, the Control panel or Linuxconf may be used. On Slackware, edit /etc/rc.d/inet2 to prevent its ever being started again.



One of the two principal security problems with NFS (besides vulnerabilities of security bugs in prior versions) is due to NFS running on top of the UDP protocol. UDP packets can be spoofed easily, allowing a cracker to gain access to portions of your file system you grant to your most trusted NFS clients or even send fake data back to legitimate clients. The other problem is that data is not encrypted thus allowing it to be seen by anyone sniffing the network.

Starting around early 2000 Linux distributions began offering an enhanced NFS that can run on top of TCP as the original UDP protocol. Running NFS on top of TCP solves the UDP spoofing problem. More specifically, TCP support is in NFSv3 that was first included in the 2.2.14 kernel. The tcp mount option can be used on the client when mounting an NFS file system to carry NFS operations to be done over TCP. It may be placed in /etc/fstab too.

Additionally, running NFS on TCP allows you to use TCP Wrappers to limit access to your NFS server and detect and lock out interlopers with Adaptive TCP Wrappers. The portmap program now supports TCP Wrappers.

I have not myself nor encountered references to it, I expect that one could Insert Secure shell (SSH) in top of NFS over TCP, yielding a facility secure from network sniffing and spoofing. Running recent versions of NFS via SSH-wrapped TCP might be a more secure alternative to not using it at all; there is very little experience with so it is still an unknown.

You will pay a substantial performance penalty, on the order of 50 percent, by switching NFS from UDP to TCP. This is typical of any given client/server application over TCP instead of UDP. This performance penalty is due to the doubling of traffic to support the protocol's built-in acknowledgment packets. Another limitation of TCP that UDP does not have is that, connection-oriented, the process on each end of a connection needs a separate socket and handle a separate file descriptor.