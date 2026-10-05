
## CHAPTER 10 NETWORKING AND THE INTERNET

- IPv6 reserves 24 bits in the header for advanced services, as resource reservation protocols, better backbone routing, and improved traffic engineering.
- IPv6 makes multicast protocols mandatory and uses them extensively. In IPv4, multicast, which improves scalability, is optional.
- IPv6 aggregates blocks more efficiently because of the huge address space. This aggregation makes obsolete *NAT* (page 1161), which decreased scalability and introduced protocol issues.
- IPv6 provides a simplified packet header that allows hardware accelerators to work better.

A sample IPv6 address is fe80::a00:20ff:fe5bbe/10. Each group of hexadecimal digits is equivalent to a number between 0 and 65,536 ($16^4$). A pair of adjacent colons indicates a hex value of 0x0000; leading zeros need not be shown. With eight sets of hexadecimal digits, $65,536 = 2^{16}$ addresses are possible. In an IPv6 address on a host with the default autoconfiguration, the first characters in the address are always fe80. The last 64 bits hold an interface ID designation, which is often the *MAC address* (page 1158) of the system's Ethernet controller.

## COMMUNICATE OVER A NETWORK

Many commands that you can use to communicate with other users on a single computer system have been extended to work over a network. Examples of extended utilities include electronic mail programs, *finger* (page 181), and communications utilities (such as talk). These utilities are examples of the UNIX philosophy: Instead of creating a new, special-purpose tool, modify an existing one.

Many utilities use a convention for the format of network addresses: *user@host* (spoken as “user at host”). When you use an @-sign in an argument to one of these utilities, the utility interprets the text as follows: as the name of a host. When you omit the @ sign, the utility assumes that you are requesting information or responding with the local system.

The prompts show in the examples in this chapter include the hostname of the system you are using. If you frequently use more than one system over a network, you may find it difficult to keep track of which system you are interacting with at any particular moment. If you set your prompt to include the hostname of the current system, it will always be clear which system you are using. To identify the computer

```
$ hostname
kudos
```

See page 321 for information on how you can change the prompt.

## finger: DISPLAYS INFORMATION About REMOTE USERS

The finger utility displays information about one or more users on a system. The utility was designed for local use, but when networks became popular, it was obvious that finger should be enhanced to reach out and collect information remotely. In the following examples, finger displays information about all users logged in on the system named bravo:

```
[kudos]$ finger @bravo
[bravo.example.com]
| Login Name | Tty | Idle | Login Time | Office | Phone |
| :--- | :--- | :--- | :--- | :--- | :--- |
| sam | The Great | | 1 | 1:35 | Oct 22 12:23 | (kudos) |
| max | Max Wild | | 4 | Oct 22 12:23 | (::) |
| max | Max Wild | | 5 | 19 Oct 22 12:23 | (::) |
| zach | Branch | | 7 | 2:24 | Oct 22 8:45 | (::) |
| h1s | Helen Simpson | | 11 | Oct 20 12:00 | (::) |
```

A user's name in front of the @ causes finger to display information from the remote system by the specified user. If the remote system has matches for that name, finger displays the results for all of them:

```
[kudos]$ finger @bravo
[bravo.example.com]
| Login Name | Tty | Idle | Login Time | Office | Phone |
| :--- | :--- | :--- | :--- | :--- | :--- |
| max | Max Wild | | 4 | 19 Oct 22 12:23 | (kudos) |
| max | Max Wild | | 5 | Oct 22 12:23 | (::) |
```

The finger utility works by querying a standard network service, the finger daemon, runs on the system being queried. Although this service is available in the finger package for Ubuntu Linux, some sites choose not to run it to maintain load on their systems, reduce security risks, or maintain privacy. When you use finger to obtain information about someone at a site, you will see an error message or nothing at all. As a result, the report displayed for any given system may differ from the preceding examples.

## in.finger daemon

