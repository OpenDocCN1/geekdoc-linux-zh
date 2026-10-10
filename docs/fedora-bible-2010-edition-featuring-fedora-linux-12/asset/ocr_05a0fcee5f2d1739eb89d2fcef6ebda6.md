+   - **Intrusion attacks** — To remotely use the resources of a target machine, attackers must first look for an opening to exploit. In the absence of inside information such as passwords or encryption keys, they must scan the target machine to see what services are offered. Perhaps one of the services is weakly secured and the attacker can use some known exploit to fingle his or her way in.

A tool called nmap is generally considered the best way to scan a host for services (note that nmap is a tool that can be used for good and bad). Once the attacker has a list of the available services running on his target, he needs to find a way to trick one of those services into letting him have privileged access to the system. Usually, this is done with a program called an exploit.

While DoS attacks are disruptive, intrusion type attacks are the most damaging. The reasons are varied, but the result is always the same. An uninvited guest is now taking up residence on your machine and is using it in a way you have no control over.

# Protecting against denial-of-service attacks

As explained earlier, a denial-of-service attack attempts to crash your computer or at least degrade its performance to an unusable level. There are a variety of denial-of-service exploits. Most try to overload some system resource, such as your available disk space or your Internet connection. Some common attacks and defenses are discussed in the following sections.

# Mailbombing

Mailbombing is the practice of sending so much e-mail to a particular user or system that the computer’s hard drive becomes full. There are several ways to protect your systems from mailbombing. You can use the Procmail e-mail-filtering tool or configure your sendmail daemon.

> **CROSS-REFERENCE:** See Chapter 18 for a more complete description of sendmail.

# Blocking mail with Procmail

The Procmail e-mail-filtering tool is installed by default with Fedora and is tightly integrated with the sendmail e-mail daemon; thus, it can be used to selectively block or filter out specific types of e-mail. You can learn more about Procmail at the Procmail web site: www.procmail.org.

To enable Procmail for your user account, create a .procmailrc file in your home directory. The file should be mode 0600 (readable by you but nobody else). Type the following, replacing evilmailer with the actual e-mail address that is mailbombing you:

```
# Delete mail from evilmailer
:0
* ^From.\*evilmailer
/dev/null
```