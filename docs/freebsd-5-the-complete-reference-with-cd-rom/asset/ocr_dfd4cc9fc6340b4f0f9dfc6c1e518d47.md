To do any good, an **SSH server** requires that users run **SSH clients**. FreeBSD's OpenSSH package includes such a client, called *ssh*. Clients for other OSs, although not as common as Telnet clients, are readily available. Check `http://www.free ssh.org` for information on free **SSH clients** for many OSs. Commercial terminal programs for Windows and Mac OS often include **SSH** support.

# Running an SSH Server

One fairly straightforward way to configure FreeBSD to run **SSH** is to use *sysinstall*:

+   1. As root, type `/stand/sysinstall` to launch the configuration utility.
+   2. From the main *sysinstall* menu, select the Configure option.
+   3. From the resulting *FreeBSD Configuration Menu* screen, select Networking.
+   4. From the resulting *Network Services Menu* screen, select the *Sshd* option, if it’s not selected.
+   5. Select *Ok*, *Cancel*, and then *Exit Install* to get out of *sysinstall*.

Behind the scenes, this procedure adds the following line to the `/etc/rc.conf` file:

```
```text
ssh_enable="YES"
```
```

This line controls whether FreeBSD launches *sshd*, the **SSH** server, at boot time. If you prefer not to use *sysinstall*, you can add this line yourself with a text editor. Once this line is added, FreeBSD will launch **SSH** when it next restarts. In the meantime, you can launch the server manually:

```
```bash
# /usr/sbin/sshd
```
```

Unlike Telnet, **SSH** usually runs stand-alone rather than via a super server. This configuration improves performance slightly because *sshd* needs to create cryptographic keys whenever it starts up. Normally, *sshd* uses configuration options from its configuration file, described in the next section. You can override some of these options with command-line arguments, though. You might do this when debugging the **SSH** server. Consult the *sshd man* page for more details on these options.