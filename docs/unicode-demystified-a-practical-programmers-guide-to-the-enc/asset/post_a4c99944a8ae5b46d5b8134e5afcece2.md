
| Tool | What It Does | Where to Get It (Continued) | Table C-1 |
|---|---|---|---|
| netcat | Explores, tests, and diagnoses works. | freshmeat.net/projects/netcat | | |
| netsys | A full-disclosure unmoderated security mailing list. | lists.netsys.com | | |
| nmap | Scans hosts to see what ports are available. It can perform stealth scans, determining OS type, find ports, and so on. | www.insecure.org/nmap | | |
| OPIE | Provides one-time passwords for system access. | innernet/opie | | |
| papers | Miscellaneous computer security papers. | www.fish.com | | |
| Psionic (Abacus) Portsentry | Monitors for and reacts to port scans. | www.psionic.com/products/portsentry.html | | |
| RBAC | Role Based Access Control. Assigns roles and privileges associated with the roles. | csrc.nist.gov/rbac | | |
| SAINT | Security Administrator's Integrated Network Tool. Assesses and analyzes network vulnerabilities. This tool follows satan. | www.wwdsl.com/saint | | |
| samhain | A file integrity checker. Has a GUI configurator, client/server capability, and real-time reporting capability. | samhain.sourceforge.net | | |
| SARA | The Auditor's Research Security analysis tool. | www-arc.com/sara | | |
| SATAN | Security Auditor's Tool for Analyzing: Scans your host and network for vulnerabilities. This program is starting to show its age. | www.fish.com/satan | | |
| SecurityFocus | Home for security tools, mail lists, libraries, and cogent analysis. | www.securityfocus.com | | |

| Tool | What It Does | Where to Get It (Continued) | Table C |
|---|---|---|---|
| sentry | Detects port scans. | ftp.cerias.purdue.edu/pub/tools/unix/logutils/sentry | | |
| sfinger | A secure, configurable replacement for the finger daemon. | ftp.cerias.purdue.edu/pub/tools/unix/daemons/sfingerd | | |
| skey | One-time disposable passwords for login. | See logdaemon earlier in this list. | | |
| snort | A flexible IDS. | www.snort.org | | |
| srp | Secure Remote Password. Upgrades common protocols, such as TELNET and FTP to use secure password exchange. | srp.stanford.org | | |
| ssh | A secure rsh, rdist, rlogin replacement with encrypted sessions and other options. Supplied with Red Hat Linux. | www.ssh.org openssh.org | | |
| sudo | Gives very limited Superuser capabilities on an as-needed basis to system operators. | http://ftp.coursean.com/pub/sudo | | |
| swatch | A Perl-based log parser and analyzer. | www.oit.ucsb.edu/~eta/swatch | | |
| syslog-ng | A cryptographically secure replacement for syslog. | www.balabit.hu/en/downloads/syslog-ng | | |
| tcp_wrappers | Monitor, filter, and log incoming requests for systat, finger, ftp, telnet, rlogin, rsh, exec, tftp, talk, and other network services by wrapping system daemons. | ftp://porcupine.org/pub/security/index.html | | |
| tct | The Coroner's Toolkit. Performs forensic analysis. | www.fish.com/tct | | |
| titan | Audits and fixes potential security issues. Originally coded for Solaris, it is being ported to GNU/Linux. | www.fish.com/titan | | |
| tklogger | Visualizes logs. Requires Tcl/Tk. | ftp://cerias.purdue.edu/pub/tools/unix/logutils/tklogger | | |
| Treachery | A collection of tools for security and auditing. | www.treachery.net/tools | | |
| tripwire | Checks for possible signs of intruder activity. Supplied with Red Hat Linux. | ftp://cerias.purdue.edu/pub/tools/unix/ids/tripwire | | |

# Appendix Summary

Security is inversely proportional to usability. There must be a balance between the requirements that your users have to get their work done and the amount of security that is implemented. It is often unnecessary to provide top security for a small business with only a few employees. On the other hand, if you work for a government military contractor, you are bound to have extreme security constraints and an official audit policy to determine whether your security policies are implemented correctly.

Review your own security requirements periodically. Several of the tools mentioned in this appendix are designed to help you do this. Such tools as ness, chain, and SAINT all provide an auditing mechanism.

