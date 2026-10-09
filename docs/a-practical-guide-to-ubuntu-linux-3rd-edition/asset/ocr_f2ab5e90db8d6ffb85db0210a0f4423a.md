+   • Provided with Ubuntu Linux is PAM, which allows you to set up different methods and levels of authentication in many ways (page 478).

+   • Process accounting—a good supplement to system security—can provide a continuous record of user actions on your system. See the accton man page (part of the acct package) for more information.

+   • Emerging standards for such things as Role-Based Access Control (RBAC) allow tighter delegation of privileges along defined organizational boundaries. You can delegate a role or roles to each user as appropriate to the access required.

+   • General mailing lists and archives are useful repositories of security information, statistics, and papers. The most useful are the bugtraq mailing list and CERT. The bugtraq site and email service offer immediate notifications about specific vulnerabilities, whereas CERT provides notice of widespread vulnerabilities and useful techniques to fix them, plus links to vendor patches.

+   • The syslogd facility can direct messages from system daemons to specific files such as those in /var/log. On larger groups of systems, you can send all important syslogd information to a secure host, where that host’s only function is to store syslogd data so it cannot be tampered with. See page 404 and the syslogd man page for more information.

# ## Login Security

Without a secure host, good login security cannot add much protection. Table C-1 on page 1124 lists some of the best login security tools, including replacement daemons for telnetd, rlogind, and rshd. Many sites use ssh, which comes as both free-ware and a commercially supported package that works on UNIX/Linux, Windows, and Macintosh platforms.

The PAM facility (page 478) allows you to set up multiple authentication methods for users in series or in parallel. In-series PAM requires multiple methods of authentication for a user. In-parallel PAM uses any one of a number of methods for authentication.

Although not the most popular choice, you can configure a system to take advantage of one-time passwords. S/Key is the original implementation of one-time passwords by Bellcore. OPIE (one-time passwords in everything), which was developed by the U.S. Naval Research Labs, is an improvement over the original Bellcore system. In one permutation of one-time passwords, the user gets a piece of paper listing a set of one-time passwords. Each time a user logs in, she enters a password from the piece of paper. Once used, a password becomes obsolete, and the next password

> 7. CERT is slow but useful as a medium for coordination between sites. It acts as a tracking agency to document the spread of security problems.