which is a port of the Debian alternatives feature, gives the administrator the tools to transparently exchange one service or application for another on a Red Hat Linux system.

As an administrator of a Red Hat Linux system, you may decide that you want to use a different software package to handle mail service or print service, for example. Using the alternatives system, you can add that new service in such a way that the users of the system don't have to change the commands they use to print a document or send an e-mail.

The alternatives system was added to the `chkconfig` software package for Red Hat Linux 7.3. Its main components are the `alternatives` command and the `/etc/alternatives` directory (which contains a set of links that link user commands to the new services).

> **CROSS-REFERENCE:** The alternatives system is described in Chapter 10.

# ### Installation

A new checkcheck feature has been added to the Red Hat Linux installation process. This feature checks that the Red Hat Linux distribution CDs are not damaged or corrupted. If you run the `mediacheck` and a CD fails, you know that you have a bad distribution CD.

> **CROSS-REFERENCE:** Red Hat Linux installation is described in Chapter 2.

# ### Postfix mail-transfer agent

The postfix software package is designed to be an alternative to the `sendmail` mail transport agent (MTA). It is compatible to `sendmail` in many ways, allowing people to use aliases, forwarding, and other features in the same way. However, it is designed to provide much faster performance and easier administration by not relying on the complex `sendmail.cf` file.

Using the new alternatives, you can replace `sendmail` with postfix in a way that is mostly invisible to the end users. See Chapter 19 for a description of postfix.

# ### CUPS print server

The Common Unix Printing System (CUPS) is a portable software system for managing printing services in Linux and UNIX systems. CUPS can replace the `LPing` printing system while still allowing people to use most of the same commands they used with `LPing` to print documents on local and remote printers.

Using the new alternatives, you can replace `LPing` with CUPS in a way that is mostly invisible to the end users.

> **CROSS-REFERENCE:** See Chapter 17 for a description of CUPS.