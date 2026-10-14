
# `/usr/sbin/faxsetup`

```
01: # /usr/sbin/faxsetup

02: Setup program for HylaFAX (tm) 4.1beta1.

03: Created for i686-pc-linux on Thu Jul 1 15:05:50 BST 1999.

04: Checking system for proper client configuration.
05: Checking system for proper server configuration.
06: Warning: /sbin/vgetty does not exist or is not an executable program!
07: The file:

08: /sbin/vgetty

09: does not exist or this file is not an executable program.  The
10: HylaFAX software optionally uses this program and the fact that
11: it does not exist on the system is not a fatal error.  If the
12: program resides in a different location and you do not want to
13: install a symbolic link for /sbin/vgetty that points to your program
14: then you must reconfigure and rebuild HylaFAX from source code.

15: Warning: /bin/egetty does not exist or is not an executable program!

16: The file:

17: /bin/egetty

18: does not exist or this file is not an executable program.  The
19: HylaFAX software optionally uses this program and the fact that
20: it does not exist on the system is not a fatal error.  If the
21: program resides in a different location and you do not want to
22: install a symbolic link for /bin/egetty that points to your program
23: then you must reconfigure and rebuild HylaFAX from source code.

24: Make /var/spool/fax/bin/ps2fax a link to /var/spool/fax/bin/ps2fax.gs.

25: You do not appear to have a "fax" user in the password file.
26: HylaFAX needs this to work properly, add it [yes]?
27: Added user "fax" to /etc/passwd.

28: Modem support functions written to /var/spool/fax/etc/setup.modem.
29: Configuration parameters written to /var/spool/fax/etc/setup.cache.

30: No scheduler config file exists, creating one from scratch.
31: Country code [1]? 972
32: Area code []? 4
33: Long distance dialing prefix [1]? 0
34: International dialing prefix [011]? 00
35: Dial string rules file (relative to /var/spool/fax) ["etc/dialrules"]?
36: Tracing during normal server operation [1]?
37: Default tracing during send and receive sessions [0xffffffff]?
38: Continuation cover page (relative to /var/spool/fax) []?
39: Timeout when converting PostScript documents (secs) [180]?
40: Maximum number of concurrent jobs to a destination [1]?
41: Define a group of modems []?
42: Time of day restrictions for outbound jobs ["Any"]?
43: Pathname of destination control file (relative to /var/spool/fax) []?
44: Timeout before purging a stale UUCP lock file (secs) [30]?
45: Max number of pages to permit in an outbound job [0xffffffff]? 25
46: Syslog facility name for ServerTracing messages [daemon]?

47: The non-default scheduler parameters are:

48: CountryCode:        972
49: AreaCode:           4
50: LongDistancePrefix:      0
51: InternationalPrefix:     00
52: MaxSendPages:             25

53: Are these ok [yes]?

54: Creating new configuration file /var/spool/fax/etc/config...

55: Restarting HylaFAX server processes.
56: Should I restart the HylaFAX server processes [yes]?

57: /etc/rc.d/init.d/hylafax start
58: HylaFAX: faxq hfaxd (without old protocol or SNPP support).

59: You do not appear to have any modems configured for use.  Modems are
60: configured for use with HylaFAX with the faxaddmodem(1M) command.
61: Do you want to run faxaddmodem to configure a modem [yes]?
62: Serial port that modem is connected to []? ttyS1
63: Hmm, there does not appear to be a fuser command on your machine.
64: This means that I am unable to insure that all processes using the
65: modem have been killed.  I will keep going, but beware that you may
66: have competition for the modem.

67: Ok, time to setup a configuration file for the modem.  The manual
68: page config(4F) may be useful during this process.  Also be aware
69: that at any time you can safely interrupt this procedure.

70: Reading scheduler config file /var/spool/fax/etc/config.

71: No existing configuration, let's do this from scratch.

72: Country code [1]? 972
73: Area code [415]? 4
74: Phone number of fax modem [+1.999.555.1212]? +972.4.8331039
75: Local identification string (for TSI/CIG) ["NothingSetup"]? "MyFaxServer"
76: Long distance dialing prefix [1]? 0
77: International dialing prefix [011]? 00
78: Dial string rules file (relative to /var/spool/fax) [etc/dialrules]?
79: Tracing during normal server operation [1]?
80: Tracing during send and receive sessions [11]?
81: Protection mode for received facsimile [0600]?
82: Protection mode for session logs [0600]?
83: Protection mode for ttyS1 [0600]?
84: Rings to wait before answering [1]?
85: Modem speaker volume [off]?
86: Command line arguments to getty program ["-h %l dx_%s"]?
87: Pathname of TSI access control list file (relative to /var/spool/fax) [""]?
88: Pathname of Caller-ID access control list file (relative to /var/spool/fax) [""]?
89: Tag line font file (relative to /var/spool/fax) [etc/lutRS18.pcf]?
90: Tag line format string ["From %s|%c|Page %p of %t"]?
91: Time before purging a stale UUCP lock file (secs) [30]?
92: Hold UUCP lockfile during inbound data calls [Yes]?
93: Hold UUCP lockfile during inbound voice calls [Yes]?
94: Percent good lines to accept during copy quality checking [95]?
95: Max consecutive bad lines to accept during copy quality checking [5]?
96: Max number of pages to accept in a received facsimile [25]?
```
