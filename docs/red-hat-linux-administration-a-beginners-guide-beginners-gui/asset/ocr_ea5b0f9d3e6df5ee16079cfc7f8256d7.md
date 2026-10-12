# 9.5 Employing a Checklist

If you don’t keep track of the systems you administer, you never know what’s going on with them. Using a simple checklist can help keep you aware of security issues that need to be bolted down on every system, not just the one you practiced on while reading this module! Table 9-1 shows a sample checklist that you can modify to meet your own needs.

| Rule | Security Measure |
|---|---|
| 1. | Use software to enhance safety |
| 1.1 | Set password protection on your boot loader |
| 1.2 | When installing, keep the Red Hat default of using shadow passwords with MD5 encryption |
| 1.3 | Enable PAM |
| 1.4 | Use OpenSSH rather than **rlogin** and **rsh** (see Module 1.5 for more on OpenSSH) |
| 1.5 | Install and configure Tripwire, and monitor its output |
| 1.6 | Use **up2date** or a manual process to ensure that update packages are installed from a secure site |
| 1.7 | Periodically use a vulnerability scanner to keep yourself and your systems honest |
| 2. | Configure the system to enhance safety |
| 2.1 | Do not open file and directory permissions any wider than necessary, especially executable and configuration files |
| 2.2 | Do not use SetUID root permissions |
| 2.3 | Disable reboots using the CTRL-ALT-DEL key combination (in the ` /etc/inittab` file) |
| 2.4 | Use restrictive settings on Apache, DNS, FTP, SMTP, POP/IMAP, printing, and NFS configurations (and only enable these servers as needed) |
| 2.5 | Configure iptables firewalling as appropriate |
| 3. | Restrict or eliminate vulnerable software |
| 3.1 | Do not use **xinetd** services unless necessary |
| 3.2 | Disable the **rlogin** and **rsh** commands; use OpenSSH instead |
| 3.3 | Disable unnecessary processes listening on ports |
| 4. | Use your brain |
| 4.1 | Limit access to the physical server |

**Table 9-1** Sample Security Consciousness Checklist