Some companies specialize in security and auditing. Hiring one of them may be costly but may result in specific recommendations for areas that you may have overlooked in your initial setup. When you hire someone to audit your security, you may be providing both physical and Superuser access to your systems. Make sure the company that you hire has a good history, has been in business for several years, and has impeccable references. Check on them periodically: Things change over time. Avoid the temptation to hire former system crackers as consultants. Security consultants should have an irreproachable ethical background, or you will always have doubts about their intentions.

Your total security package is based on your risk assessment of your vulnerabilities. Strengthen those areas that are most important for your business. For example, many sites will rely on a firewall to protect them completely from the Internet, whereas internal hosts receive little or no security attention. Crackers refer to this "the crunchy outside surrounding the soft chewy middle." Yet this is entirely sufficient to protect some sites. Perform your own risk assessment and address your needs accordingly. If need, hire a full-time security administrator whose job it is to design and audit your security policies.

# IN THIS APPENDIX

- Background 1428
- POSIX.1 1428
- POSIX.2 1430
- POSIX.3 1442
- POSIX.4 1442
- POSIX.5 1443
- Profiles and POSIX Standards 1446

# The POSIX Standards

In the past, the existence of various versions of the UNIX system was a fruitful source of creative and innovative software. However, it has also been a persistent source of frustration for users and programmers. Users who moved between the BSD and System V versions of the system, for example, discovered that commands that worked on one system did not work, or worked differently, on the other. Programmers found a similar phenomenon: Programs that worked on one system differently, or even failed to compile, on another. In 1984 the user's group /usr/group (now called UniForum) started an effort to specify a “standard UNIX.” This effort expanded beyond the wildest dreams of its initiators in the POSIX series of standards.

POSIX standards specify interfaces for application programs but say nothing about how the interfaces are to be implemented. Thus a wide variety of systems, including most varieties of UNIX, GNU/Linux, and many systems that are unrelated to either, now supply versions of these interfaces. As an example, you can run bash with --posix option to make it conform closely with the POSIX.2 standard (page 1430). As a consequence, GNU/Linux can support more and more application programs that run on other POSIX systems.

Richard Stallman¹ provides a connection between GNU and POSIX as he started GNU and was involved in the start of POSIX. The Introduction to POSIX.1 states that “The name POSIX was suggested by Richard Stallman.” POSIX is almost an acronym for Portable Operating System Interface and Stallman probably put the X on the end to give it UNIX “ring.”

- 1. Refer to “The GNU/Linux Connection” on page 4 for more information on Richard Stallman.

# Background

POSIX is the name for a collection of software standards based on but not limited to the UNIX system. The standards are developed by working groups of the Institute for Electronics and Engineering (IEEE); participation in these groups is open to everyone. For this and other reasons, the POSIX standards are referred to as Open Systems Standards.

The explicit goal of the POSIX effort is to promote application portability. Thus the standards specify both program and user interfaces but not implementations. Refer to www.pasc.org/standing/sd11.html#statable for the most recent information on the status of the POSIX standards.

# POSIX.1

POSIX.1 (POSIX 1003.1), the original POSIX standard, was adopted in 1988. POSIX.1 is a C programming language interface standard. In its original form it specified the syntax and semantics of 203 C functions and the contents of various data structures (page 1463). Subsequent revisions have greatly expanded its scope (Table D-1). In 1993 interfaces for supporting real-time programming were added, and in 1995 interfaces for supporting multithreaded application programs were added.

POSIX.1 specifies the abstract structure of a filesystem. For example, a system that conforms to POSIX.1 must have a hierarchical filesystem with directories, FIFO files, and regular files. Each file must have attributes typical of UNIX system files, such as permission bits, owner and group IDs, and link counts. Programming interfaces refer to filenames using familiar UNIX-style pathways, such as /home/alex/src/load.c.

| Name | Description |
|---|---|
| POSIX 1003.1 (POSIX.1) | Base system interfaces in the C language. Includes real-time extensions, threads, protocol independent interfaces, and more. |
| POSIX 1003.2 (POSIX.2) | Shell and utilities, including interactive utilities. |
| POSIX 2003 (POSIX.3) | Test methods for measuring conformance to POSIX standards. |
| POSIX 2003.1 (POSIX.3.1) | Test methods for POSIX 1003.1. |
