![](Images/cover00194.jpeg)

![](Images/image00193.jpeg)

KALI LINUX

TOOLS

REVEALED A STEP BY STEP GUIDE TO LEARN WIRELESS PENETRATION TECHINQUES AND BASICS OF PENETRATION TESTING, INCLUDES COMMAND LINE AND HACKING WITH KALI LINUX FOR BEGINNERS.

BY

RANDY GIBSON

TABLE OF CONTENTS

CHAPTER ONE

DATA GATHERING - VOIP ANALYSIS

CHAPTER TWO

DATA GATHERING - VPN ANALYSIS

CHAPTER THREE

WEAKNESS ANALYSIS

CHAPTER FOUR

INFORMATION BASE ASSESSMENT

CHAPTER FIVE

FUZZING TOOLS

CHAPTER SIX

MISC SCANNERS

CHAPTER SEVEN

OPEN SOURCE ASSESSMENT

CHAPTER EIGHT

OPEN-VAS

CHAPTER NINE

WEB APPLICATIONS: CMS IDENTIFACTION

CHAPTER TEN

DATA SET EXPLOITATION

CHAPTER ELEVEN

IDS/IPS IDENTIFACATION

CHAPTER TWELVE

WEB APPLICATION FUZZERS

CHAPTER THIRTEEN

WEB APPLICATION PROXIES

CHAPTER FOURTEEN

WEB CRAWLERS

CHAPTER FIFTEEN

WEB VULNERABILITY SCANNERS

CHAPTER SIXTEEN

SECRET PHRASE ATTACKS: GPU TOOLS

CHAPTER SEVENTEEN

DISCONNECTED ATTACKS

CHAPTER EIGHTEEN

ONLINE ATTACKS

INTRODUCTION

This reference guide portrays every contraption independently and is centered on any person who needs to get to know automated criminal science and penetration testing or resuscitate their knowledge around there with devices open in Kali Linux. Note! I've endeavored to gather whatever amount of information as could sensibly be anticipated, regardless, even notwithstanding that, a couple of sections don't have information, which I might revive on the off chance that I get more information. Also, messes up are inevitable.

The justification for existing was to make the most point by point wellspring of every device in Kali Linux for quick reference and better plan. The information about each instrument when in doubt contains: DESCRIPTION, USAGE, EXAMPLE and now and again OPTIONS and TIPs. Kali Linux mechanical assemblies are not limited to Kali Linux/Backtrack (most can be presented on other Linux disseminations pondering all of the significant conditions.

Besides, a couple of devices are moreover open on various types of working systems like Windows and Mac OS). Kali Linux is a new and making OS – a couple of devices may be added, a couple - revived, a couple – wiped out as time goes on. It is acknowledged that all instruments are run as root (or as head) (in Kali Linux you are root as per usual).

Every one of the information collected with regards to every device has been found uninhibitedly on the Internet and is straightforwardly open. Wellsprings of information are alluded to close to the end.

Most request line gadgets join decisions, in any case, due to space examinations, only a couple devices have options recorded (filter the web for decisions, read documentation/manual, use – h or - help).

For additional information on each instrument - search the web, click on associations or really investigate the references around the end

NB:

Benevolently DO NOT USE KALI LINUX AND THE TOOLS LISTED HERE FOR ANY ILLEGAL OPERATION! Gadgets which are unequivocally centered around DOS, DDOS or anonymity are now and again used in certifiable responsibility, and are as such not presented obviously in Kali Linux

CHAPTER ONE

DATA GATHERING - VOIP ANALYSIS

• pro

• enumiax

Pro

DESCRIPTION

Pro (Automated Corporate Enumerator) is a basic yet incredible VoIP Corporate Directory specification apparatus that mirrors the conduct of an IP Phone to download the name and expansion passages that a given telephone can show on its screen interface. Expert can be utilized in one of two ways. In the first place, it can auto discover the TFTP Server IP Address through DHCP, or (second) the client can indicate the TFTP Server IP address as an order line boundary of the instrument. Regardless, you should supply the MAC Address of the IP Phone with the - m choice all together for the instrument to effectively download the setup record through TFTP.

USAGE: pro [-I interface] [ - m macintosh address ] [ - t tftp server ip address | - c cdp mode | - v voice vlan id | - r vlan interface | - d verbose mode ]

OPTIONS: http://ucsniff.sourceforge.net/ace.html

EXAMPLE: pro - I eth0 - v 96 - m 00:1E:F7:28:9C:8E (Mode to indicate the Voice VLAN ID)

