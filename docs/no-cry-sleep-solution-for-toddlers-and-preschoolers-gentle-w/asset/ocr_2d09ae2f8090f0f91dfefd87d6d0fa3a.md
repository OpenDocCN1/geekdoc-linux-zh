# TABLE 24-1
Mail Transfer Agents

| Agent | Description |
|---|---|
| Sendmail | Sendmail mail transfer agent
www.sendmail.com |
| Postfix | Fast, easy to configure, and secure mail transfer agent compatible with Sendmail and designed to replace it
www.postfix.org |
| Qmail | Fast, flexible, and secure MTA with its own implementation and competitive with Postfix
www.qmail.org |
| Exim | MTA based on smail3
www.exim.org |
| Courier | Courier MTA
www.courier-mta.org |
| Mail Transport Agent Switcher | Red Hat tool to let you switch between using Sendmail and Postfix (Mail Transport Agent Switcher in System Settings menu and window) |

# Mail Servers

Red Hat Linux automatically installs and configures both Sendmail and Postfix for you. On starting your system, you can send and receive messages between local users using Sendmail or Postfix. Red Hat includes a special tool called the Mail Transport Agent Switcher, accessible from the System Settings menu or window, to let you switch between the two. You can also set up your Linux system to run a POP server. POP servers hold users’ mail until they log in to access their messages, instead of having mail sent to their hosts directly. Both Postfix and Sendmail will be discussed in this chapter.

Courier is a fast, small, and secure MTA that maintains some compatibility with Sendmail. The Courier software package also includes POP, IMAP, and webmail servers along with mailing list services. It supports extensive authentication methods including shadow passwords, PAM, and LDAP.

Qmail is also a fast and secure MTA, but it has little compatibility with Sendmail. It has its own configuration and maintenance files. Like Postfix, it has a modular design, using a different program for each mail task. It also focuses on security, speed, and easy configuration.

> NOTE Messages sent within a single standalone system require a loopback interface. Most Linux distributions, including Red Hat, do this automatically for you during the installation process. A loopback interface enables your system to address itself, allowing it to send and receive mail to and from itself. A loopback interface uses the hostname localhost and a special IP address reserved for use by local systems, 127.0.0.1. You can examine your /etc/hosts file to see if your loopback interface has been configured as the local host. You should see 127.0.0.1 localhost listed as the first entry.