Most vendors that ship **sendmail** include not only the binary but also the cf directory from the distribution tree, which they hide somewhere among the operating system files. Table 20.5 will help you find it.

**Table 20.5 — sendmail configuration directory location**

| System | Directory |
|---|---|
| Ubuntu | `/usr/share/sendmail` |
| SUSE | `/usr/share/sendmail` |
| Red Hat | `/usr/share/sendmail-cf` |
| Solaris | `/etc/mail/cf` |
| HP-UX | `/usr/newconfig/etc/mail/cf` |
| AIX | `/usr/samples/tcpip/sendmail/cf` |

# The switch file

Most systems have a “service switch” configuration file, **/etc/nsswitch.conf**, that enumerates the methods that can satisfy various standard queries such as user and host lookups. If more than one resolution method is listed for a given type of query, the service switch file also determines the order in which the various methods are consulted.

The existence of the service switch is normally transparent to software. However, **sendmail** likes to exert fine-grained control over its lookups, so it currently ignores the system switch file and uses its own internal service configuration file (`/etc/mail/service.switch`) instead.

Two fields in the switch file impact the mail system: aliases and hosts. The possible values for the hosts service are dns, nis, nisplus, and files. For aliases, the possible values are files, nis, nisplus, and ldap. Support for the mechanisms you use (except files) must be compiled into **sendmail** before the service can be used.

# Starting sendmail

**sendmail** should not be controlled by **inetd** or **xinetd**, so it must be explicitly started at boot time. See Chapter 3, *Booting and Shutting Down*, for startup details. The flags that **sendmail** is started with determine its behavior. You can run **sendmail** in several modes, selected with the `-b` flag. `-bs` stands for “be” or “become” and is always used with another flag that determines the role **sendmail** will play. Table 20.6 lists the legal values and also includes the `-A` flag, which selects between MTA and MSA behavior.

If you are configuring a server that will accept incoming mail from the Internet, run **sendmail** in daemon mode (`-bd`). In this mode, **sendmail** listens on network port 25 and waits for work. You will usually specify the `-q` flag, too—it sets the

8. The ports that **sendmail** listens on are determined by `DAEMON_OPTIONS`; port 25 is the default.