EXAMPLE: pro - I eth0 - c 0 - m 00:1E:F7:28:9C:8E (Mode to auto-find voice vlan ID in the listening mode for CDP

EXAMPLE: pro - I eth0 - c 1 - m 00:1E:F7:28:9C:8E (Mode to auto-find voice vlan ID in the mocking mode for CDP)

Enumiax

DESCRIPTION

enumIAX is an Inter Asterisk Exchange rendition 2 (IAX2) convention username animal power enumerator. enumIAX might work in two unmistakable modes; Sequential Username Guessing or Dictionary Attack.

USAGE: enumiax [options]

OPTIONS:

-d Dictionary assault utilizing document

-I Interval for auto-save (# of activities, default 1000)

-m # Minimum username length (in characters)

-M # Maximum username length (in characters)

-r # Rate-limit calls (in microseconds)

-s Read meeting state from state document

-v Increase verbosity (rehash for extra verbosity)

-V Print adaptation data and exit

-h Print help/use data and exit

EXAMPLE: enumiax 172.16.1.100 – m 4 – M 8 – v (enumIAX under successive mode endeavoring usernames that have four and eight characters) enumiax 172.16.1.100 – d dict – v (next, use enumIAX under word reference mode by utilizing the accompanying sentence structure)

EXAMPLE:./enumiax - v - m3 - M3 192.168.1.104 ./enumiax - d dict - v 192.168.1.104

CHAPTER TWO

DATA GATHERING - VPN ANALYSIS

• ike-filter

ike-filter

DESCRIPTION

Ike-filter is an order line device that utilizes the IKE convention to find, unique mark and test IPSec VPN servers. ike-filter permits you to:

• Send IKE bundles to quite a few objective hosts, utilizing a configurable result transmission capacity or parcel rate. This is valuable for VPN discovery, when you might have to filter enormous location spaces.

• Develop the active IKE bundle in an adaptable manner. This incorporates IKE parcels which don't follow the RFC prerequisites.

• Translate and show any brought bundles back.

• Break forceful mode pre-shared keys. You can utilize ike-output to get the PSK hash information, and afterward use psk-break to acquire the key. Use ike-examine [options] [hosts...]

OPTIONS: http://www.nta-monitor.com/wiki/index.php/Ike-scan_User_Guide or ike-filter - - help

EXAMPLE: ike-filter - M 10.0.0.0/24

EXAMPLE: ike-filter - - auth=3 10.0.0.0/24 (utilize the standard change set with the confirmation strategy set to RSA Signature rather than the default Pre-Shared key for each change. This strategy is shockingly compelling at finding VPN servers that will not react to the standard change set.)

EXAMPLE: ike-check - M - - trans=5,2,1,2 - - showbackoff 10.0.0.1 (backoff fingerprinting)

CHAPTER THREE

WEAKNESS ANALYSIS

• cisco-examining instrument

• cisco-worldwide exploiter

• cisco-ocs

• cisco-light

• Yersinia

cisco-inspecting instrument

DESCRIPTION

Cisco Auditing Tool - Perl script which examines cisco switches for normal weaknesses. Checks for default passwords, effectively guessable local area names, and the IOS history bug. Incorporates support for modules and filtering various hosts.

USAGE: ./CAT [options]

OPTIONS:

-h hostname (for examining single hosts)

-f hostfile (for examining various hosts)

-p port # (default port is 23)

-w (wordlist for local area name speculating)

-a passlist (wordlist for secret key speculating)

-I [ioshist] (Check for IOS History bug)

-l logfile (record to log to, default screen)

-q calm mode (no screen yield)

EXAMPLE: ./CAT - h 192.168.1.100 - w wordlist - a passwords - I

EXAMPLE:./CAT - h 192.168.1.22 - a rundowns/passwords - w records/local area (Audit Cisco Telnet Password and SNMP Community String)

cisco-worldwide exploiter

DESCRIPTION:

Cisco Global Exploiter (CGE), is a high level, straightforward and quick security testing apparatus/exploit motor that can take advantage of 14 weaknesses in different Cisco switches and switches. CGE is order line driven Perl script which has a straightforward and simple to utilize front-end.

USAGE: cge.pl<target>< vulnerability number>

OPTIONS: (14 weaknesses)

[1] - Cisco 677/678 Telnet Buffer Overflow Vulnerability

[2] - Cisco IOS Router Denial of Service Vulnerability

[3] - Cisco IOS HTTP Auth Vulnerability

[4] - Cisco IOS HTTP Configuration Arbitrary Administrative Access Vulnerability

[5] - Cisco Catalyst SSH Protocol Mismatch Denial of Service Vulnerability

[6] - Cisco 675 Web Administration Denial of Service Vulnerability

[7] - Cisco Catalyst 3500 XL Remote Arbitrary Command Vulnerability

[8] - Cisco IOS Software HTTP Request Denial of Service Vulnerability

[9] - Cisco 514 UDP Flood Denial of Service Vulnerability

[10] - CiscoSecure ACS for Windows NT Server Denial of Service Vulnerability

[11] - Cisco Catalyst Memory Leak Vulnerability

[12] - Cisco CatOS CiscoView HTTP Server Buffer Overflow Vulnerability

[13] - 0 Encoding IDS Bypass Vulnerability (UTF)

[14] - Cisco IOS HTTP Denial of Service Vulnerability

EXAMPLE: cge.pl 192.168.1.254 3 (exploit the Cisco IOS HTTP Auth Vulnerability and ideally utilizing the pleasant connection gave we ought to have essential admittance to the switch we are assaulting, (not empower))

cisco-ocs

DESCRIPTION

cisco-ocs otherwise called cisco-ocs Mass Scanner. This apparatus gives a solitary capacity which is to check enormous scopes of IP's searching for Cisco gadgets or actually any gadget tuning in on TCP port 23, endeavors to login utilizing telnet with a secret key of cisco, then, at that point, passes the empower order to the Cisco switch if its ready to login through telnet, utilizes cisco again for the empower secret phrase, lastly reports a triumph if its ready to get to the empower brief utilizing these precise advances. Tragically, this is the main capacity of the apparatus as you can't indicate a wordlist of passwords to endeavor or so far as that is concerned you can't set anything acknowledge for the scope of IP locations to examine.

USAGE: ./ocs <range start IP> <range end IP>

EXAMPLE: ./ocs 192.168.1.21 192.168.1.23

cisco-light

DESCRIPTION

Cisco Light was planned as a mass examining, fingerprinting, and double-dealing apparatus. Cisco light is not normal for different instruments in that it uses various strings, (forking methods), to dispatch filtering processes. It likewise utilizes a few strategies to all the while do application layer fingerprinting. Cisco Light can be utilized for dispatching word reference based secret key assaults against the administrations and finding has running the accompanying administrations: Telnet, SSH, Web, NTP, SNMP.

USAGE: ./cisco- light.pl<options>< IP,hostname,network>

USAGE:./cisco- light.pl<options> - F<hostlist>

OPTIONS: really look at http://www.vulnerabilityassessment.co.uk/torch.htm

EXAMPLE: ./cisco- light.pl - A 10.10.0.0/16

EXAMPLE:./cisco- light.pl - s - b - F sshtocheck.txt

EXAMPLE:./cisco- light.pl - w - z 10.10.0.0/16

EXAMPLE:./cisco- light.pl - j - b - g - F tftptocheck.txt

Yersinia

DESCRIPTION

Yersinia is an organization instrument intended to exploit a few shortcomings in various organization conventions. It professes to be a strong structure for investigating and testing the sent organizations and frameworks. Assaults for the accompanying organization conventions are executed: Spanning Tree Protocol (STP), Cisco Discovery Protocol (CDP), Dynamic Trunking Protocol (DTP), Dynamic Host Configuration Protocol (DHCP), Hot Standby Router Protocol (HSRP), IEEE 802.1Q, IEEE 802.1X, Inter-Switch Link Protocol (ISL), VLAN Trunking Protocol (VTP) USAGE yersinia [-hVID] [-l logfile] convention [protocol_options]

OPTIONS:

-V Program variant.

-h This assistance screen.

-I Interactive mode (ncurses).

-D Daemon mode.

-l logfile Select logfile.

-c conffile Select config record.

Protocol Can be one of the accompanying: cdp, dhcp, dot1q, dtp, hsrp, stp, vtp

EXAMPLE: yersinia – D (run in Daemon mode)

CHAPTER FOUR

INFORMATION BASE ASSESSMENT

• bbqsql

• dbpwaudit

• hexorbase

• mdb-export

• mdb-parsecsv

• mdb-sql

• mdb-tables

• oscanner

• sidguesser

• sqldict

• sqlmap

• sqlninja

• sqlsus

• tnscmd10g

bbqsql

DESCRIPTION

Blind SQL infusion can be an aggravation to take advantage of. At the point when the accessible devices work they function admirably, however when they don't you need to compose something custom. This is tedious and dreary. BBQSQL can assist you with resolving those issues.

BBQSQL is a visually impaired SQL infusion system written in Python. It is incredibly valuable while assaulting interesting SQL infusion weaknesses. BBQSQL is likewise a self-loader apparatus, permitting a considerable amount of customization for those difficult to trigger SQL infusion discoveries. The device is worked to be information base freethinker and is amazingly adaptable. It likewise has a natural UI to make setting up assaults a lot simpler.

Python gevent is additionally carried out, making BBQSQL amazingly quick.

USAGE: n/a, choice determination/arrangement

OPTIONS: https://github.com/Neohapsis/bbqsql

EXAMPLE: n/a

dbpwaudit

DESCRIPTION

DBPwAudit is a Java apparatus that permits you to perform online reviews of secret phrase quality for a very long time motors. The application configuration considers simple adding of extra data set drivers by basically duplicating new JDBC drivers to the jdbc index. Design is acted in two documents, the aliases.conf record is utilized to plan drivers to nom de plumes and the rules.conf lets the application know how to deal with blunder messages from the sweep.

The apparatus has been tried and known to work with:

- Microsoft SQL Server 2000/2005

- Prophet 8/9/10/11

- IBM DB2 Universal Database

- MySQL

USAGE: dbpwaudit – s<server> - d<db> - D<driver> - U<users> - P<passwords> [options]

OPTIONS: http://www.edwiget.name/2012/07/evaluating mysql-passwords-with-dbpwaudit/

EXAMPLE: ./dbpwaudit.sh - s localhost - d mysql - D MySQL - U ~/mysql-users.txt - P ~/mysql-password.txt (Assuming I have a db server on localhost and a rundown of mysql usernames saved in my home index as mysql-users.txt and a rundown of passwords to attempt likewise in my home catalog as mysql-password.txt, this order would review the mysql server)

TIP: extra advances are needed for this program to work: http://www.edwiget.name/2012/07/evaluating mysql-passwords-with-dbpwaudit/

Hexorbase

DESCRIPTION

HexorBase is an information base application intended for regulating and examining numerous data set servers all the while from a brought together area, it is fit for performing SQL inquiries and bruteforce assaults against normal data set servers (MySQL, SQLite, Microsoft SQL Server, Oracle, PostgreSQL ). HexorBase permits parcel steering through intermediaries or even Metasploit turning shenanigans to speak with somewhat distant servers which are concealed inside neighborhood subnets.

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

mdb-export

DESCRIPTION

The MDB Tools project is a work to record the MDB document design utilized in Microsoft's Access data set bundle, and to give a bunch of devices and applications to make that information accessible on different stages. In particular, MDB Tools incorporates projects to send out mapping and information to different data sets like MySQL, Oracle, Sybase, PostgreSQL, and others.

mdb-export is a utility program circulated with MDB Tools. It delivers a CSV (comma isolated worth) yield for the given table. Such result is reasonable for importation into information bases or accounting pages.

USAGE: mdb-export [-H] [-d ] [-R ] [[-Q] || [-q [-X ]]] [-I] [-D ] [-S]

OPTIONS: http://linux.die.net/man/1/mdb-trade

EXAMPLE: mdb-export - d ';' something.mdb Main > Main.csv

EXAMPLE: mdb-export - X \ - D "%Y-%m-%d %H:%M:%S" orsk.mdb Main > Main.csv

mdb-parsecsv

DESCRIPTION

The MDB Tools project is a work to archive the MDB record design utilized in Microsoft's Access data set bundle, and to give a bunch of apparatuses and applications to make that information accessible on different stages. In particular, MDB Tools incorporates projects to trade diagram and information to different data sets like MySQL, Oracle, Sybase, PostgreSQL, and others.

mdb-parsecsv is a utility program dispersed with MDB Tools. mdb-parsecsv takes a CSV record addressing an information base table, and converts it into a C exhibit. Assuming the principal contention doesn't exist as a document, mdb-parsecsv will search for a similar filename with '.txt' affixed. The document expansion is stripped, and the result kept in touch with the base name in addition to a '.c' augmentation.

USAGE: n/a

EXAMPLE: n/a

mdb-sql

DESCRIPTION

The MDB Tools project is a work to report the MDB record design utilized in Microsoft's Access data set bundle, and to give a bunch of apparatuses and applications to make that information accessible on different stages. In particular, MDB Tools incorporates projects to send out composition and information to different data sets like MySQL, Oracle, Sybase, PostgreSQL, and others.

mdb-sql - an order line SQL apparatus that permits one to type sql inquiries and get results. mdb-sql permits questioning of a MDB data set utilizing a restricted SQL subset language.

USAGE: mdb-sql [-HFp] [-d<delimiter>] [-I<file> ] [-o<file> ] [<database>]

OPTIONS: http://linux.die.net/man/1/mdb-sql

EXAMPLE: n/a

mdb-tables

DESCRIPTION

The MDB Tools project is a work to archive the MDB record design utilized in Microsoft's Access data set bundle, and to give a bunch of apparatuses and applications to make that information accessible on different stages. In particular, MDB Tools incorporates projects to send out pattern and information to different data sets like MySQL, Oracle, Sybase, PostgreSQL, and others.

mdb-tables is a utility program dispersed with MDB Tools. It delivers a rundown of tables held inside a MDB data set in an arrangement appropriate for use in shell scripts.

USAGE: mdb-tables [-S] [-1|-d <delimiter>] <database>

OPTIONS: http://linux.die.net/man/1/mdb-tables

EXAMPLE: mdb-tables database.mdb

Oscanner

DESCRIPTION

Oscanner is an Oracle appraisal structure created in Java. It has a module based design and accompanies a few modules that presently do: Sid Enumeration, Passwords tests (normal and word reference), Enumerate Oracle adaptation, Enumerate account jobs, Enumerate account advantages, Enumerate account hashes, Enumerate review data, Enumerate secret phrase strategies, Enumerate information base connections

USAGE: OracleScanner – s<ip> - r<repfile> [options]

USAGE: oscanner – s<ip> - r<repfile> [options]

OPTONS:

–s<servername>

-f<serverlist>

-P<portnr>

-v be verbose

EXAMPLE: oscanner.sh - s 192.168.0.1

Sidguesser

DESCRIPTION

sidguesser surmises sids/occurrences against an Oracle information base as per a predefined word reference document. The speed is slow (80-100 conjectures each second) however it does the work.

USAGE: sidguesser - I - d [options]

OPTIONS:

-p<portnr> Use explicit port (default 1521)

-r<report> Report to document

-m<mode> findfirst OR findall (default)

EXAMPLE: sidguesser - I 192.168.0.223 - d words.txt

Sqldict

DESCRIPTION

SQLdict is an essential single ip animal power MS SQL Server secret word utility that can complete a word reference assault against a named SQL account.

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

sqlmap

DESCRIPTION

sqlmap is an open source infiltration testing device that mechanizes the method involved with distinguishing and taking advantage of SQL infusion blemishes and taking over of information base servers. It accompanies an amazing location motor, numerous specialty highlights for a definitive infiltration analyzer and a wide scope of switches enduring from data set fingerprinting, over information getting from the data set, to getting to the hidden record framework and executing orders on the working framework by means of out-of-band associations.

USAGE: sqlmap.py [options]

OPTIONS: https://github.com/sqlmapproject/sqlmap/wiki/Usage

EXAMPLE: sqlmap.py - u "http://www.target.com/vuln.php?id=1" - f - - pennant - - dbs – clients (Run sqlmap against a solitary objective URL)

EXAMPLE: sqlmap.py - g "inurl:\".php?id=1\"" (test and infuse on GET boundaries dependent on aftereffects of your Google doofus)

EXAMPLE: sqlmap.py - u "http://www.target.com/vuln.php" - - data="id=1" - f - - standard - - dbs - - clients (chase after POST solicitations)

EXAMPLE: sqlmap.py - u "http://192.168.136.131/sqlmap/mysql/fundamental/get_int.php?id=1" \ - - auth-type Basic - - auth-cred "testuser:testpass" (HTTP validation)

EXAMPLE: sqlmap.py - l burp.log - - scope="(www)?\.target\.(com|net|org)" (Filtering focuses from gave intermediary log utilizing customary articulation)

Sqlninja

DESCRIPTION

Sqlninja is an apparatus designated to take advantage of SQL Injection weaknesses on a web application that utilizes Microsoft SQL Server as its back-end. Its fundamental objective is to give a remote access on the weak DB server, even in an exceptionally unfriendly climate. It ought to be utilized by infiltration analyzers to help and computerize the method involved with assuming control over a DB Server when a SQL Injection weakness has been found.

USAGE: arrangement and execution happens through sqlninja.conf; see documentation for additional subtleties

OPTION: http://sqlninja.sourceforge.net/sqlninja-howto.html

EXAMPLE: n/a

Sqlsus

DESCRIPTION

sqlsus is an open source MySQL infusion and takeover device. By means of an order line interface, you can recover the database(s) structure, infuse your own SQL questions (even complex ones), download records from the web waiter, creep the site for writable catalogs, transfer and control an indirect access, clone the database(s), and substantially more... At whatever point pertinent, sqlsus will impersonate a MySQL console yield.

More information: http://sqlsus.sourceforge.net/

USAGE: Generate a design document with sqlsus - - genconf my.cfg, read the remarks and adjust it to mirror your objective. Dispatch sqlsus, with your design as a boundary sqlsus my.cfg, you will get a shell.

OPTIONS: http://sqlsus.sourceforge.net/documentation.html

EXAMPLE: n/a, actually look at documentation

tnscmd10g

DESCRIPTION

 tnscmd can be utilized to talk, on an extremely basic level, with Oracle's TNS audience. The TNS audience (also known as tnslsnr) is the organization interface between a data set customer and the information base server. tnslsnr tunes in on port 1521/tcp.

The tnslnsr keeps a straightforward log of action - - simple in that it doesn't log a ton of helpful data. For example, it doesn't log the IP address of TNS meetings. On the off chance that you start a TCP meeting to the tnslsnr port, you won't gain a lot of ground; it will not give a flag and will presumably disengage in case you type something. Relax; this is the thing that tnscmd is for. tnscmd essentially converses with the tnslsnr interaction. tnslsnr will react to specific orders like ping (an application-level no-operation), variant (dumps adaptation data about Oracle), status (dumps status about the audience and information base occasions), and administrations (dumps data about the running administrations.) Commands are evidently case-obtuse.

More data: http://www.jammed.com/~jwa/hacks/security/tnscmd/tnscmd-doc.html

USAGE: tnscmd [command] - h hostname where 'order' is something like ping, adaptation, status, and so on (default is ping)

EXAMPLE: tnscmd - h oraclebox.example.com - p 1521 – indent (ping this host to check whether it is really running tnslsnr)

EXAMPLE: tnscmd [badcommand] - h oraclebox.example.com ("Bad" TNS bundles can crash the audience, whether or not or not the DBA has set a secret phrase. badcommand can be any of: trc_file trc_level use_plugandplay trc_directory snmp_visible log_file log_status log_directory)

CHAPTER FIVE

FUZZING TOOLS

• bed

• fuzz_ip6

• ohrwurm

• powerfuzzer

• sfuzz

• siparmyknife

• spike-generic_chunked

• spike-generic_listen_tcp

• spike-generic_send_tcp

• spike-generic_listen_upd

bed

DESCRIPTION

BED (also known as Bruteforce Exploit Detector) is a plain-text convention fuzzer that checks programming for normal weaknesses like support floods, design string bugs, whole number floods, and so on The apparatus as of now upholds following conventions: finger, ftp, http, imap, irc, lpd, pjl, pop, smtp

USAGE: ./bed.pl – s<Plugin> [options]

OPTIONS:

-s <Plugin>Plugin to utilize (compulsory). Substantial modules are: FTP/SMTP/POP/HTTP/IRC/IMAP/PJL/LPD/FINGER/SOCKS4/SOCKS5 Use "./bed.pl - s " to acquire the boundaries you want for the module.

-t<target> Host to check (default: localhost)

-p<port> Port to interface with (default: standard port)

-o<timeout> seconds to stand by after each test (default: 2 seconds)

EXAMPLE: ./bed.pl - s HTTP - t 192.168.100.16 - p 80

fuzz_ip6

DESCRIPTION

thc-ipv6 - THC-IPV6-ATTACK-TOOLKIT - just run the apparatuses without choices and they will give you help and show the order line choices.

fuzz_ip6 - fluffs an icmp6 parcel.

TIP DETECTION:

Most instruments can undoubtedly be distinguished by an IDS or particular recognition programming. This is done deliberately to make maverick use identification simpler. The devices either determine a decent bundle signature, or conventionally sniff for parcels (for example accordingly likewise offering an explanation to icmp6 neighbor requesting which are shipped off a non-existing macintosh, and are in this way extremely simple to identify). Assuming that you don't need this, change the code.

USAGE: fuzz_ip6 [-x] [-t number | - T number] [-p number] [-IFSDHRJ] [-X|-1|-2|-3|-4|-5|-6|-7|-8|-9|-0 port] interface unicast-or-multicast-address [address-in-information pkt]

OPTIONS: https://github.com/mmoya/thc-ipv6/mass/ace/fuzz_ip6.c

EXAMPLE: n/a

ohrwurm

DESCRIPTION

ohrwurm is a little and basic RTP fuzzer, it has been tried it on few SIP telephones, not a solitary one of them withstood the fluffing.

Highlights:

• peruses SIP messages to get data of the RTP port numbers

• perusing SIP can be overlooked by giving the RTP port numbers, so any RTP traffic can be fluffed

• RTCP traffic can be stifled to stay away from that codecs find out about the "uproarious line"

• extraordinary consideration is taken to break RTP dealing with itself

• the RTP payload is fluffed with a consistent BER

• the BER is configurable

• requires arpspoof from dsniff to do the MITM assault

• requires the two telephones to be in an exchanged LAN (GW activity just works somewhat)

USAGE: n/a

EXAMPLE: n/a

Powerfuzzer

DESCRIPTION

Powerfuzzer is an exceptionally robotized and completely adaptable web fuzzer (HTTP convention based application fuzzer) in view of numerous other Open Source fuzzers accessible and data accumulated from various security assets and sites. It was intended to be easy to understand, current, viable and working. More data: http://www.powerfuzzer.com/#news

At present, it is fit for recognizing these issues:

- Cross Site Scripting (XSS)

- Infusions (SQL, LDAP, code, orders, and XPATH)

- CRLF

- HTTP 500 situations with (characteristic of a potential misconfiguration/security defect incl. cradle flood)

USAGE: n/a; GUI apparatus

EXAMPLE: n/a; GUI instrument

Sfuzz

DESCRIPTION

basic fuzzer is by and large what it seems like - a straightforward fuzzer. try not to botch straightforward with an absence of fuzz capacity. this fuzzer has two organization methods of activity, a result mode for creating order line fuzzing scripts, just as taking fuzzing strings from literals and building strings from arrangements.

basic fuzz is worked to fill a need - the requirement for a rapidly configurable discovery testing utility that doesn't need cozy information on the internal activities of C or require specific programming rigs. The point is to give a basic interface, clear sources of info/results, and reusability.

USAGE: sfuzz [output modes] [logging] [config file] [network host] [variables] [misc]

USAGE: sfuzz – h (for help) or read documentation by following the connection beneath

OPTIONS: https://github.com/orgcandman/Simple-Fuzzer

EXAMPLE: sfuzz - T - f/tmp/myfirst.cfg - S foo.com - p 80

Siparmyknife

DESCRIPTION

SIP Army Knife is a fuzzer that looks for cross site prearranging, SQL infusion, log infusion, design strings, cradle floods, and then some. sipsak − a utility for different tests on taste servers and client specialists.

USAGE:  sipsak [-dFGhiILnNMRSTUVvwz] [-a PASSWORD ] [-b NUMBER ] [-c SIPURI ] [-C SIPURI ] [-D NUMBER ] [-e NUMBER ] [-E STRING ] [-f FILE ] [-g STRING ] [-HHOSTNAME ] [-l PORT ] [-m NUMBER ] [-o NUMBER ] [-p HOSTNAME ] [-P NUMBER ] [-q REGEXP ] [-r PORT ] [-t NUMBER ] [-u STRING ] [-W NUMBER ] [-xNUMBER ] - s SIPURI OPTIONS http://sipsak.org/man-page.html

EXAMPLE: sipsak - vv - s sip:nobody@foo.bar (Send an OPTIONS solicitation to nobody@foo.bar and show got answers)

EXAMPLE:  sipsak - T - s taste nobody@foo.bar (Trace the SIP way to nobody@foo.bar)

EXAMPLE:  sipsak - U - C sip:me@home - x 3600 - a secret phrase - s sip:myself@company (Insert a sending contact for myself at work to me at home for one hour and confirmed with secret key whenever required)

EXAMPLE:  sipsak - I - C vacant - a secret key - s sip:myself@work (Query the presently enlisted ties for myself at work and validate with secret key whenever required)

EXAMPLE:  sipsak - M - v - s sip:colleaue@work - B "Noon!" (Send the text "Noon!" to the associate and show result)

spike-generic_chunked

DESCRIPTION

At the point when you want to break down another organization convention for support floods or comparable shortcomings, the SPIKE is the apparatus of decision for experts. While it requires a solid information on C to utilize, it produces results top notch in the field. It gives you the likelihood to join his APIs inside the C code or essentially utilizing some pre-fabricated instruments which cycles scripts made utilizing the SPIKE's natives.

More data: http://resources.infosecinstitute.com/introduction to-fluffing/

More data: http://resources.infosecinstitute.com/fuzzer-mechanization with-spike/

USAGE: n/a

EXAMPLE: n/a

spike-generic_listen_tcp

DESCRIPTION

At the point when you really want to break down another organization convention for support floods or comparative shortcomings, the SPIKE is the apparatus of decision for experts. While it requires a solid information on C to utilize, it produces results top notch in the field. It gives you the likelihood to consolidate his APIs inside the C code or basically utilizing some pre-fabricated apparatuses which cycles scripts made utilizing the SPIKE's natives.

More data: http://resources.infosecinstitute.com/introduction to-fluffing/

More data: http://resources.infosecinstitute.com/fuzzer-mechanization with-spike/

USAGE: n/a

EXAMPLE: n/a

spike-generic_send_tcp

DESCRIPTION

At the point when you really want to investigate another organization convention for support floods or comparable shortcomings, the SPIKE is the apparatus of decision for experts. While it requires a solid information on C to utilize, it produces results best in class in the field. It gives you the likelihood to consolidate his APIs inside the C code or just utilizing some pre-constructed apparatuses which cycles scripts made utilizing the SPIKE's natives.

More data: http://resources.infosecinstitute.com/introduction to-fluffing/

More data: http://resources.infosecinstitute.com/fuzzer-mechanization with-spike/

USAGE: n/a

EXAMPLE: n/a

spike-generic_listen_upd

DESCRIPTION

At the point when you really want to dissect another organization convention for cushion floods or comparable shortcomings, the SPIKE is the apparatus of decision for experts. While it requires a solid information on C to utilize, it produces results best in class in the field. It gives you the likelihood to fuse his APIs inside the C code or essentially utilizing some pre-assembled instruments which cycles scripts made utilizing the SPIKE's natives.

More data: http://resources.infosecinstitute.com/introduction to-fluffing/

More data: http://resources.infosecinstitute.com/fuzzer-computerization with-spike/

USAGE: n/a

EXAMPLE: n/a

CHAPTER SIX

MISC SCANNERS

• lynis

• nikto

• nmap

• unix-privesc-check

lynis

DESCRIPTION

Lynis is an evaluating apparatus for Unix (subject matter experts). It filters the framework and accessible programming, to distinguish security issues. Next to security related data it will likewise filter for general framework data, introduced bundles and setup botches.

This product points in helping computerized inspecting, programming patch the executives, weakness and malware examining of Unix based frameworks. It very well may be run without earlier establishment, so consideration on read just capacity is no issue (USB stick, album/dvd).

Lynis helps examiners in performing Basel II, GLBA, HIPAA, PCI DSS and SOX (Sarbanes-Oxley) consistence reviews.

USAGE: ./lynis [options] [cronjob]

OPTIONS: http://www.rootkit.nl/records/lynis-documentation.html

EXAMPLE: ./lynis - c - - examiner "computerized" – cronjob

Nikto

DESCRIPTION

Nikto is web server scanner which performs complete tests against web servers for quite a long time, including north of 6500 possibly risky documents/CGIs, checks for obsolete variants of more than 1250 servers, and adaptation explicit issues on north of 270 servers. It additionally checks for server arrangement things, for example, the presence of different file records, HTTP server choices, and will endeavor to distinguish introduced web servers and programming. Check things and modules are often refreshed and can be naturally refreshed.

USAGE: nikto.pl [host] [target] [options]

OPTIONS:  [http://cirt.net/nikto2-docs/options.html](http://cirt.net/nikto2-docs/options.html)

EXAMPLE: nikto.pl - h 192.168.0.1 - T 58 (check tuning)

EXAMPLE: nmap - p80 192.168.0.0/24 - oG - | nikto.pl - h - (Multiple Host Testing)

EXAMPLE: nikto.pl - h 192.168.0.1 - p 80,88,443 (Multiple Port Testing)

EXAMPLE: nikto.pl - h https://192.168.0.1:443/(fundamental testing and filtering utilizing a full URL sentence structure)

EXAMPLE: nikto.pl - h 192.168.0.1 - p 443 (actually taking a look at explicit port)

Nmap

DESCRIPTION

nmap is positively THE scanner to know. Because of its various boundaries, it is a swiss armed force blade to all circumstances where network recognizable proof is required. It empowers in addition to other things to list network has and filter their ports.

USAGE: ./nmap [Scan Type(s)] [Options] {target specification}

EXAMPLE: ./nmap - sP 192.168.100.0/24 (Lists has on an organization)

EXAMPLE: ./nmap - sS - sV 192.168.100.18 (Scans a host. This model uses a TCP/SYN output and attempts to recognize introduced administrations)

unix-privesc-check

DESCRIPTION

Unix-privesc-checker is a content that sudden spikes in demand for Unix frameworks. It attempts to find misconfigurations that could permit nearby unprivileged clients to raise advantages to different clients or to get to neighborhood applications (e.g., information bases). It's expected to be controlled by security reviewers and infiltration analyzers against frameworks they have been locked in to evaluate, and furthermore by framework chairmen who need to check for "self-evident" misconfigurations. It can even be run as a cron work so you can check routinely for misconfigurations that may be presented.

More data:  [https://code.google.com/p/unix-privesc-check/wiki/Checks](https://code.google.com/p/unix-privesc-check/wiki/Checks)

and [http://pentestmonkey.net/apparatuses/unixprivesc-check](http://pentestmonkey.net/apparatuses/unixprivesc-check)

USAGE: unix-privesc-check { standard | point by point }

EXAMPLE: unix-privesc-actually look at standard

CHAPTER SEVEN

OPEN SOURCE ASSESSMENT

• casefile

• maltego

Casefile

DESCRIPTION

CaseFile enables you to rapidly add, connect and dissect information having the equivalent diagramming adaptability and execution as Maltego without the utilization of changes. Consolidating Maltego's phenomenal chart and connection investigation this device takes into account investigators to analyze interfaces between physically added information to mind map your data.

• CaseFile is a visual knowledge application that can be utilized to decide the connections and certifiable connections between many various sorts of data.

• It enables you to rapidly see second, third and n-th request connections and find interfaces in any case undiscoverable with different kinds of insight apparatuses.

• CaseFile comes packaged with various sorts of substances that are ordinarily utilized in examinations permitting you to act rapidly and proficiently. CaseFile likewise can add custom substance types permitting you to stretch out the item to your own informational indexes.

USAGE: n/a; GUI device

EXAMPLE: n/a, GUI apparatus

Maltego

DESCRIPTION

Maltego is a novel stage created to convey an unmistakable danger picture to the climate that an association claims and works. Maltego can find, total and picture this data. Maltego is a program that can be utilized to decide the connections and true connections between individuals, gatherings of individuals (informal communities), organizations, associations, sites, phrases, affiliations, archives and records, web foundation (spaces, DNS names, netblocks, IP addresses).

USAGE: n/a, GUI instrument

EXAMPLE: n/a, GUI instrument

CHAPTER EIGHT

OPEN-VAS

• penvas-gsd

• openvas-arrangement

openvas-gsd

DESCRIPTION

The Open Vulnerability Assessment System (OpenVAS) is a structure of a few administrations and instruments. The center of this SSL-got administration situated design is the OpenVAS Scanner. The scanner proficiently executes the genuine Network Vulnerability Tests (NVTs) which are presented with day by day refreshes through the OpenVAS NVT Feed or by means of a business feed administration.

The Greenbone Security Desktop (GSD) is a Qt-based work area customer for OMP.

More data: http://www.backtrack-linux.org/wiki/index.php/OpenVas

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI device

openvas-arrangement

DESCRIPTION

The Open Vulnerability Assessment System (OpenVAS) is a structure of a few administrations and devices. The center of this SSL-got administration arranged design is the OpenVAS Scanner. The scanner effectively executes the real Network Vulnerability Tests (NVTs) which are presented with day by day refreshes by means of the OpenVAS NVT Feed or through a business feed administration.

More information: http://www.backtrack-linux.org/wiki/index.php/OpenVas

USAGE: n/a; GUI device

EXAMPLE: n/a GUI device

CHAPTER NINE

WEB APPLICATIONS: CMS IDENTIFACTION

• blindelephant

• plecost

• wpscan

Blindelephant

DESCRIPTION

The BlindElephant Web Application Fingerprinter endeavors to find the variant of a (known) web application by contrasting static records at known areas against precomputed hashes for forms of those documents in the accessible deliveries in general. The procedure is quick, low-data transmission, non-obtrusive, nonexclusive, and profoundly automatable. BlindElephant can be utilized straightforwardly as an apparatus on the order line, or as a library to give fingerprinting usefulness to another program.

USAGE: BlindElephant.py [options] url appName

OPTIONS:

-h, - - help show this help message and exit

-p PLUGINNAME, - - pluginName=PLUGINNAME Fingerprint form of module (ought to apply to web application given in appname)

-s, - -Skip Skip fingerprinting webpp, simply unique mark module

-n NUMPROBES, - - numProbes=NUMPROBES Number of records to get (more might expand exactness). Default: 15

-w, - - winnow If more than one form are returned, use winnowing to endeavor to limit it down (up to numProbes extra demands)

-l, - - List list upheld webapps and modules

EXAMPLE: BlindElephant.py http://laws.qualys.com movabletype

plecost

DESCRIPTION

Wordpress finger printer device, plecost look and recovers data about the module variants introduced in Wordpress frameworks. It can investigate a solitary URL or play out an examination dependent on the outcomes recorded by Google. Moreover shows CVE code related with each module, if exists. Plecost recovers the data contained on Web destinations upheld by Wordpress, and furthermore permits a pursuit on the outcomes ordered by Google.

USAGE: ./plecost.py [options] [ URL | [-l num] - G]

OPTIONS: [https://code.google.com/p/plecost/](https://code.google.com/p/plecost/)

EXAMPLE: plecost - R plugins.txt - n 5 (Reload initial 5 modules list)

EXAMPLE: plecost - n 5 - G - I plugins.txt (Search weak locales for initial 5 modules)

EXAMPLE: plecost - I plugin_list.txt - s 12 - M 30 - t 20 - o results.txt www.example.com (Search modules with 20 strings, rest time somewhere in the range of 12 and 30 seconds for www.example.com)

wpscan

DESCRIPTION

WPScan is a discovery WordPress weakness scanner.

USAGE: wpscan.rb – url [target ip] [options]

OPTIONS: http://wpscan.org/

EXAMPLE: ruby wpscan.rb - - url www.example.com (Do 'non-meddling' checks...)

EXAMPLE: ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - strings 50 (Do wordlist secret phrase savage power on counted clients utilizing 50 threads...)

EXAMPLE:  ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - username administrator (Do wordlist secret phrase savage power on the 'administrator' username only...)

EXAMPLE:  ruby wpscan.rb - - url www.example.com - - count p (Enumerate introduced modules... )

EXAMPLE:  ruby wpscan.rb - - url www.example.com – count (Run all identification tools...)

CHAPTER TEN

DATA SET EXPLOITATION

• bbqsql

• sqlninja

• sqlsus

Bbqsql

DESCRIPTION

 Blind SQL infusion can be an aggravation to take advantage of. At the point when the accessible apparatuses work they function admirably, yet when they don't you need to compose something custom. This is tedious and drawn-out. BBQSQL can assist you with resolving those issues.

BBQSQL is a visually impaired SQL infusion structure written in Python. It is very valuable while assaulting precarious SQL infusion weaknesses. BBQSQL is likewise a self-loader apparatus, permitting a considerable amount of customization for those difficult to trigger SQL infusion discoveries. The instrument is worked to be data set rationalist and is incredibly flexible. It likewise has an instinctive UI to make setting up assaults a lot more straightforward. Python gevent is additionally carried out, making BBQSQL very quick.

USAGE: n/a, choice determination/arrangement

OPTIONS: https://github.com/Neohapsis/bbqsql

EXAMPLE: n/a

sqlninja

DESCRIPTION

Sqlninja is an apparatus designated to take advantage of SQL Injection weaknesses on a web application that utilizes Microsoft SQL Server as its back-end. Its fundamental objective is to give a remote access on the weak DB server, even in an exceptionally unfriendly climate. It ought to be utilized by infiltration analyzers to help and mechanize the most common way of assuming control over a DB Server when a SQL Injection weakness has been found.

USAGE:  Configuration and execution happens through sqlninja.conf; see documentation for additional subtleties

OPTIONS: http://sqlninja.sourceforge.net/sqlninja-howto.html

EXAMPLE: n/a

sqlsus

DESCRIPTION

sqlsus is an open source MySQL infusion and takeover instrument. Through an order line interface, you can recover the database(s) structure, infuse your own SQL questions (even complex ones), download documents from the web waiter, creep the site for writable registries, transfer and control a secondary passage, clone the database(s), and substantially more... At whatever point important, sqlsus will impersonate a MySQL console yield.

More data: http://sqlsus.sourceforge.net/

USAGE: Generate an arrangement record with sqlsus - - genconf my.cfg, read the remarks and adjust it to mirror your objective. Dispatch sqlsus, with your setup as a boundary sqlsus my.cfg, you will get a shell.

OPTIONS: http://sqlsus.sourceforge.net/documentation.html

EXAMPLE: n/a, really look at documentation

CHAPTER ELEVEN

IDS/IPS IDENTIFACATION

• ua-tester

ua-tester

DESCRIPTION

UATester is a python script that demands a page from a webserver with various client specialists. With this content one can rapidly find assuming that various pages exist for various client specialists (for example versatile page, IE advanced page, and so on) This device is intended to naturally check a given URL utilizing a rundown of standard and nonstandard User Agent strings given by the client (1 for each line). The aftereffects of these checks are then answered to the client for additional manual examination where required.

USAGE: ./uatester.py – u<url> [options]

OPTIONS: http://packetstormsecurity.com/records/94305/UA-Tester-User-Agent-Tester-1.03.html

EXAMPLE: ./UATester.py - u www.example.com - f ./useragentlist.txt - v

EXAMPLE:  ./UATester.py - u https://www.wordpress.com

EXAMPLE:  ./UATester.py - u http://www.defaultserver.com - v - - investigate

EXAMPLE:  ./UATester.py - u facebook.com - v - d MDBX EXAMPLE ./UATester.py - u https://www.google.com - s "MySpecialUserAgent"\n'''

CHAPTER TWELVE

WEB APPLICATION FUZZERS

• burpsuite

• powerfuzzer

• webscarab

• webslayer

• websploit

• wfuzz

• xsser

• zaproxy

Burpsuite

DESCRIPTION

Burp Suite is an incorporated stage for performing security testing of web applications. Its different apparatuses work consistently together to help the whole testing process, from beginning planning and examination of an application's assault surface, through to finding and taking advantage of safety weaknesses.

Burp Suite contains the accompanying key parts:

• A capturing Proxy, which allows you to examine and change traffic between your program and the objective application.

• An application-mindful Spider, for slithering substance and usefulness.

• A high level web application Scanner, for computerizing the recognition of various sorts of weakness.

• An Intruder instrument, for performing amazing altered assaults to find and take advantage of surprising weaknesses.

• A Repeater instrument, for controlling and resending individual solicitations.

• A Sequencer device, for testing the arbitrariness of meeting tokens.

• The capacity to save your work and resume working later.

• Extensibility, permitting you to handily compose your own modules, to perform complex and exceptionally modified assignments inside Burp.

More information:  [http://portswigger.net/burp/](http://portswigger.net/burp/)

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

Powerfuzzer

DESCRIPTION

Powerfuzzer is a profoundly computerized and completely adaptable web fuzzer (HTTP convention based application fuzzer) in view of numerous other Open Source fuzzers accessible and data assembled from various security assets and sites. It was intended to be easy to use, present day, viable and working.

More information: http://www.powerfuzzer.com/#news

Presently, it is equipped for recognizing these issues:

- Cross Site Scripting (XSS)

- Infusions (SQL, LDAP, code, orders, and XPATH)

- CRLF

- HTTP 500 situations with (demonstrative of a potential misconfiguration/security blemish incl. cushion flood)

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI apparatus

Webscarab

DESCRIPTION

WebScarab is a structure for investigating applications that convey utilizing the HTTP and HTTPS conventions. It is written in Java, and is along these lines convenient to numerous stages. WebScarab has a few methods of activity, executed by various modules. In its most normal utilization, WebScarab works as a catching intermediary, permitting the administrator to survey and change demands made by the program before they are shipped off the server, and to audit and alter reactions got back from the server before they are gotten by the program. WebScarab can capture both HTTP and HTTPS  correspondence. The administrator can likewise survey the discussions (solicitations and reactions) that have gone through WebScarab.

More information: https://www.owasp.org/index.php/WebScarab_Getting_Started

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI apparatus

Webslayer

DESCRIPTION

WebSlayer is an apparatus intended for animal driving Web Applications, it tends to be utilized to find not connected assets (indexes, servlets, scripts, and so on), savage power GET and POST boundaries, beast power structures boundaries (User/Password), fluffing, and so forth The instrument has an amazing payload generator and a simple and adaptable outcomes analyzer.

More data: [https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project](https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project)

USAGE: n/a; GUI instrument

EXAMPLE:n/a; GUI instrument

Websploit

DESCRIPTION

WebSploit is utilized to sweep and investigation far off framework to track down different sort of weaknesses. This apparatus is exceptionally amazing and upholds numerous weaknesses. WebSploit is utilized for: Social Engineering Works, Scan, Crawler and Web Analysis, Automatic Exploiter and Support Network Attacks. Highlights:

• Autopwn - Used From Metasploit For Scan and Exploit Target Service

• wmap - Scan,Crawler Target Used From Metasploit wmap module

• design infector - infuse turn around and tie payload into record design

• phpmyadmin Scanner

• LFI Bypasser

• Apache Users Scanner

• Dir Bruter

• administrator locater

• MLITM Attack - Man Left In The Middle, XSS Phishing Attacks

• MITM - Man In The Middle Attack

• Java Applet Attack

• MFOD Attack Vector

• USB Infection Attack

• ARP Dos Attack

• Web Killer Attack

• Counterfeit Update Attack

• Counterfeit Access point Attack

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI apparatus

Wfuzz

DESCRIPTION

Wfuzz is an apparatus intended for bruteforcing Web Applications, it very well may be utilized for finding assets not connected (catalogs, servlets, scripts, and so on), bruteforce GET and POST boundaries for really taking a look at changed sort of infusions (SQL, XSS, LDAP,etc), bruteforce Forms boundaries (User/Password), Fuzzing,etc.

More information: https://code.google.com/p/wfuzz/wiki/Howto

USAGE: wfuzz.py [options] [file] [config] [target ip]

EXAMPLE: wfuzz.py - c - z document, wordlists/commons.txt - - hc 404 - R 2 http://www.mysite.com/FUZZ (Example of way disclosure, utilizing a recursive degree of 2)

EXAMPLE: wfuzz.py - z file,wordlists/http_methods.txt - X http://testphp.vulnweb.com/(HTTP strategy checking model)

EXAMPLE: wfuzz.py - z list,TRACE - X http://testphp.vulnweb.com/(Scanning for TRACE strategy utilizing a rundown payload)

EXAMPLE: wfuzz.py - c - z file,wordlists/methods.txt - - hc 404 - v - - follow http://www.mysite.com/FUZZ (Bruteforce following HTTP diverts)

EXAMPLE: wfuzz.py - c - z file,wordlists/commons.txt - - hc 404 - I http://www.mysite.com/FUZZ (Bruteforce utilizing HEAD HTTP strategy)

EXAMPLE: wfuzz.py - z list,http://mysite.com - z list,dir-dir2-dir3 FUZZ/FUZ2Z (Bruteforce utilizing URL as payload and a rundown of catalogs.)

Xsser

DESCRIPTION

Cross Site "Scripter" (also known as XSSer) is a programmed - system to distinguish, exploit and report XSS weaknesses in online applications. It contains a few choices to attempt to sidestep specific channels, and different extraordinary strategies of code infusion.

USAGE: xsser [OPTIONS] [-u |-I |-d ] [-g |-p |-c ] [Request(s)] [Vector(s)] [Bypasser(s)] [Technique(s)] [Final Injection(s)]

OPTIONS: [http://xsser.sourceforge.net/](http://xsser.sourceforge.net/)

EXAMPLE: python xsser.py - u http://host.com (Simple infusion from URL)

EXAMPLE:  python xsser.py - I "file.txt" - - intermediary "http://127.0.0.1:8118" - - referer "666.666.666.666" (Simple infusion from File, with peak intermediary and parodying HTTP Referer headers)

EXAMPLE:  python xsser.py - u "http://host.com" - p index.php?target=search&subtarget=top&searchstring=" – s (Simple infusion from URL, utilizing POST, with insights results)

EXAMPLE:  python xsser.py - u "host.com" – hash (Send a pre-actually taking a look at hash to check whether target will create - bogus positive-results)

Zaproxy

DESCRIPTION

The OWASP Zed Attack Proxy (ZAP) is a simple to utilize coordinated entrance testing instrument for tracking down weaknesses in web applications. It is intended to be utilized by individuals with a wide scope of safety experience and as such is great for engineers and practical analyzers who are new to infiltration testing just as being a valuable expansion to an accomplished pen analyzers' tool stash.

More data: https://code.google.com/p/zaproxy/

USAGE:n/a; GUI device

EXAMPLE: n/a; GUI apparatus

CHAPTER THIRTEEN

WEB APPLICATION PROXIES

• burpsuite

• paros

• proxystrike

• vega

• webscarab

• zaproxy

Burpsuite

DESCRIPTION

Burp Suite is a coordinated stage for performing security testing of web applications. Its different devices work flawlessly together to help the whole testing process, from introductory planning and examination of an application's assault surface, through to finding and taking advantage of safety weaknesses.

Burp Suite contains the accompanying key parts:

• A blocking Proxy, which allows you to review and change traffic between your program and the objective application.

• An application-mindful Spider, for creeping content and usefulness.

• A high level web application Scanner, for mechanizing the identification of various sorts of weakness.

• An Intruder apparatus, for performing amazing modified assaults to find and take advantage of uncommon weaknesses.

• A Repeater apparatus, for controlling and resending individual solicitations.

• A Sequencer device, for testing the arbitrariness of meeting tokens.

• The capacity to save your work and resume working later.

• Extensibility, permitting you to effortlessly compose your own modules, to perform complex and profoundly modified assignments inside Burp.

More data:  [http://portswigger.net/burp/](http://portswigger.net/burp/)

USAGE:  n/a; GUI apparatus

EXAMPLE: n/a; GUI device

Paros

DESCRIPTION

Paros is an important testing apparatus for your security and weakness testing. Paros can be utilized to bug/creep your whole site, and afterward execute canned weakness scanner tests. Yet, Paros goes past that, it accompanies an implicit utility that would proxy be able to traffic. This Paros Proxy utility can be utilized to alter or control any http or https traffic on the fly. This makes a portion of the seriously fascinating security sorts of testing. It will assist you with separating possible space's of safety concern and afterward manual endeavor to play out the kind of testing you want.

More data:  [http://www.testingsecurity.com/paros_proxy](http://www.testingsecurity.com/paros_proxy) and [http://www.parosproxy.org/](http://www.parosproxy.org/)

To make it work run ./startserver.sh and design the program you are utilizing so the intermediary utilizes 127.0.01: 8080 for http and https.

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI device

Proxystrike

DESCRIPTION

ProxyStrike is a functioning Web Application Proxy. It's a device intended to track down weaknesses while perusing an application. It was made on the grounds that the issues we looked in the pentests of web applications that relies vigorously upon Javascript, relatively few web scanners did it great in this stage, so we accompanied this intermediary. At this moment it has accessible SQL infusion and XSS modules. Both modules are intended to get however many weaknesses as we can, it's that why the SQL Injection module is a Python port of the incomparable DarkRaver "Sqlibf". The interaction is exceptionally straightforward, ProxyStrike runs like an intermediary tuning in port 8008 naturally, so you need to peruse the ideal site setting your program to utilize ProxyStrike as an intermediary, and  ProxyStrike will investigate every one of the boundaries in foundation mode. For the client is a latent intermediary since you won't see any disparate in the conduct of the application, yet behind the scenes is exceptionally dynamic.

More information:  [https://code.google.com/p/proxystrike](https://code.google.com/p/proxystrike)

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI instrument

Vega

DESCRIPTION

Vega is an open source stage to test the security of web applications. Vega can assist you with finding and approve SQL Injections, Cross-Site Scripting (XSS), coincidentally uncovered delicate data, and different weaknesses.

Highlights:

• Computerized Crawler and Vulnerability Scanner

• Steady UI

• Site Crawler

• Catching Proxy

• SSL MITM

• Content Analysis

• Extensibility through a Powerful Javascript Module API

• Adaptable cautions

• Information base and Shared Data Model

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI instrument

webscarab

DESCRIPTON

WebScarab is a system for examining applications that impart utilizing the HTTP and HTTPS conventions. It is written in Java, and is accordingly convenient to numerous stages. WebScarab has a few methods of activity, carried out by various modules. In its most normal utilization, WebScarab works as a capturing intermediary, permitting the administrator to survey and alter demands made by the program before they are shipped off the server, and to audit and change reactions got back from the server before they are gotten by the program. WebScarab can catch both HTTP and HTTPS correspondence. The administrator can likewise survey the discussions (solicitations and reactions) that have gone through WebScarab.

More data:  [https://www.owasp.org/index.php/WebScarab_Getting_Started](https://www.owasp.org/index.php/WebScarab_Getting_Started)

USAGE:  n/a; GUI apparatus

EXAMPLE: n/a; GUI device

Zaproxy

DESCRIPTION

The OWASP Zed Attack Proxy (ZAP) is a simple to utilize coordinated infiltration testing device for tracking down weaknesses in web applications. It is intended to be utilized by individuals with a wide scope of safety experience and as such is great for designers and utilitarian analyzers who are new to infiltration testing just as being a helpful expansion to an accomplished pen analyzers' tool stash.

More data:  [https://code.google.com/p/zaproxy/](https://code.google.com/p/zaproxy/)

USAGE: n/a; GUI apparatus

EXAMPLE: n/a; GUI instrument

CHAPTER FOURTEEN

WEB CRAWLERS

• apache-clients

• burpsuite

• cutycapt

• dirb

• dirbuster

• vega

• webscarab

• webslayer

• zaproxy

apache-users

DESCRPTION

apache-users permits looking through server username catalog (if use from apache webserver)/permits filtering registry of apache clients. This module is important for the WebSploit Toolkit.

USAGE: n/a

EXAMPLE: n/a

Burpsuite

DESCRIPTION

Burp Suite is an incorporated stage for performing security testing of web applications. Its different apparatuses work flawlessly together to help the whole testing process, from beginning planning and examination of an application's assault surface, through to finding and taking advantage of safety weaknesses. Burp Suite contains the accompanying key parts:

• A capturing Proxy, which allows you to assess and adjust traffic between your program and the objective application.

• An application-mindful Spider, for slithering substance and usefulness.

• A high level web application Scanner, for robotizing the discovery of various sorts of weakness.

• An Intruder device, for performing incredible altered assaults to find and take advantage of strange weaknesses.

• A Repeater apparatus, for controlling and resending individual solicitations.

• A Sequencer device, for testing the irregularity of meeting tokens.

• The capacity to save your work and resume working later.

• Extensibility, permitting you to effortlessly compose your own modules, to perform complex and exceptionally tweaked undertakings inside Burp.

More information:  [http://portswigger.net/burp/](http://portswigger.net/burp/)

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

Cutycapt

DESCRIPTION

CutyCapt is a little cross-stage order line utility to catch WebKit's delivering of a page into an assortment of vector and bitmap designs, including SVG, PDF, PS, PNG, JPEG, TIFF, GIF, and BMP.

USAGE: CutyCapt - - url=<target ip> - - out=<output file>.<extension>

OPTIONS:  [http://cutycapt.sourceforge.net/](http://cutycapt.sourceforge.net/)

EXAMPLE: CutyCapt - - url=http://www.example.org/ - - out=localfile.png

TIP:

Utilizing CutyCapt without X server You can't utilize CutyCapt without a X server, yet you can utilize for example Xvfb as light-weight server assuming you are not running an intuitive graphical work area climate.

For instance, you could utilize:

% xvfb-run - - server-args="- screen 0, 1024x768x24" ./CutyCapt - - url=... - - out=...

Dirb

DESCRIPTION

DIRB is a Web Content Scanner. It searches for existing (as well as covered up) Web Objects. It essentially works by dispatching a word reference based assault against a web server and investigating the reaction. DIRB accompanies a bunch of preconfigured assault wordlists for simple use however you can utilize your custom wordlists. Additionally DIRB once in a while can be utilized as an exemplary CGI scanner, yet recollect – it is a substance scanner not a weakness scanner.

More data:  [http://dirb.sourceforge.net/faq.txt](http://dirb.sourceforge.net/faq.txt)

USAGE: dirb <url><your dict file>

EXAMPLE: ./dirb http://www.site.com/directory1/wordlist.txt

EXAMPLE: ./dirb http://www.site.com/wordlist.txt,dirnamefile.txt

Dirbuster

DESCRIPTION

DirBuster is a multi strung java application intended to beast power catalogs and documents names on web/application servers. Frequently it is the situation when something resembles a web server in a condition of default establishment, when really – it isn't, and has pages and applications concealed inside.

DirBuster endeavors to see as these.

More information: [https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

Vega

DESCRIPTION

Vega is an open source stage to test the security of web applications. Vega can assist you with finding and approve SQL Injections, Cross-Site Scripting (XSS), coincidentally revealed touchy data, and different weaknesses.

Highlights:

• Computerized Crawler and Vulnerability Scanner

• Steady UI

• Site Crawler

• Catching Proxy

• SSL MITM

• Content Analysis

• Extensibility through a Powerful Javascript Module API

• Adaptable alarms

• Information base and Shared Data Model

USAGE: n/a; GUI apparatus

EXAMPLE: n/a; GUI instrument

Webscarab

DESCRIPTION

WebScarab is a system for investigating applications that impart utilizing the HTTP and HTTPS conventions. It is written in Java, and is in this way convenient to numerous stages. WebScarab has a few methods of activity, carried out by various modules. In its most normal use, WebScarab works as a capturing intermediary, permitting the administrator to survey and change demands made by the program before they are shipped off the server, and to audit and alter reactions got back from the server before they are gotten by the program. WebScarab can block both HTTP and HTTPS correspondence. The administrator can likewise audit the discussions (solicitations and reactions) that have gone through WebScarab.

More data:  [https://www.owasp.org/index.php/WebScarab_Getting_Started](https://www.owasp.org/index.php/WebScarab_Getting_Started)

USAGE:  n/a; GUI apparatus

EXAMPLE:  n/a; GUI device

Webslayer

DESCRIPTION

WebSlayer is a device intended for savage compelling Web Applications, it tends to be utilized to find not connected assets (indexes, servlets, scripts, and so forth), beast power GET and POST boundaries, animal power structures boundaries (User/Password), fuzzing, and so on The apparatus has an incredible payload generator and a simple and adaptable outcomes analyzer.

More information: [https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project](https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project)

USAGE: n/a; GUI instrument

EXAMPLE:  n/a; GUI instrument

Zaproxy

DESCRIPTION

The OWASP Zed Attack Proxy (ZAP) is a simple to utilize coordinated entrance testing instrument for tracking down weaknesses in web applications. It is intended to be utilized by individuals with a wide scope of safety experience and as such is great for engineers and practical analyzers who are new to entrance testing just as being a valuable expansion to an accomplished pen analyzers' tool stash.

More information:  [https://code.google.com/p/zaproxy/](https://code.google.com/p/zaproxy/)

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

CHAPTER FIFTEEN

WEB VULNERABILITY SCANNERS

• burpsuite

• zaproxy

• dead body

• davtest

• deblaze

• fimap

• grabber

• joomscan

• nikto

• padbuster

• proxystrike

• skipfish

• sqlmap

• vega

• w3af

• wapiti

• webscarab

• webshag-cli

• webshaggui

• websploit

• wpscan

• xsser

Burpsuite

DESCRIPTION

Burp Suite is a coordinated stage for performing security testing of web applications. Its different instruments work consistently together to help the whole testing process, from beginning planning and examination of an application's assault surface, through to finding and taking advantage of safety weaknesses. Burp Suite contains the accompanying key parts:

• A blocking Proxy, which allows you to review and alter traffic between your program and the objective application.

• An application-mindful Spider, for creeping content and usefulness.

• A high level web application Scanner, for mechanizing the discovery of various kinds of weakness.

• An Intruder apparatus, for performing incredible redid assaults to find and take advantage of strange weaknesses.

• A Repeater apparatus, for controlling and resending individual solicitations.

• A Sequencer instrument, for testing the arbitrariness of meeting tokens.

• The capacity to save your work and resume working later.

• Extensibility, permitting you to effectively compose your own modules, to perform complex and exceptionally altered undertakings inside Burp.

More data:  [http://portswigger.net/burp/](http://portswigger.net/burp/)

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI instrument

Corpse

DESCRIPTION

corpse is an order line WebDAV customer for Unix. It upholds document transfer, download, on-screen show, namespace activities (move/duplicate), assortment creation and erasure, and locking tasks.

USAGE: ./dead body xxx.xxx.xxx.xxx

Use dead body [-et][-V][-h] http://hostname[:port]/way

OPTIONS: [http://linux.die.net/man/1/corpse](http://linux.die.net/man/1/corpse)

EXAMPLE: corpse http://dav.example.com/(Connects to the server myserver.example.com, opening the root assortment)

EXAMPLE:  corpse http://zope.example.com:8022/Users/fred/(Connects to the server zope.example.com utilizing port 8022, opening the assortment "/Users/fred/")

EXAMPLE:  corpse https://secure.example.com/(Connects to a server called secure.example.com utilizing SSL)

TIP: ~/.cadaverrcIndividual client settings that can abrogate corpse defaults.

Davtest

DESCRIPTION

DAVTest tests WebDAV empowered waiters by transferring test executable records, and afterward (alternatively) transferring documents which take into consideration order execution or different activities straightforwardly on the objective. Highlights

• Naturally send exploit records in case code executes

• Programmed randomization of catalog to assist with concealing records utilizing MKCOL

• Send message documents and attempt MOVE to executable name

• Essential and Digest approval

• Programmed tidy up of transferred documents

• Send a discretionary record

USAGE: davtest.pl – url<url> [options]

OPTIONS: [https://code.google.com/p/davtest/wiki/Usage](https://code.google.com/p/davtest/wiki/Usage)

EXAMPLE:  davtest.pl - url http://localhost/davdir (Test document transfers at this area)

EXAMPLE:  davtest.pl - url http://localhost/davdir - sendbd auto (Test document transfers at this area and send secondary passages for any kinds which execute effectively)

EXAMPLE:  davtest.pl - url http://localhost/davdir - auth user:pass - uploadfile secondary passages/perl_cmd.pl - uploadloc perl.pl

(Transfer a record utilizing verification, send the perl_cmd.pl indirect access and call it perl.pl on the server)

Deblaze

DESCRIPTION

deblaze is a distant strategy identification apparatus for flex servers. This device will permit you to perform technique specification and cross examination against streak remoting end focuses. Deblaze gives the accompanying usefulness: Brute Force Service and Method Names, Method Interrogation, Flex  Technology Fingerprinting, Parameter location, Basic boundary fluffing, Proxy AMF demands/reactions, HTML revealing.

USAGE: deblaze [option]

OPTIONS: [http://deblaze-tool.appspot.com/utilization](http://deblaze-tool.appspot.com/utilization)

EXAMPLE: deBlaze.py - u http://192.168.165.132:8080/amfphp/gateway.php - s securityService - m sendEmail - p test@test.com

EXAMPLE:  python2.5 deblaze-0.3.py - P 8080:targetIP:targetPort

EXAMPLE:  python deBlaze.py - u http://192.168.165.132:8080/amfphp/gateway.php - s Discoveryservice - m getServices

EXAMPLE:  python deBlaze.py - u http://192.168.165.132:8400/examples/messagebroker/qosamfpolling - 1 names.txt - m test

Fimap

DESCRIPTION

fimap is a little python device which can find, plan, review, exploit and even google consequently for nearby and remote record incorporation messes with in webapps. fimap ought to be something like sqlmap only for LFI/RFI messes with rather than sql infusion. The objective of fimap is to work on the quality and security of your site. More information: https://code.google.com/p/fimap

USAGE: ./fimap.py [options] OPTIONS https://code.google.com/p/fimap/wiki/FimapHelpPage

EXAMPLE: fimap - u http://localhost/vulnerable.php?inc=index.php

EXAMPLE:  ./fimap.py - u 'http://localhost/test.php?file=bang&id=23' (Scan a solitary URL for FI blunders) EXAMPLE ./fimap.py - m - l '/tmp/urllist.txt' (Scan a rundown of URLS for FI mistakes)

EXAMPLE:  ./fimap.py - g - q 'inurl:include.php' (Scan Google indexed lists for FI mistakes)

EXAMPLE:  ./fimap.py - H - u 'http://localhost' - d 3 - w/tmp/urllist (Harvest all connections of a page with recurse level of 3 and compose the URLs to/tmp/urllist

Grabber

DESCRIPTION

Grabber is a web application scanner. Essentially it recognizes some sort of weaknesses in your site. Grabber is straightforward, not quick but rather compact and truly versatile. This product is intended to check little sites like personals, discussions and so on by no means huge application: it would take too prolonged stretch of time and flood your organization.

Highlights

• Cross-Site Scripting

• SQL Injection (there is likewise an uncommon Blind SQL Injection module)

• Record Inclusion

• Reinforcement records check

• Basic AJAX check (parse each JavaScript and get the URL and attempt to get the boundaries)

• Crossover investigation/Crystal ball testing for PHP application utilizing PHP-SAT

• JavaScript source code analyzer: Evaluation of the quality/accuracy of the JavaScript with JavaScript Lint

• Age of a record [session_id, time(t)] for next details investigation.

USAGE:  grabber.py [options]

OPTIONS:  [http://www.securitytube-tools.net/index.php@title=Grabber.html](http://www.securitytube-tools.net/index.php@title=Grabber.html)

EXAMPLE: read: http://rgaucher.info/beta/grabber/

Joomscan

DESCRIPTION

joomscan recognizes document consideration, SQL infusion, order execution weaknesses of an objective Joomla! site.

Highlights

• Accurate form Probing (the scanner can determine if an objective is running variant 1.5.12)

• Normal Joomla! based web application firewall discovery

• Looking through known weaknesses of Joomla! also its parts

• Answering to Text and HTML yield

• Prompt update capacity by means of scanner or svn

USAGE: joomscan.pl - u - x proxy:port

OPTONS: [https://www.owasp.org/index.php/OWASP_Joomla_Vulnerability_Scanner_Usage](https://www.owasp.org/index.php/OWASP_Joomla_Vulnerability_Scanner_Usage)

EXAMPLE:  joomscan.pl - pv - u victim.com - x localhost:8080

EXAMPLE: joomscan.pl read DOCFILE (where DOCFILE is one of these: changelog,release_note,readme,credits,faq,owasp_project)

Nikto

DESCRIPTION

Nikto is web server scanner which performs extensive tests against web servers for a considerable length of time, including more than 6500 conceivably risky records/CGIs, checks for obsolete variants of north of 1250 servers, and rendition explicit issues on more than 270 servers. It additionally checks for server setup things, for example, the presence of various list records, HTTP server choices, and will endeavor to recognize introduced web servers and programming. Scan items and plugins are frequently updated and can be automatically updated.

USAGE: nikto.pl [host] [target] [options]

OPTIONS: [http://cirt.net/nikto2-docs/options.html](http://cirt.net/nikto2-docs/options.html)

EXAMPLE: nikto.pl - h 192.168.0.1 - T 58 (check tuning)

EXAMPLE:  nmap - p80 192.168.0.0/24 - oG - | nikto.pl - h - (Multiple Host Testing)

EXAMPLE:  nikto.pl - h 192.168.0.1 - p 80,88,443 (Multiple Port Testing)

EXAMPLE:  nikto.pl - h https://192.168.0.1:443/(fundamental testing and checking utilizing a full URL sentence structure)

EXAMPLE:  nikto.pl - h 192.168.0.1 - p 443 (really looking at explicit port)

Padbuster

DESCRIPTION

PadBuster - Automated content for performing Padding Oracle assaults. PadBuster gives the ability to decode self-assertive ciphertext, encode discretionary plaintext, and perform computerized reaction examination to decide if a solicitation is powerless against cushioning prophet assaults. More data and how to utilize: http://blog.gdssecurity.com/labs/2010/9/14/robotized cushioning oracleattacks-with-padbuster.html and http://howtohack.poly.edu/wiki/Padding_Oracle_Attack

USAGE: padBuster.pl<url><encrypted sample><block size><encoding>

EXAMPLE: padBuster.pl http://sampleapp/home.jsp?UID=7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 8 - encoding 2

EXAMPLE:  padBuster.pl http://sampleapp/home.jsp?UID=7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 8 - encoding 2 - plaintext "Scramble TEST"

Proxystrike

DESCRIPTION

ProxyStrike is a functioning Web Application Proxy. It's an instrument intended to track down weaknesses while perusing an application. It was made on the grounds that the issues we looked in the pentests of web applications that relies intensely upon Javascript, relatively few web scanners did it great in this stage, so we accompanied this intermediary. At this moment it has accessible SQL infusion and XSS modules. Both modules are intended to get however many weaknesses as we can, it's that why the SQL Injection module is a Python port of the incomparable DarkRaver "Sqlibf". The interaction is exceptionally basic, ProxyStrike runs like an intermediary tuning in port 8008 naturally, so you need to peruse the ideal site setting your program to utilize ProxyStrike as an intermediary, and ProxyStrike will dissect every one of the boundaries in foundation mode. For the client is a detached intermediary since you won't see any divergent in the conduct of the application, yet behind the scenes is exceptionally dynamic.

More data:  [https://code.google.com/p/proxystrike](https://code.google.com/p/proxystrike)

USAGE: n/a; GUI apparatus

EXAMPLE: n/a; GUI device

Skipfish

DESCRIPTION

Skipfish is a functioning web application security surveillance apparatus. It readies an intuitive sitemap for the designated site via completing a recursive creep and word reference based tests. The subsequent guide is then clarified with the result from various dynamic (yet ideally non-troublesome) security checks. The last report created by the apparatus is intended to fill in as an establishment for proficient web application security evaluations.

USAGE: ./skipfish [options] - o output_dir @/way/to/url_list.txt

OPTIONS: https://code.google.com/p/skipfish/wiki/SkipfishDoc

EXAMPLE: ./skipfish - o output_dir - S existing_dictionary.wl - W new_dict.wl \ http://www.example.com/a few/beginning/path.txt

EXAMPLE:./skipfish - D test2.example.com - o yield dir http://test1.example.com/

EXAMPLE: ./skipfish – D ./skipfish - MEU - S word references/minimal.wl - W new_dict.wl \ - C "AuthCookie=value" - X/logout.aspx - o output_dir \ http://www.example.com/.example.com - o yield dir http://test1.example.com/

Sqlmap

DESCRIPTION

sqlmap is an open source entrance testing instrument that mechanizes the method involved with recognizing and taking advantage of SQL infusion imperfections and taking over of data set servers. It accompanies an incredible discovery motor, numerous specialty highlights for a definitive infiltration analyzer and a wide scope of switches enduring from data set fingerprinting, over information getting from the data set, to getting to the fundamental record framework and executing orders on the working framework through out-of-band associations.

USAGE: sqlmap.py [options]

OPTIONS:  [https://github.com/sqlmapproject/sqlmap/wiki/Usage](https://github.com/sqlmapproject/sqlmap/wiki/Usage)

EXAMPLE: sqlmap.py - u "http://www.target.com/vuln.php?id=1" - f - - standard - - dbs – clients (Run sqlmap against a solitary objective URL)

EXAMPLE: sqlmap.py - g "inurl:\".php?id=1\"" (test and infuse on GET boundaries dependent on consequences of your Google nitwit)

EXAMPLE: sqlmap.py - u "http://www.target.com/vuln.php" - - data="id=1" - f - - standard - - dbs - - clients (chase after POST solicitations)

EXAMPLE: sqlmap.py - u "http://192.168.136.131/sqlmap/mysql/fundamental/get_int.php?id=1" \ - - auth-type Basic - - auth-cred "testuser:testpass" (HTTP validation)

EXAMPLE:  sqlmap.py - l burp.log - - scope="(www)?\.target\.(com|net|org)" (Filtering focuses from gave intermediary log utilizing customary articulation)

Vega

DESCRIPTION

Vega is an open source stage to test the security of web applications. Vega can assist you with finding and approve SQL Injections, Cross-Site Scripting (XSS), coincidentally revealed delicate data, and different weaknesses.

Highlights:

• Robotized Crawler and Vulnerability Scanner

• Predictable UI

• Site Crawler

• Capturing Proxy

• SSL MITM

• Content Analysis

• Extensibility through a Powerful Javascript Module API

• Adaptable cautions

• Information base and Shared Data Model

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI device

w3af

DESCRIPTION

w3af is a Web Application Attack and Audit Framework. The venture gives a weakness scanner and abuse apparatus for Web applications. It gives data about security weaknesses and helps in entrance testing endeavors. w3af recognizes most web application weaknesses utilizing in excess of 130 modules. After ID, weaknesses like (blind) SQL infusions, OS telling, remote record incorporations (PHP), crosssite prearranging (XSS), and risky document transfers, can be taken advantage of to acquire various kinds of admittance to the far off framework. More data: http://w3af.org/

USAGE:  n/a; GUI device

EXAMPLE:   n/a; GUI apparatus

Wapiti

DESCRIPTION

Wapiti permits you to review the security of your web applications. It performs "discovery" filters, for example it doesn't concentrate on the source code of the application yet will examines the site pages of the conveyed webapp, searching for contents and structures where it can infuse information. When it gets this rundown, Wapiti behaves like a fuzzer, infusing payloads to check whether a content is defenseless. Wapiti can recognize the accompanying weaknesses :

• Record Handling Errors (Local and remote incorporate/require, fopen, readfile...)

• Data set Injection (PHP/JSP/ASP SQL Injections and XPath Injections)

• XSS (Cross Site Scripting) Injection

• LDAP Injection

• Order Execution recognition (eval(), framework(), passtru()...)

• CRLF Injection (HTTP Response Splitting, meeting fixation...)

USAGE:  python wapiti.py http://server.com/base/url/[options]

OPTIONS: http://wapiti.sourceforge.net/

EXAMPLE: python wapiti.py http://127.0.0.1/vuln/ - c cookies.txt - x http://127.0.0.1/vuln/index.php?page=logout

Webscarab

DESCRIPTION

WebScarab is a system for investigating applications that convey utilizing the HTTP and HTTPS conventions. It is written in Java, and is accordingly compact to numerous stages. WebScarab has a few methods of activity, carried out by various modules. In its most normal utilization, WebScarab works as a catching intermediary, permitting the administrator to survey and adjust demands made by the program before they are shipped off the server, and to audit and change reactions got back from the server before they are gotten by the program. WebScarab can capture both HTTP and HTTPS correspondence. The administrator can likewise survey the discussions (solicitations and reactions) that have gone through WebScarab.

More information:  [https://www.owasp.org/index.php/WebScarab_Getting_Started](https://www.owasp.org/index.php/WebScarab_Getting_Started)

USAGE:    n/a; GUI instrument

EXAMPLE: n/a; GUI apparatus

webshag-cli

DESCRIPTION

Webshag is a multi-strung, multi-stage web server review instrument. Written in Python, it accumulates regularly valuable functionalities for web server evaluating like site slithering, URL filtering or record fluffing. Webshag can be utilized to examine a web server in HTTP or HTTPS, through an intermediary and utilizing HTTP confirmation (Basic and Digest). Notwithstanding that it proposes imaginative IDS avoidance functionalities pointed toward making connection between's solicitation more muddled (for example utilize an alternate arbitrary per demand HTTP intermediary server). The normal functionalities of the webshag are

• Port Scanning

• Web Crawling

• Url Scanning

• Recovering the rundown of area names

• Record fluffing

More data:  [http://www.scrt.ch/en/assault/downloads/webshag](http://www.scrt.ch/en/assault/downloads/webshag)

USAGE:     ./webshag-cli - m pscan < target-ip >

USAGE:     ./webshag_cli.py - m bug - p 80/< target-ip >

EXAMPLE: ./webshag_cli.py - m uscan - x - o html - f '/root/Desktop/hackingDNA.html'

webshag-gui

DESCRIPTION

Webshag is a multi-strung, multi-stage web server review device. Written in Python, it assembles usually helpful functionalities for web server evaluating like site creeping, URL checking or record fluffing. Webshag can be utilized to check a web server in HTTP or HTTPS, through an intermediary and utilizing HTTP validation (Basic and Digest). Notwithstanding that it proposes imaginative IDS avoidance functionalities pointed toward making relationship between's solicitation more confounded (for example utilize an alternate irregular for every solicitation HTTP intermediary server). The normal functionalities of the webshag are

• Port Scanning

• Web Crawling

• Url Scanning

• Recovering the rundown of area names

• Record fluffing

More data:  [http://www.scrt.ch/en/assault/downloads/webshag](http://www.scrt.ch/en/assault/downloads/webshag)

USAGE: n/a; GUI instrument

EXAMPLE:  n/a; GUI instrument

Websploit

DESCRIPTION

WebSploit is utilized to sweep and examination distant framework to track down different kind of weaknesses. This instrument is exceptionally amazing and upholds various weaknesses. WebSploit is utilized for: Social Engineering Works, Scan, Crawler and Web Analysis, Automatic Exploiter and Support Network Attacks.

Highlights:

• Autopwn - Used From Metasploit For Scan and Exploit Target Service

• wmap - Scan,Crawler Target Used From Metasploit wmap module

• design infector - infuse switch and tie payload into record design

• phpmyadmin Scanner

• LFI Bypasser

• Apache Users Scanner

• Dir Bruter

• administrator locater

• MLITM Attack - Man Left In The Middle, XSS Phishing Attacks

• MITM - Man In The Middle Attack

• Java Applet Attack

• MFOD Attack Vector

• USB Infection Attack

• ARP Dos Attack

• Web Killer Attack

• Counterfeit Update Attack

• Counterfeit Access point Attack

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI instrument

wpscan

DESCRIPTION

WPScan is a discovery WordPress weakness scanner.

USAGE: wpscan.rb – url [target ip] [options]

OPTIONS:  [http://wpscan.org/](http://wpscan.org/)

EXAMPLE: ruby wpscan.rb - - url www.example.com (Do 'non-meddlesome' checks...)

EXAMPLE: ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - strings 50 (Do wordlist secret key beast power on counted clients utilizing 50 threads...)

EXAMPLE: ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - username administrator (Do wordlist secret key beast power on the 'administrator' username only...)

EXAMPLE: ruby wpscan.rb - - url www.example.com - - list p (Enumerate introduced modules... )

EXAMPLE: ruby wpscan.rb - - url www.example.com – list (Run all count tools...)

xsser

DESCRIPTION

Cross Site "Scripter" (also known as XSSer) is a programmed - structure to distinguish, exploit and report XSS weaknesses in electronic applications. It contains a few choices to attempt to sidestep specific channels, and different extraordinary strategies of code infusion.

USAGE: xsser [OPTIONS] [-u |-I |-d ] [-g |-p |-c ] [Request(s)] [Vector(s)] [Bypasser(s)] [Technique(s)] [Final Injection(s)]

OPTIONS:  [http://xsser.sourceforge.net/](http://xsser.sourceforge.net/)

EXAMPLE: python xsser.py - u http://host.com (Simple infusion from URL)

EXAMPLE: python xsser.py - I "file.txt" - - intermediary "http://127.0.0.1:8118" - - referer "666.666.666.666" (Simple infusion from File, with peak intermediary and parodying HTTP Referer headers)

EXAMPLE: python xsser.py - u "http://host.com" - p index.php?target=search&subtarget=top&searchstring=" – s (Simple infusion from URL, utilizing POST, with insights results)

EXAMPLE: python xsser.py - u "host.com" – hash (Send a pre-really looking at hash to check whether target will produce - bogus positive-results)

Zaproxy

DESCRIPTION

The OWASP Zed Attack Proxy (ZAP) is a simple to utilize coordinated infiltration testing apparatus for tracking down weaknesses in web applications. It is intended to be utilized by individuals with a wide scope of safety experience and as such is great for designers and practical analyzers who are new to infiltration testing just as being a valuable expansion to an accomplished pen analyzers' tool kit. More information: https://code.google.com/p/zaproxy/

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI instrument

CHAPTER SIXTEEN

SECRET PHRASE ATTACKS: GPU TOOLS

• oclhashcat-light

• oclhashcat-plus

• pyrit

oclhashcat-light

DESCRIPTION

oclhashcat-light – world's quickest NTLM, MD5, SHA1, SHA256 and descrypt saltine. oclHashcat-light is a GPGPU saltine that is enhanced for breaking execution. Thusly, it is restricted to just doing single-hash breaking utilizing Markov assault, Brute-Force assault and Mask assault.

USAGE: oclHashcat-light [options]... hash [mask] OPTIONS http://hashcat.net/wiki/doku.php?id=oclhashcat_lite

EXAMPLE: ./oclHashcat-lite64.bin 9b957cc6ab97cbf88c4f6f0f146adafe  EXAMPLE: ./oclHashcat-lite64 - m 1900 - n 80 - 1 00010203040506070809 - - outfile=out.txt 21B1E417AF2DE6496772BCC2FE33D2593A9BB7A0:003515230478373400 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1

EXAMPLE: ./oclHashcat-lite64.bin - m 1900 - n 800 - 1 00010203040506070809 - - outfile=351514044968571.txt - - session=35151404496857_1 514D1FCDE9231B61DAD191F7BC7675B87D8628B5:003515140449685700 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1

EXAMPLE:./oclHashcat-lite64.bin - m 1900 - n 800 - 1 00010203040506070809 - - outfile=355933045509554.txt - - session=35593304550955_1 B928680D8D7B1242BEBC8B7AC24FF2B90198E213:003559330455095500 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1

oclhashcat-plus

DESCRIPTION

oclhashcat-plus - world's quickest md5crypt, phpass, mscash2 and WPA/WPA2 saltine and world's sole GPGPU based standard motor. oclHashcat-in addition to is a GPGPU-based multi-hash saltine utilizing a bruteforce assault (carried out as cover attack),combinator assault, word reference assault, half breed assault, veil assault, and rule-based assault.

USAGE: oclHashcat-plus [options]... hash|hashfile|hccapfile [dictionary|mask|directory]...

OPTIONS: http://hashcat.net/wiki/doku.php?id=oclhashcat_plus

EXAMPLE: oclHashcat-plus64.exe - m 2500 capture.hccap rockyou.txt (Dictionary assault)

EXAMPLE:  oclhashcat-plus64.exe - m 2500 - a3 capture.hccap ?d?d?d?d?d?d?d?d (Brute-Force Attack)

EXAMPLE:  oclHashcat-plus64.exe - m 2500 - r rules/best64.rule capture.hccap rockyou.txt (Rule-based assault)

pyrit

DESCRIPTION

Pyrit permits to make gigantic data sets, pre-figuring part of the IEEE 802.11 WPA/WPA2-PSK validation work in a space-time-tradeoff. Taking advantage of the computational force of Many-Core-and different stages through ATI-Stream, Nvidia CUDA and OpenCL, it is right now by a wide margin the most remarkable assault against one of the world's most utilized security-conventions.

USAGE: pyrit [options] order

OPTIONS: [https://code.google.com/p/pyrit/wiki/ReferenceManual](https://code.google.com/p/pyrit/wiki/ReferenceManual)

EXAMPLE: pyrit - e NETGEAR confirm

EXAMPLE:  pyrit - r/temp/kismet_dump - o small_dump.pcap stripLive

EXAMPLE:  pyrit - r "large_dumps_*.pcap" - e MyNetwork - o tiny_compressed_dump_MyNetwork.dump.gz strip

EXAMPLE:  pyrit - r test.pcap - b 00:de:ad:be:ef:00 - I words.txt attack_passthrough

EXAMPLE:  pyrit - I dirty_words.txt.gz - e NETGEAR - o - passthrough | cowpatty - d - - r wpatestcapture.cap - s NETGEAR

EXAMPLE:  pyrit - u sqlite:////var/nearby/pyrit.db hand-off

EXAMPLE:  pyrit - u http://192.168.0.100:17934 group

CHAPTER SEVENTEEN

DISCONNECTED ATTACKS

• cachedump

• chntpw

• cmospwd

• crunch

• dictstat

• hashcat

• hash-identifier

• john the ripper

• johnny

• lsadump

• oclhashcat-light

• oclhashcat-plus

• ophcrack

• ophcrack-cli

• policygen

• pwdump

• pyrit

• rainbowcrack

• rcracki_mt

• rsmangler

• samdump2

• sipcrack

• sucrack

• truecrack

cachedump

DESCRIPTION

Cachedump is extraordinary for recovering the reserved Active Directory accreditations from XP machines. CacheDump will make a CacheDump NT Service to get SYSTEM right and make his stuff on the vault. Then, at that point, it will recover the LSA Cipher Key to decode (rc4/hmac_md5 GloubiBoulga) store section esteems. A John The Ripper module has been created to assault the hashed values that are recovered ( timing identical to MD4( MD4( password|U(username) ) ).

USAGE: you want fixed John The Ripper, then, at that point, ./john - format:mscash file.txt

OPTIONS: [https://github.com/mcandre/fgdump/tree/ace/cachedump](https://github.com/mcandre/fgdump/tree/ace/cachedump)

EXAMPLE: Cachedump: c:\cachedump.exe user:2d9f0b052932ad18b87f315641921cda:lab:lab.internal

Copy the outcome in mscash.txt

c:\cachedump.exe – v

Administration not found. Introducing CacheDump Service (C:\cachedump.exe - s) CacheDump administration effectively introduced. Administration began. user:2d9f0b052932ad18b87f315641921cda:lab:lab.internals Service at present dynamic. Halting help... Administration effectively eliminated. John Plugin:

$ ./john - format:mscash ./mscash.txt

Loaded 1 password hash (M$ Cache Hash [mscash]) password (client)

chntpw

DESCRIPTION

chntpw is a Linux utility to (re)set the secret word of any client that has a legitimate (neighborhood) account on your WinNT or Win2000 framework, by adjusting the crypted secret key in the vault's SAM document. You don't have to realize the old secret key to set another one. It works disconnected (i.e., you need to closure your PC and boot off a linux floppy plate). The bootdisk incorporates stuff to get to NTFS parcels and scripts to stick the entire thing together. This utility works with SYSKEY and incorporates the choice to turn it off. A bootdisk picture is given.

USAGE: chntpw [options] <systemfile> [securityfile] [otherreghive] [… ]

OPTIONS: chntpw - h

EXAMPLE: chntpw - I sam (begins the program in the intuitive mode and indicates the name of the Windows sam record)

Cmospwd

DESCRIPTION

CmosPwd is a cmos/profiles secret key recuperation instrument.

More data:  [http://www.cgsecurity.org/cmospwd.txt](http://www.cgsecurity.org/cmospwd.txt)

USAGE: cmospwd [/d]

USAGE:  cmospwd [/d]/[rlw] cmos_backup_file reestablish/load/compose

USAGE:  cmospwd/k kill cmos cmospwd/m[01]* execute chosen module

EXAMPLE: cmospwd/d (to dump cmos in ascii and sweep code)

EXAMPLE:  cmospwd/m0010011 (to execute module 3, 6 and 7)

Crunch

DESCRIPTION

crunch is a device for making bruteforce wordlists which can be utilized to review secret phrase strength. The size of these wordlists isn't to be thought little of, but crunch can utilize examples to lessen wordlist sizes, can pack yield records in different arrangements and (since v2.6) presently incorporates a message informing the size regarding the wordlist that will be made, giving you a 3 second window to stop the creation should the size be excessively huge for your expected use.

More information:  [http://adaywithtape.blogspot.co.uk/2011/05/making wordlists-with-crunch-v30.html](http://adaywithtape.blogspot.co.uk/2011/05/making%20wordlists-with-crunch-v30.html)

USAGE: crunch [min length] [max length] [ character set] [options]

USAGE:  ./crunch [min length] [max length] [character set] [options] - o filename.txt (writing to record)

EXAMPLE: crunch 8 8 abc + + \!\@\# - t TEST^%,@ - o test.txt

EXAMPLE:  ./crunch 1 1 - p bird feline canine (making changes of arrangements of words)

EXAMPLE:  ./crunch 6 6 0123456789ABCDEF

EXAMPLE:./crunch 6 6 ABC\!\@\#\$

EXAMPLE:  ./crunch 6 6 0123456789 - b 1mb - o START (making wordlists in squares of a specific size)

EXAMPLE:  ./crunch 8 8 abcDEF123 - b 100mb - o START (make a wordlist split in records of close to 100mb)

EXAMPLE:  ./crunch 6 6 0123456789 - c 200000 - o START (make records containing close to 200000 (200 thousand) lines (passphrases))

EXAMPLE:  ./crunch "123abcDEF " - t TEST@@@@ (remember a space for the charset, then, at that point, encase the charset in quotes)

Dictstat

DESCRIPTION

The dictstat Python script is an extraordinary little device for secret phrase breaking results examination or for standard wordlist investigation.

More data: http://www.question-defense.com/2012/12/16/dictstat-backtrack-5-privilegeescalation-secret phrase assaults disconnected assaults dictstat

USAGE: dictstat.py [options] passwords.txt

OPTIONS:

-variant show program's adaptation number and exit

-h, - - assist with showing this assistance message and exit

-l 8, - - length=8 Password length channel.

-c loweralpha, - - charset=loweralpha Password charset channel.

-m stringdigit, - - mask=stringdigit Password veil channel

-o masks.csv, - - maskoutput=masks.csv Save veils to a record

EXAMPLE: ./dictstat.py/root/wordlists/500-most noticeably terrible passwords.txt

EXAMPLE: ./dictstat.py - l 4/root/wordlists/500-most noticeably terrible passwords.txt (Password Length Filter)

EXAMPLE: ./dictstat.py - c numeric/root/wordlists/500-most noticeably terrible passwords.txt (Password Charset Filter)

EXAMPLE: ./dictstat.py - m stringdigit - o stringdigit.txt/root/wordlists/500-most noticeably terrible passwords.txt (Password Mask Filter)

Hashcat

DESCRIPTION

Hashcat is the world's quickest CPU-based secret key recuperation instrument. While it's not so quick as its GPU partners oclHashcat-in addition to and oclHashcat-light, huge records can be handily parted in half with a decent word reference and a touch of information on the order switches.

USAGE: hashcat [options] hashfile [mask|wordfiles|directories]

OPTIONS: http://hashcat.net/wiki/doku.php?id=hashcat

EXAMPLE: hashcat-cli64.exe - a 3 – bf-cs-buf abcdefghijklmnopqrstuvwxyz – bf-pw-max 16 - m 0 – o yourfoundpasswords.txt - n 4 – eliminate yourhashlist.txt (brutecforce)

EXAMPLE:  hashcat-cli64.exe - a 0 - m 0 - o yourfoundpasswords.txt - n 4 – eliminate yourhashlist.txt C:\yourwordlist.txt

EXAMPLE:  hashcat-cli64.exe - a 0 - r rules\best64.rule - m 0 - o yourfoundpasswords.txt - n 4 – eliminate yourhashlist.txt C:\yourwordlist.txt (rules)

hash-identifier

DESCRIPTION

hash-identifier is a product to recognize the various kinds of hashes used to encode information and particularly passwords. More data: https://code.google.com/p/hash-identifier/

USAGE: type your hash and get most and least potential hashes

EXAMPLE:

Start program:

python ./Hash_ID_v1.1.py

Present your hash:

e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855

john the ripper

DESCRIPTION

John the Ripper (JTR) is a free secret key breaking programming instrument. It is one of the most famous secret phrase testing and breaking programs as it joins various secret phrase saltines into one bundle, autodetects secret key hash types, and incorporates an adjustable wafer. It very well may be run against different scrambled secret key arrangements including a few sepulcher secret word hash types most regularly found on different Unix flavors (in view of DES, MD5, or Blowfish), Kerberos AFS, and Windows NT/2000/XP/2003 LM hash. Extra modules have stretched out its capacity to incorporate MD4-based secret key hashes and passwords put away in LDAP, MySQL, and others.

USAGE: john [OPTIONS] [PASSWORD-FILES]

OPTIONS: [http://www.osix.net/modules/article/?id=455](http://www.osix.net/modules/article/?id=455)

EXAMPLE:

Save User:gyuJo098KkLy9 into crackme.txt

Then, at that point, run john with any helpful choices

john - single crackme.txt (Single break mode)

john - wordfile:password.lst crackme.txt (word reference assault)

john - incremental:alpha crackme.txt (just letters; steady strategy)

john - incremental:digits crackme.txt (just numbers; steady strategy)

john - incremental:lanman crackme.txt (letters, numbers, and some extraordinary characters; gradual technique)

john - incremental:all crackme.txt (all characters; gradual strategy)

Johnny

DESCRIPTION

Johnny is a GUI for John the Ripper.

All fundamental things function admirably:

• product of broke passwords through clipboard,

• send out works with office suits (tried with LibreOffice Calc),

• client could begin, respite and resume assault (however just a single meeting is permitted worldwide),

• all assault related choices work,

• all information document designs are upheld (unadulterated hashes, pwdump, passwd, blended),

• "shrewd" default choices,

• exact result of broke passwords,

• smooth work, for example no slacks,

• config is put away in .conf record (~/.john/johnny.conf),

• pleasant blunder messages and other easy to use things,

• numerous minor fixes to clean ui.

USAGE: n/a; GUI apparatus

EXAMPLE: n/a; GUI apparatus

Lsadump

DESCRIPTION

LSADump is an application that is utilized to accumulate Windows secret word hashes from PCs running Windows.

USAGE: lsadump $machine.acc [machine]

USAGE: ./lsadump.py<system hive><security hive>

EXAMPLE: lsadump - f/home/morgan/Memory\ Images/PhysicalMemory.bin - y 0xe1035b60 - s 0xe77b9b60

oclhashcat-light

DESCRIPTION

oclhashcat-light – world's quickest NTLM, MD5, SHA1, SHA256 and descrypt saltine. oclHashcat-light is a GPGPU saltine that is streamlined for breaking execution. Along these lines, it is restricted to just doing single-hash breaking utilizing Markov assault, Brute-Force assault and Mask assault.

USAGE: oclHashcat-light [options]... hash [mask]

OPTIONS: http://hashcat.net/wiki/doku.php?id=oclhashcat_lite

EXAMPLE: ./oclHashcat-lite64.bin 9b957cc6ab97cbf88c4f6f0f146adafe

EXAMPLE:  ./oclHashcat-lite64 - m 1900 - n 80 - 1 00010203040506070809 - - outfile=out.txt 21B1E417AF2DE6496772BCC2FE33D2593A9BB7A0:003515230478373400 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1

EXAMPLE:  ./oclHashcat-lite64.bin - m 1900 - n 800 - 1 00010203040506070809 - - outfile=351514044968571.txt - - session=35151404496857_1 514D1FCDE9231B61DAD191F7BC7675B87D8628B5:003515140449685700 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1

EXAMPLE:  ./oclHashcat-lite64.bin - m 1900 - n 800 - 1 00010203040506070809 - - outfile=355933045509554.txt - - session=35593304550955_1 B928680D8D7B1242BEBC8B7AC24FF2B90198E213:003559330455095500 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1

oclhashcat-plus

DESCRIPTION

oclhashcat-plus - world's quickest md5crypt, phpass, mscash2 and WPA/WPA2 saltine and world's solitary GPGPU based principle motor. oclHashcat-in addition to is a GPGPU-based multi-hash saltine utilizing a bruteforce assault (executed as cover attack),combinator assault, word reference assault, half and half assault, veil assault, and rule-based assault.

USAGE: oclHashcat-plus [options]... hash|hashfile|hccapfile [dictionary|mask|directory]...

OPTIONS: http://hashcat.net/wiki/doku.php?id=oclhashcat_plus

EXAMPLE: oclHashcat-plus64.exe - m 2500 capture.hccap rockyou.txt (Dictionary assault)

EXAMPLE:  oclhashcat-plus64.exe - m 2500 - a3 capture.hccap ?d?d?d?d?d?d?d?d (Brute-Force Attack)

EXAMPLE:  oclHashcat-plus64.exe - m 2500 - r rules/best64.rule capture.hccap rockyou.txt (Rule-based assault)

ophcrack

DESCRIPTION

Ophcrack is a free open source (GPL authorized) program that breaks Windows passwords by utilizing LM works out rainbow tables. The program incorporates the capacity to import the hashes from an assortment of configurations, including unloading straightforwardly from the SAM documents of Windows. On most PCs, ophcrack can break most passwords inside a couple of moments. Ophcrack is a Windows secret word saltine dependent on a period memory compromise utilizing rainbow tables. This is another variation of Hellman's unique compromise, with better execution. It recuperates 99.9% of alphanumeric passwords in a moment or two. Ophcrack works for Windows NT/2000/XP/Vista. Ophcrack can be utilized with order line utilizing the choices underneath, or can be run as an unadulterated graphical programming.

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI apparatus

ophcrack-cli

DESCRIPTION

Ophcrack is a free open source (GPL authorized) program that breaks Windows passwords by utilizing LM works out rainbow tables. The program incorporates the capacity to import the hashes from an assortment of arrangements, including unloading straightforwardly from the SAM records of Windows. On most PCs, ophcrack can break most passwords inside a couple of moments. Assuming that you have introduced ophrack-cli bundle, graphical interface isn't accessible.

USAGE: ophcrack [options]

OPTIONS: [http://dev.man-online.org/man1/ophcrack-cli/](http://dev.man-online.org/man1/ophcrack-cli/)

OPTIONS:  ophcrack - h

EXAMPLE: ophcrack - g - d/way/to/tables - t xp_free_fast,0,3:vista_free - f in.txt (Launch ophcrack in order line utilizing tables 0 and 3 in/way/to/tables/xp_free_fast and all tables in/way/to/tables/vista_free and breaks hashes from pwdump document in.txt)

Policygen

DESCRIPTION

PolicyGenerator creates another reference strategy module or updates a current module dependent on mentioned admittance as access vectors. It produces permit rules and alternatively module require proclamations and reference strategy interfaces. As a matter of course just permit rules are created. PolicyGenerator can likewise alternatively add remarks clarifying why a specific access was permitted dependent on the review messages that produced the entrance.

USAGE:  n/a

EXAMPLE: n/a

Pwdump

DESCRIPTION

pwdump dumps Windows secret key hashes. pwdump is the name of different Windows programs that yield the LM and NTLM secret key hashes of neighborhood client accounts from the Security Account Manager (SAM). To work, it should be run under an Administrator account, or have the option to get to an Administrator account on the PC where the hashes are to be unloaded. Pwdump could be said to think twice about on the grounds that it could permit a vindictive manager to get to client's passwords.

More information:  [http://www.foofus.net/~fizzgig/pwdump/](http://www.foofus.net/~fizzgig/pwdump/)

USAGE: n/a

EXAMPLE:  pwdump - u AnAdministrativeUser [-p password] 192.168.0.10

Pyrit

DESCRIPTION

Pyrit permits to make huge information bases, pre-registering part of the IEEE 802.11 WPA/WPA2-PSK validation progressively ease in a space-time-tradeoff. Taking advantage of the computational force of Many-Core-and different stages through ATI-Stream, Nvidia CUDA and OpenCL, it is as of now by a long shot the most remarkable assault against one of the world's most utilized security-conventions.

USAGE: pyrit [options] order

OPTIONS: [https://code.google.com/p/pyrit/wiki/ReferenceManual](https://code.google.com/p/pyrit/wiki/ReferenceManual)

EXAMPLE: pyrit - e NETGEAR confirm

EXAMPLE:  pyrit - r/temp/kismet_dump - o small_dump.pcap stripLive

EXAMPLE:  pyrit - r "large_dumps_*.pcap" - e MyNetwork - o tiny_compressed_dump_MyNetwork.dump.gz strip

EXAMPLE:  pyrit - r test.pcap - b 00:de:ad:be:ef:00 - I words.txt attack_passthrough

EXAMPLE:  pyrit - I dirty_words.txt.gz - e NETGEAR - o - passthrough | cowpatty - d - - r wpatestcapture.cap - s NETGEAR

EXAMPLE:  pyrit - u sqlite:////var/nearby/pyrit.db hand-off

EXAMPLE:  pyrit - u http://192.168.0.100:17934 bunch

Rainbowcrack

DESCRIPTION

RainbowCrack is a PC program which creates rainbow tables to be utilized in secret word breaking. RainbowCrack varies from "ordinary" beast power wafers in that it utilizes enormous pre-processed tables called rainbow tables to lessen the time allotment expected to break a secret key radically. RainbowCrack was created by Zhu Shuanglei, and carries out a further developed time-memory compromise cryptanalysis assault which started in Philippe Oechslin's Ophcrack.

USAGE: rcrack rainbow_table_pathname - h hash

USAGE:  rcrack rainbow_table_pathname - l hash_list_file

USAGE:  rcrack rainbow_table_pathname - f pwdump_file

OPTIONS:

rainbow_table_pathname pathname of the rainbow table(s), wildchar(*, ?) upheld

-h hash utilize raw hash as information

-l hash_list_file use hash list record as information, each hash in a line

-f pwdump_file use pwdump document as info, this will deal with LAN Manager hash as it were

EXAMPLE:    rcrack *.rt - h 5d41402abc4b2a76b9719d911017c592

EXAMPLE:     rcrack *.rt - l hash.txt

EXAMPLE:     rcrack *.rt - f hash.txt

rcracki_mt

DESCRIPTION

Rcracki_mt can be utilized to play out a rainbow table assault on secret key hashes. It is expected for ordered and culminated rainbow tables, principally produced by the circulated project www.freerainbowtables.com

USAGE: rcracki_mt [options] [hash]

OPTIONS: [http://sourceforge.net/project/shownotes.php?release_id=682650](http://sourceforge.net/project/shownotes.php?release_id=682650)

EXAMPLE:     rcracki_mt - h 5d41402abc4b2a76b9719d911017c592 - t 4 - o save.txt C:\md5

EXAMPLE:      rcracki_mt - r - s my_personal_hashes

Rsmangler

DESCRIPTION

RSMangler will take a wordlist and perform different controls on it like those done by John the Ripper with a couple of additional items. The super new element is changes mode which takes each word in the rundown and consolidates it with the others to create every conceivable stage (not blends, request matters).

USAGE: rsmangler.rb [OPTIONS]

OPTIONS: [http://www.randomstorm.com/rsmangler-security-tool.php](http://www.randomstorm.com/rsmangler-security-tool.php)

EXAMPLE: ./rsmangler.rb – record wordlist.txt > new_wordlist.txt

samdump2

DESCRIPTION

samdump2 dumps Windows 2k/NT/XP/Vista secret key hashes.

More data: http://www.hackingdna.com/2012/05/learn-samdump-on-backtrack-5.html

USAGE: samdump2 samhive keyfile

EXAMPLE: ./samdump2 SAM bootkey > hashes

EXAMPLE:  samdump2/mnt/Windows/Windows/System32/config/SAM syskey.txt

EXAMPLE:  samdump2/mnt/Windows/Windows/System32/config/SAM syskey.txt>hash.txt

EXAMPLE:  samdump2/root/sda2/Windows/System32/config/SAM saved-syskey.txt >/root/pass1

EXAMPLE:

Instance of recovering the SAM hashes from a Windows segment/dev/sda1:

# mkdir - p/mnt/sda1

# mount/dev/sda1/mnt/sda1

# bkhive/mnt/sda1/Windows/System32/config/SYSTEM/tmp/saved-syskey.txt

# samdump2/mnt/sda1/Windows/System32/config/SAM/tmp/saved-syskey.txt >/tmp/hashes.txt

Sipcrack

DESCRIPTION

sipcrack - a set-up of instruments to sniff and break the review validations inside the SIP convention. Meeting Initiation Protocol (SIP) is a convention created by the IETF MMUSIC Working Group and is a proposed standard for starting, changing, and ending an intuitive client meeting that includes interactive media components like video, voice, texting, internet games, and augmented reality.

SIPcrack is a SIP login sniffer/saltine that contains 2 projects: sipdump to catch the overview validation and sipcrack to bruteforce the hash utilizing a wordlist or standard information.

sipdump dumps SIP digest validations. In the event that a login is found, the sniffed login is kept in touch with the landfill document. See 'sipdump - h' for choices. sipcrack bruteforces the client's secret word with the landfill document created by sipdump. Assuming a secret phrase is found, the sniffed and broke login will be refreshed in the landfill document. See 'sipcrack - h' for choices.

USAGE: sipcrack [options]<dump_file>

OPTIONS:

-s Use stdin for passwords

-w wordlist document containing all passwords to attempt.

-p num print breaking process each n passwords (for - w) (ATTENTION: dials back intensely)

EXAMPLE:

sipdump - I eth0 logins.dump

sipcrack - w mywordlist.txt logins.dump

Sucrack

DESCRIPTION

sucrack is a multithreaded Linux/UNIX instrument for animal power breaking neighborhood client accounts by means of su. This instrument proves to be useful as conclusive example on a framework where you have not too many advantages but rather you are in the wheel bunch. Numerous su executions require a pseudo terminal to be connected to take the secret key from the client. This is the reason you couldn't utilize a basic shell content to accomplish this work. This instrument, written in c, is profoundly proficient and can endeavor numerous logins simultaneously. If it's not too much trouble, be exhorted that utilizing this device will take a great deal of the CPU execution and top off the logs rapidly.

| rule | description | original | rewritten |
| A | all characters to upper case | myPassword | MYPASSWORD |
| F | first character to upper case | myPassword | MyPassword |
| L | last character to upper case | myPassword | myPassworD |
| a | all characters to lower case | AnotherPASS | anotherpass |
| f | first character to lower case | AnotherPASS | anotherPASS |
| l | last character to lower case | AnotherPASS | AnotherPASs |
| D | prepend a digit (0..9) | password | 1password |
| d | append a digit (0..9) | password | password1 |
| e | 1337ify the word | password | p455w0rd |
| x | enable all of the above rules |  |  |

USAGE: sucrack [options]<wordlist.txt>

OPTIONS: [http://www.leidecker.info/projects/sucrack.shtml](http://www.leidecker.info/projects/sucrack.shtml)

EXAMPLE: sucrack - s 10 - a wordlist.txt

EXAMPLE: sucrack - c - a wordlist.txt

EXAMPLE: sucrack - u myuser wordlist.txt

EXAMPLE: sucrack - b 50 - w 10 wordlist.txt

EXAMPLE: sucrack - r - l AFL wordlist.txt

Truecrack

DESCRIPTION

TrueCrack is a beast power secret key saltine for TrueCrypt (Copyrigth) volume documents. It chips away at Linux and it is streamlined for Nvidia Cuda innovation.

It upholds:

• PBKDF2 (characterized in PKCS5 v2.0) depends on dependent on key induction capacities: Ripemd160, Sha512 and Whirlpool.

• XTS block figure mode for hard plate encryption dependent on AES.

TrueCrack can play out a savage power assault dependent on:

• Word reference: read the passwords from a document of words.

• Letters in order: produce all passwords of given length from given letter set.

TrueCrack deals with gpu and computer chip. In gpu, TrueCrack requires a heaps of assets. We propose to run TrueCrack in a distant meeting without Xserver and framebuffer.

USAGE: Dictionary assault: truecrack – t<truecrypt_file> - k<ripemd160|sha512|whirlpool> - w<wordlist_file> [-b<parallel_blocks> ]

USAGE:  Alphabet assault: truecrack - t<truecrypt_file> - k<ripemd160|sha512|whirlpool>-c<charset> [-s<minlength> ] – m<maxlength> [-b<parallel_block> ]

OPTIONS: [https://code.google.com/p/truecrack/](https://code.google.com/p/truecrack/)

EXAMPLE:  ./truecrack – t test_12345678 – w ../../pass.lst – v

CHAPTER EIGHTEEN

ONLINE ATTACKS

• burpsuite

• cewl

• cisco-inspecting apparatus

• dbpwaudit

• findmyhash

• hydra

• hydra-gtk

• medusa

• ncrack

• onesixtyone

• patator

• phrasendrescher

• thc-pptp-bruter

• webscarab

• zaproxy

Burpsuite

DESCRIPTION

Burp Suite is an incorporated stage for performing security testing of web applications. Its different apparatuses work flawlessly together to help the whole testing process, from beginning planning and investigation of an application's assault surface, through to finding and taking advantage of safety weaknesses. Burp Suite contains the accompanying key parts:

• A blocking Proxy, which allows you to assess and adjust traffic between your program and the objective application.

• An application-mindful Spider, for creeping content and usefulness.

• A high level web application Scanner, for mechanizing the recognition of various kinds of weakness.

• An Intruder apparatus, for performing amazing tweaked assaults to find and take advantage of uncommon weaknesses.

• A Repeater instrument, for controlling and resending individual solicitations.

• A Sequencer device, for testing the haphazardness of meeting tokens.

• The capacity to save your work and resume working later.

• Extensibility, permitting you to effectively compose your own modules, to perform complex and exceptionally tweaked assignments inside Burp.

More data:  [http://portswigger.net/burp/](http://portswigger.net/burp/)

USAGE: n/a; GUI device

EXAMPLE: n/a; GUI instrument

Cewl

DESCRIPTION

CeWL is a ruby application which insects a given url to a predefined profundity, alternatively following outside connections, and returns a rundown of words which would then be able to be utilized for secret key wafers like John the Ripper. Of course, CeWL sticks to simply the site you have indicated and will go to a profundity of 2 connections, this conduct can be changed by passing contentions. Be cautious if setting a huge profundity and permitting it to go offsite, you could wind up floating on to a great deal of different spaces. All expressions of three characters and over are result to stdout. This length can be expanded and the words can be kept in touch with a document as opposed to screening so the application can be mechanized.

USAGE: cewl [OPTION] ... URL

OPTIONS: [http://www.digininja.org/projects/cewl.php](http://www.digininja.org/projects/cewl.php)

EXAMPLE: ./cewl.rb - w passwords.txt http://www.digininja.org/projects/cewl.php (make a secret key record from http://www.digininja.org/projects/cewl.php and save the secret key document in passwords.txt)

cisco-evaluating device

DESCRIPTION

Cisco Auditing Tool - Perl script which filters cisco switches for normal weaknesses. Checks for default passwords, effectively guessable local area names, and the IOS history bug. Incorporates support for modules and checking various hosts.

USAGE: ./CAT [options]

OPTIONS:

-h hostname (for checking single hosts)

-f hostfile (for filtering different hosts)

-p port # (default port is 23)

-w (wordlist for local area name speculating)

-a passlist (wordlist for secret key speculating)

-I [ioshist] (Check for IOS History bug)

-l logfile (record to log to, default screen)

-q calm mode (no screen yield)

EXAMPLE: ./CAT - h 192.168.1.100 - w wordlist - a passwords - I

EXAMPLE: ./CAT - h 192.168.1.22 - a rundowns/passwords - w records/local area (Audit Cisco Telnet Password and SNMP Community String)

Dbpwaudit

DESCRIPTION

DBPwAudit is a Java apparatus that permits you to perform online reviews of secret word quality for quite a long time motors. The application configuration considers simple adding of extra data set drivers by essentially replicating new JDBC drivers to the jdbc index. Design is acted in two records, the aliases.conf document is utilized to plan drivers to nom de plumes and the rules.conf lets the application know how to deal with blunder messages from the sweep.

The device has been tried and known to work with:

- Microsoft SQL Server 2000/2005

- Prophet 8/9/10/11

- IBM DB2 Universal Database

- MySQL

USAGE: dbpwaudit – s<server> - d<db> - D<driver> - U<users> - P<passwords> [options]

OPTIONS: [http://www.edwiget.name/2012/07/evaluating mysql-passwords-with-dbpwaudit/](http://www.edwiget.name/2012/07/evaluating%20mysql-passwords-with-dbpwaudit/)

EXAMPLE: ./dbpwaudit.sh - s localhost - d mysql - D MySQL - U ~/mysql-users.txt - P ~/mysql-password.txt (Assuming I have a db server on localhost and a rundown of mysql usernames saved in my home index as mysql-users.txt and a rundown of passwords to attempt additionally in my home catalog as mysql-password.txt, this order would review the mysql server)

TIP: extra advances are needed for this program to work: http://www.edwiget.name/2012/07/inspecting mysql-passwords-with-dbpwaudit/

Findmyhash

DESCRIPTION

findmyhash.py endeavors to break various kinds of hashes utilizing free internet based administrations.

USAGE: python findmyash.py<algorithm> [OPTIONS]

USAGE: findmyash.py<algorithm> [OPTIONS]

OPTIONS:

h<hash_value> If you just need to break one hash, determine its worth with this choice.

-f<file> If you have a few hashes, you can determine a document with one hash for every line. NOTE: All of them must be a similar sort.

-g If your hash can't be broken, search it in Google and show every one of the outcomes. NOTE: This choice ONLY works with - h (one hash input) choice.

EXAMPLE: python findmyhash.py MD5 - h 098f6bcd4621d373cade4e832627b4f6

EXAMPLE: python findmyhash.py MD4 - h "db346d691d7acc4dc2625db19f9e3f52"

EXAMPLE: python findmyhash.py SHA224 - h "90a3ed9e32b2aaf4c61c410eb925426119e1a9dc53d4286ade99a809"

EXAMPLE: python findmyhash.py LM - h "01fc5a6be7bc6929aad3b435b51404ee"

EXAMPLE: python findmyhash.py CISCO7 - h "12090404011C03162E"

Hydra

DESCRIPTION

THC-Hydra is an extremely quick (multi-strung) network logon wafer which upholds various administrations: afp, cisco, cisco-empower, cvs, firebird, ftp, http-get, http-head, http-intermediary, https-get, https-head, httpsform-get, https-structure post, icq, imap, imap-ntlm, ldap2, ldap3, mssql, mysql, ncp, nntp, prophet audience, pcanywhere, pcnfs, pop3, pop3-ntlm, postgres, rexec, rlogin, rsh, sapr3, taste, smb, smbnt, smtp-auth, smtp-authntlm, snmp, socks5, ssh2, svn, teamspeak, telnet, vmauthd, vnc.

USAGE: hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e ns] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-f] [-s PORT] [-S] [-vV] server administration [OPT]

OPTIONS: [http://www.aldeid.com/wiki/Thc-hydra#Usage](http://www.aldeid.com/wiki/Thc-hydra#Usage)

EXAMPLE: hydra 127.0.0.1 mysql - l root - P/information/dictionnaires/test.txt - t 4

EXAMPLE:  hydra 192.168.1.26 ssh2 - s 22 - P pass.txt - L users.txt - e ns - t 10

EXAMPLE:  hydra 192.168.1.69 http-structure post "/w3af/bruteforce/form_login/dataReceptor.php:user=^USER^&pass=^PASS^:Bad login" - L users.txt - P pass.txt - t 10 - w 30 - o hydra-http-post-attack.txt

hydra-gtk

DESCRIPTION

THC-Hydra is an exceptionally quick (multi-strung) network logon saltine which upholds various administrations: afp, cisco, cisco-empower, cvs, firebird, ftp, http-get, http-head, http-intermediary, https-get, https-head, httpsform-get, https-structure post, icq, imap, imap-ntlm, ldap2, ldap3, mssql, mysql, ncp, nntp, prophet audience, pcanywhere, pcnfs, pop3, pop3-ntlm, postgres, rexec, rlogin, rsh, sapr3, taste, smb, smbnt, smtp-auth, smtp-authntlm, snmp, socks5, ssh2, svn, teamspeak, telnet, vmauthd, vnc.

Likewise a GUI apparatus.

USAGE: hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e ns] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-f] [-s PORT] [-S] [-vV] server administration [OPT]

OPTIONS: [http://www.aldeid.com/wiki/Thc-hydra#Usage](http://www.aldeid.com/wiki/Thc-hydra#Usage)

EXAMPLE: hydra 127.0.0.1 mysql - l root - P/information/dictionnaires/test.txt - t 4

EXAMPLE:  hydra 192.168.1.26 ssh2 - s 22 - P pass.txt - L users.txt - e ns - t 10

EXAMPLE:  hydra 192.168.1.69 http-structure post "/w3af/bruteforce/form_login/dataReceptor.php:user=^USER^&pass=^PASS^:Bad login" - L users.txt - P pass.txt - t 10 - w 30 - o hydra-http-post-attack.txt

Medusa

DESCRIPTION

Medusa - Open Source Software 'Login Brute-Forcer' for Password Auditing. Quick, enormously equal, measured, login beast forcer" with modules accessible to help practically any assistance that permits distant confirmation utilizing a secret word, including: CVS, FTP, HTTP, IMAP, MS-SQL, MySQL, POP3, PostgreSQL, SMTPAUTH, Telnet and VNC. Medusa has been intended to run quicker than Hydra by utilizing string based (rather than Hydra's cycle based) equal testing to endeavor to sign in to various hosts or clients simultaneously.

More data:  [http://www.foofus.net/jmk/medusa/medusa.html#how](http://www.foofus.net/jmk/medusa/medusa.html#how)

USAGE: [-h host|-H file] [-u username|-U file] [-p password|-P file] [-C file] - M module [OPTIONS]

OPTIONS: [http://www.irongeek.com/i.php?page=backtrack-r1-man-pages/medusa](http://www.irongeek.com/i.php?page=backtrack-r1-man-pages/medusa)

EXAMPLE:

To utilize Medusa, the accompanying should be indicated:

• The host "192.168.1.1" to associate with, utilizing the - h switch

• The client name "administrator" to associate with, utilizing the - u switch

• The name of the textfile containing the rundown of passwords to have a go at, utilizing the - P switch

• The module to use for the assistance we are reaching (for this situation http) utilizing the - M switch

medusa - h 192.168.1.1 - u "administrator" - P hugewordlist.txt - M http

Ncrack

DESCRIPTION

ncrack — Network verification breaking instrument. It was intended for high velocity equal breaking utilizing a unique motor that can adjust to various organization circumstances. Ncrack can likewise be widely adjusted for extraordinary cases, however the default boundaries are adequately conventional to cover pretty much every circumstance. It is based on a measured engineering that takes into consideration simple expansion to help extra conventions. Ncrack is intended for organizations and security experts to review enormous organizations for default or frail passwords in a quick and solid manner. It can likewise be utilized to direct genuinely refined and escalated animal power assaults against individual administrations.

USAGE: ncrack [ <Options>] {<target specification> }

OPTIONS: [http://nmap.org/ncrack/man.html](http://nmap.org/ncrack/man.html)

EXAMPLE: ncrack 10.0.0.130:21 192.168.1.2:22

EXAMPLE:  ncrack scanme.nmap.org 192.168.0.0/8 10.0.0,1,3-7.- - p22 (Ncrack acknowledges various host details on the order line, and they don't should be a similar sort)

EXAMPLE:  ncrack scanme.nmap.org:22 ftp://10.0.0.10 ssh://192.168.1.*:5910# (Per-have administration determination)

EXAMPLE:  ncrack scanme.nmap.org 10.0.0.120-122 192.168.2.0/24 - p 22,ftp:3210,telnet (Global help determination)

Onesixtyone

DESCRIPTION

onesixtyone exploits the way that SNMP is a connectionless convention and sends all SNMP demands as quick as possible. Then, at that point, the scanner trusts that reactions will return and logs them, in a style like Nmap ping clears. As a matter of course onesixtyone hangs tight for 10 milliseconds between sending bundles, which is sufficient for 100MBs exchanged organizations. The client can change this worth through the - w order line choice. Assuming that set to 0, the scanner will send parcels as quick as the bit would acknowledge them, which might prompt bundle drop.

USAGE: onesixtyone [options] <host><community>

OPTIONS:

-c<communityfile> document with local area names to attempt

-i<inputfile> document with target has

-o<output> yield log

-d investigate mode, use twice for more data

-w<n> stand by n milliseconds (1/1000 of a second) between sending parcels (default 10)

-q calm mode, don't print log to stdout, use with – l

EXAMPLE:  onesixtyone 192.168.100.51

Patator

DESCRIPTION

Patator is a multi-reason savage forcer, with a particular plan and an adaptable use. More data: https://code.google.com/p/patator/

USAGE:  python patator.py<module> - h

USAGE:  <module> - h (assuming you made the alternate routes)

EXAMPLE:    patator.py ftp_login host=10.0.0.1 user=FILE0 password=qsdf 0=logins.txt - x ignore:mesg='Login inaccurate.' (FTP : Enumerate substantial logins on a too verbose server)

Phrasendrescher

DESCRIPTION

phrasen|drescher is a breaking apparatus utilized to observe the pass expression for RSA or DSA keys as they would be utilized by SSH for example. It performs wordlist and rule based assaults against the key.

More information: http://leidecker.info/projects/phrasendrescher.shtml

USAGE:   Incremental mode: phrasendrescher - I 6:8 key-document

USAGE:   Incremental mode: phrasendrescher - I 8 key-document (producing 8 characters in length words )

USAGE:   Incremental mode: phrasendrescher - I 8:12 key-document (indicate range)

USAGE:   Dictionary mode: phrasendrescher - d wordlist key-document

USAGE:   Dictionary mode: phrasendrescher - d wordlist index containing-keys (read and attempt numerous keys in the event that you indicate a registry rather than a solitary key document)

EXAMPLE:     ./phrasendrescher - vd wordlist.txt my.key

thc-pptp-bruter

DESCRIPTION

A brute power program that neutralizes pptp vpn endpoints. The utilization of the device is really clear: simply pipe a word reference record into the thc-pptp-bruter and determine both the username and the host you are assaulting. Note that after interfacing with the gadget, you would see some concise data about the host to which you are associating, for example, "Hostname ˜c2611wooter, Vendor ˜Cisco Systems, Inc., Firmware: 4608." This is a valuable strategy for far off application layer fingerprinting.

More information: http://flylib.com/books/en/3.418.1.83/1/

USAGE:    thc-pptp-animal [options] <remote ip>

OPTIONS:

-v Verbose result/Debug yield

-W Disable windows hack [default: enabled]

-u <user> User [default: administrator]

-w <file> Wordlist record [default: stdin]

-p < > PPTP port [default: 1723]

-n < > Number of equal attempts [default: 5]

-l < > Limit to n passwords/sec [default: 100]

EXAMPLE: thc-pptp-bruter - u g0tmi1k - n 99 - l 999 10.0.0.3

Webscarab

DESCRIPTION

WebScarab is a structure for examining applications that impart utilizing the HTTP and HTTPS conventions. It is written in Java, and is along these lines convenient to numerous stages. WebScarab has a few methods of activity, executed by various modules. In its most normal use, WebScarab works as a blocking intermediary, permitting the administrator to survey and alter demands made by the program before they are shipped off the server, and to audit and change reactions got back from the server before they are gotten by the program. WebScarab can catch both HTTP and HTTPS correspondence. The administrator can likewise audit the discussions (solicitations and reactions) that have gone through WebScarab.

More information: https://www.owasp.org/index.php/WebScarab_Getting_Started

USAGE:  n/a; GUI apparatus

EXAMPLE: n/a; GUI apparatus

Zaproxy

DESCRIPTION

The OWASP Zed Attack Proxy (ZAP) is a simple to utilize incorporated entrance testing apparatus for tracking down weaknesses in web applications. It is intended to be utilized by individuals with a wide scope of safety experience and as such is great for engineers and practical analyzers who are new to infiltration testing just as being a helpful expansion to an accomplished pen analyzers' tool kit.

More data:  [https://code.google.com/p/zaproxy/](https://code.google.com/p/zaproxy/)

USAGE: n/a; GUI instrument

EXAMPLE: n/a; GUI device