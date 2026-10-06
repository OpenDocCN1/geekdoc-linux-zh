
# Host Security

Your host must be secure. Simple security steps include preventing remote logins and leaving the /etc/hosts.equiv and individual users ~/.hosts empty (or not having them at all). Complex security steps include installing IPSec for VPNs between hosts. Many common security measures are between these two extremes. A few of these follow. See Table C-1 on page 1421 for URLs.

- All potentially tricky to implement and manage, Intrusion Detection Systems (IDS) are an excellent way to keep an eye on the integrity of a device. An IDS can warn of possible attacks at subverting the host on which it runs. The great-grandsaddy of intrusion detection systems is tripwire. This host-based system checks modification times and integrity of files by using strong algorithms (cryptographic checksums and signatures) that can detect the most minor modification. There is also a commercial version of tripwire. Another commercial IDS is DragonSquire. Other free, popular, and flexible IDS include samhain and AIDE. These last two even more features and means of remaining invisible to users than tripwire. Commercial IDS that are popular in enterprise environments include Cisco IDS (formerly NetRanger), Enterasys Dragon, and IISSecure.

- The redhat-watch-list mailing list (note the s following in this URL: https://listman.redhat.com/pipermail/redhat-watch-list), can keep you up-to-date on security and bugfix announcements. Go to https://listman.redhat.com/mailman/listinfo/redhat-watch-list to subscribe to this list.

- Red Hat Network (RHN) can automatically or semiautomatically keep one or more systems up-to-date (page 936), preventing your system from becoming prey to fixed security bugs.

- Complementing host-based intrusion detection systems are network-based intrusion detection systems. These programs monitor the network and nodes and report suspicious occurrences (attack signatures) via user-defined alerts. These signatures can be matches on known worms, overflow attacks against programs, or unauthorized scans of network ports. Such programs as sport, klaxon, and NFR are used in this capacity. Commercial programs, such as DragonCentury, also fill this role.

- Provided with Red Hat Linux is PAM, which allows you to set up different methods and levels of authentication in many ways (page 1043).

- Process accounting, a good supplement to system security, can provide a continuous record of user actions on your system. See the acton man page for more information.

- Emerging standards for such things as Role Based Access Control (RBAC) allow tighter delegation of privileges along defined organizational boundaries. You can delegate each user a role or roles appropriate to the access required.

- General mailing lists and archives are an extremely useful repository of security information, statistics, and papers. The most useful are the bugtrap mailing list and CERT®. The bugtrap site and e-mail provide immediate notifications about specific vulnerabilities, whereas CERT provides notice of widespread vulnerabilities and useful techniques to fix them, as well as links to vendor patches.

- The syslog facility (provided with Red Hat Linux) can direct messages from system daemons to specific files such as in /var/log. On larger groups of systems, you can send all syslog information to a secure host, where host's only function is to store syslog data so that it cannot be tampered with. See page 399 and the syslogd man page.

# Login Security

Without a secure host, good login security cannot add much protection. “Where to Get It,” on page 1421 lists some of the best login security tools, including replacement daemons for telnet, rlogind, and rsh. The current choice of most systems is ssh, which comes from both freeway and a commercially supported package that works on UNIX/Linux, MS Windows, and Macintosh platforms.

The PAM facility (page 1043) allows you to set up multiple authentication methods for users in series or in parallel. In-series PAM requires multiple methods of authentication for a user. In-parallel PAM uses any one of a number of methods for authentication.

Although not a frequent choice, you can configure your system to take advantage of one-time passwords. S/Key is the original implementation of one-pass passwords by Bellcore. OPI (one-time passwords in everything), developed by the U.S. Naval Research Labs, is an improvement over the original Bellcore system. In permutation of one-time passwords, the user gets a piece of password listing a set of one-time passwords. Each time a user logs in, the user enters a password from the piece of paper. Once used, a password becomes obsolete, and the next password in the list is the only one that will work. Even if a malicious user compromises the network and sees your password, it will be of no use only one time. This setup makes it very difficult to log in as you want to but does nothing about protecting the data you type at the keyboard. One-time passwords

> 8. CERT is slow but useful as a medium for coordination between sites. It acts as a tracking agency to document the spread of security problems.

# Appendix C Security

Passwords are a good solution if you are at a site where no encrypted login is available. A truly secure (or paranoid) site will combine one-time passwords and encrypted logins.

Another type of secure login that is becoming more common is facilitated by a token or a smart card. Smart cards are credit-card-like devices that use a challenge-response method of authentication. Smart card and token authentication rely on something you have (the card) and something you know (a pass phrase, user ID, or pin). For example, you might enter your login name in response to the login prompt and get a password prompt. In response, you enter your PIN and the number displayed on the token. The token has a unique serial number that is stored in a database of the authentication server. The token and authentication server use this serial number as a measure of computing every 30 to 60 seconds. If the pin and token number you enter match what it be computed by the access server, you are granted access to the system.

# Remote Access Security

Issues and solutions surrounding remote access security overlap those pertaining to login and host security. Local logins may be secure with a simple login name and password, whereas remote logins (and all remote access) should be made more secure. Many breaks can be traced to reusable passwords. It is a good idea to use an encrypted authentication client, such as ssh or kerberos. You can also use smart cards for remote access.

Modem pools can also be an entry point. Most people are aware of how easy it is to monitor a network line. But people take for granted the security of the public switched telephone network (PSTN, also POTS—plain old service). You may want to set up an encrypted channel after dialing in a modem. One way to do this is by running PPP.

There are ways to provide stringent modem authentication policies so that unauthorized users are not able to use your modems. The most common techniques are PAP (password authentication protocol), CHAP (challenge handshake authentication protocol), and Radius. PAP and CHAP are relatively weak when compared to Radius, so the latter has rapidly gained in popularity. Cisco also provides a method of authentication called TACACS/TACACS+.

One or more of these authentication techniques is available in a RAS (remote access server—in a network by computer that provides network access to remote users via modem). Before purchasing a RAS, check what kind of security it provides and decide whether level of security meets your needs.

Two other techniques for remote access security can be built into a modem (RAS if it has integrated modems). One is callback: After you dial, you get a password prompt. If you type in your password, modem hangs up and calls you back at a phone number it has stored internally. But this technique is not foolproof.
