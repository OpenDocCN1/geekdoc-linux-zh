Of course, SSH’s advantages don’t come without a price. The main drawback of SSH is that the encryption and decryption consume CPU time. This fact slows down SSH connections compared to those of direct connections and can degrade overall system performance. This effect is modest, though, particularly for plain text–mode connections. If you tunnel a protocol that transfers much more data, such as X, you may see a greater performance drop when using SSH. Even in this case, the improved security is generally worth the slight speed cost.

Several SSH servers are available for Linux, but the most popular by far is the OpenSSH server (http://www.openssh.org). This program was one of the first open-source implementations of the SSH protocol, which was developed by the commercial SSH Communications Security (http://www.ssh.com), whose server is now sold under the name SSH Tectia. OpenSSH, SSH Tectia, and other SSH products can interoperate with one another, assuming they’re all configured to support at least one common level of the SSH protocol. OpenSSH 5.1, the latest version as I write, supports SSH levels 1.3, 1.5, and 2.0, with 2.0 being the preferred level because of known vulnerabilities in the earlier versions.

![](bbox=[0.11, 0.36, 0.22, 0.41])

OpenSSH is closely associated with the OpenBSD OS, so its Web site has an OpenBSD bias. If you visit the site, you may want to click the Linux link under the For Other OS’s heading. You can find Linux-compatible source code and binaries from that site, and OpenSSH now ships with most Linux distributions.

OpenSSH may be launched via either a super server (inetd or xinetd) or a SysV startup script. The latter method is preferred, because the server may need to perform CPU-intensive tasks upon starting, so if it’s started from a super server, OpenSSH may be sluggish to respond to connection requests, particularly on systems with weaker CPUs. Most distributions deliver SysV startup scripts with their SSH packages. If you make changes to your SSH configuration, you may need to pass the reload or restart option to the startup script, as in /etc/init.d/sshd reload. (Chapter 5 covers SysV startup scripts in more detail.) However it’s launched, the OpenSSH server binary name is sshd—the same as the binary name for SSH Tectia.

# # Setting SSH Options for Your System

For the most part, SSH works reasonably well when it’s first installed, so you may not need to make any changes to its configuration. If you do need to make changes, though, these are mostly handled through the main SSH configuration file, /etc/ssh/sshd_config. You can also edit some additional files to limit access to the SSH server or to change how SSH manages the login process.

# ## Configuring Basic SSH Features

The /etc/ssh/sshd_config file consists mainly of option lines that take the following form:

```
Option value
```