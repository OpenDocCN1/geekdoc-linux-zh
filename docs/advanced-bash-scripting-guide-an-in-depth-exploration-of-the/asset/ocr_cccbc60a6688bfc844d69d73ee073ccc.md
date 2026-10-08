# Advanced Bash-Scripting Guide

./is_spammer.bash 0 web4.alojamentos7.com
Starting with domain name >web4.alojamentos7.com
Using default blacklist server list.
Search depth: 0

```
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
Known network pairs:
66.208.297 web4.alojamentos7.com.
66.208.297 nsl1.alojamentos7.com.
69.56.202.147 nsl2.alojamentos7.ws.
66.208.297 alojamentos7.com.
66.208.297 nsl1.alojamentos.ws.
69.56.202.147 alojamentos.ws.
66.235.180.113 nsl1.alojamentos.org.
66.235.181.192 nsl2.alojamentos.org.
66.235.180.113 alojamentos.org.
216.234.234.30 web6.alojamentos.org.
12.96.160.115 nsl1.theplanet.com.
216.185.111.52 nsl2.theplanet.com.
69.56.141.4 maili.theplanet.com.
216.185.111.40 spoofing:theplanet.com.
216.185.111.40 www.theplanet.com.
216.185.111.52 mail.theplanet.com.
```

Checking Blacklist servers.
Checking 66.208.297
Records from dnsbl.sorbs.net
*Spam Reported See here: http://www.dnbl.sorbs.net/lookup.shtml?766.208.297*
Checking address 69.56.202.147
Checking address 69.56.202.146
Checking address 66.235.180.113
Checking address 66.235.181.192
Checking address 216.185.111.40
Checking address 216.234.234.30
Checking address 12.96.160.115
Checking address 216.185.111.52
Checking address 69.56.141.4

Advanced Bash Scripting Guide: is_spammer.bash, v2, 2004-ms

```
is_spammer_outputs_

exit $ {HS_RC}

################################################################
# The script ignores everything from here down #
#+ because of the 'exit' command, just above.
################################################################
```

# Quickstart
=====================

Prerequisites

Bash version 2.05b or 3.00 (bash --version)
A version of Bash which supports arrays. Array
support is included by default Bash configurations.

# Appendix A. Contributed Scripts