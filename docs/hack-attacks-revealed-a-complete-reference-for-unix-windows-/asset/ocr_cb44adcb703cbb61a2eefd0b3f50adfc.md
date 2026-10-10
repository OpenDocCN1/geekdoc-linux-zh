# From the Console

+   * **Information gathering.** From the console on a domain controller, hackers use the following simple steps to get a list of accounts on the target machine. With a list of user accounts, they can target individual attacks:

+   1. From the User Manager, create a trusting relationship with the target.
+   2. Launch NT Explorer, and right-click on any folder.
+   3. Select Sharing.
+   4. From the Shared window, select Add.
+   5. From the Add menu, select the target NT server. This will reveal the entire group listing of the target.
+   6. Select Show Users to see the entire user listing, including full names and descriptions.

# Novell NetWare

Novell, Inc. (www.novell.com) is a leading provider of system operation software for all types of corporate and private networks including intranets, extranets, and the Internet. Quickly climbing the corporate usage ladder since 1983, Novell NetWare currently is being used in 81 percent of Fortune 500 companies in the United States (according to Harle Hanks Market Intelligence). The company boasts greater security provision throughout the Net while accelerating e-business transformations.

# Liabilities

Getting In

Hacking the Console

**Synopsis:** Simple techniques can facilitate console breaches.

**Hack State:** Administrative privileges exploitation.

**Vulnerabilities:** All flavors prior to version 4.11.

**Breach:** When NetWare administrators load NetWare loadable modules (NLMs) `remote.nlm` and `rspx.nlm`, hackers seek a program titled `rconsole.exe`, typically from the `//public` directory. At this point, and on the same address scheme as the administrator and/or target server, the hacker loads an IPX packet sniffer and waits to capture the system password. Among hackers, a popular sniffer package is SpyNet (Chapter 8 describes this package more fully). If the attacker wants to conceal evidence of the hack, he or she erases the system log from `//etc/console.log` by unloading and reloading the conlog.nlm. This starts a new log capture file over the old one, which contains the evidence.

Stealing Supervisory Rights

**Synopsis:** Custom coding can modify a standard login account to have supervisory equivalence.

**Hack State:** Administrative privileges exploitation.

**Vulnerabilities:** NetWare 2x, 3x, 4x, IntraNetWare 4x.

**Breach:** The tempting challenge of any local hacker on a Novell network is to gain supervisory rights. `Crack98.c` by renowned hacker Mnemonic sets the connection to 0 for supervisor, then creates