The in.finger daemon gives away account information that can aid a malicious user. Some sites disable finger or randomize user IDs to make a malicious user's job more difficult. Do not install the package if you do not want to run finger. Information for remote finger looks as much as it does when finger runs on the local system, with one difference: Before displaying the results, finger reports the name of the remote system that answered your query (as shown in brackets in the preceding example). The name of the host that answers your query may be different from the system name specified on the command line, depending on how finger is configured on the remote system. In some cases, several hostnames may be listed if finger daemon contacts another to retrieve the information.

## SENDING MAIL TO A REMOTE USER

Given a user's username on a remote system and the name of the remote system or its domain, you can use email program to send a message over the network using the @ form of an address:

zach@bravo
or
zach@example.com

Many Linux utilities recognize the @ form of a network address; you may find that you can reach more remote computers with email than with other utilities described in this chapter. This disparity arises because email can deliver a message to a host that does not run IP, even though it appears to have an address. The message may be routed over the network, for example, until it reaches a remote system that has point-to-point connection to the destination system. Other utilities, such as talk, rely on IP and operate only between networked hosts.

## MAILING List Servers

A mailing list server allows you to create and manage an electronic mailing list provides a means for people interested in a particular topic to participate in electronic discussion and for a person to disseminate information periodically to a potentially large mailing list. One of the most powerful features of list servers is their ability to archive postings to the list, create an archive index, and allow users to retrieve postings from the archive based on keywords or discussion threads. Typically you can subscribe and unsubscribe from the list without human intervention. The owner of the list can restrict who subscribe, unsubscribe, and post messages to the list. Other popular lists include LISTSERV (www.lsoft.com), Lyris (www.lyris.com), and Majordomo (www.greatcircle.com/majordomo). Ubuntu maintains a few mailing lists and list archives for those mailing lists atubuntu.com. Use Google to search linux mailing list to find others.

## NETWORK UTILITIES

To realize the full benefits of a networked environment, it made sense to extend certain tools, some of which have already been described. The advent of networks also created a need for new utilities to control and monitor them, spurring the development of new tools that took advantage of network speed and connectivity. This section describes concepts and utilities for systems attached to a network.

¹¹ Although the term listserv is sometimes used generically in many different list server programs, it is a specific product and a registered trademark of Lsoft International, Inc.: LISTSERV (for more information to go to www.lsoft.com).

## TRUSTED HOSTS

Some commands, such as rcp and rsh, work only if the remote system trusts your local computer (that is, if the remote system knows your local computer and believes that it is not pretending to be another system). The /etc/hosts file lists trusted systems. For reasons of security, the root account does not rely on this file to identify trusted users from other systems.

Host-based trust is largely obsolete. Because there are many ways to circumvent trusted host security, including subverting DNS systems and IP spoofing (page 1154), authentication based on IP address is widely regarded as insecure and obsolete. In a small homogeneous network of machines with local DNS, it can be “good enough.” Its greater ease of use in these situations may outweigh the security concerns.

## Do not share your login account

You can use a ~/.hosts file to allow another user to log in as you from a remote system without knowing your password. This setup is not recommended. Do not compromise the security of your files or the entire system by sharing your login account. Use ssh and sc instead of rsh and rcp whenever possible.

## SSH TOOLS

The OpenSSH project provides a set of tools to replace rcp, rsh, and others with equivalents. These tools are installed by default in Ubuntu Linux and can be used as drop-in replacements for their insecure counterparts. The OpenSSH tool suite is covered in detail in Chapter 8.

## telnet: LOGS IN ON A REMOTE SYSTEM

You can use the TELNET protocol to interact with a remote computer. The telnet utility, a user interface to this protocol, is older than ssh and is not secure. Nevertheless, it may work where ssh (page 670) is not available (there is more non-UNIX support for TELNET for ssh access). In addition, many legacy devices, such as terminals and network devices, do not support ssh.
