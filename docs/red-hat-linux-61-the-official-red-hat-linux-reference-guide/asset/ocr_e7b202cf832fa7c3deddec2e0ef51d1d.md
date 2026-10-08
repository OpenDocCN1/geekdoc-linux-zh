# Chapter 17. Kerberos

+   - rsh and rlogin — In order to include the kerberized versions of rsh and login, you must enable klogin, eklogin, and kshell.

+   - Telnet — To use kerberized Telnet, you must enable krb5-telnet.

+   - FTP — To provide FTP access, extract and create a key for the principal with a root of ftp. Be certain to install the instance to the fully qualified hostname of the FTP server, then enable gsftfp.

+   - IMAP — The IMAP server included in the imap package uses GSS-API authentication using Kerberos 5 if it finds the key in /etc/krb5.keytab. The root for the principal should be imap.

+   - CVS — CVS kerberized gserver uses a principal of root of cvs and is otherwise identical to the CVS pserver.

For details on enabling services, refer to the chapter titled Controlling Access to Services in the Red Hat Linux Customization Guide.

# ## 17.7. Additional Resources

For more information on Kerberos, refer to the following resources.

# ### 17.7.1. Installed Documentation

+   - /usr/share/doc/krb5-server-<version-number>— The Kerberos V5 Installation Guide and the Kerberos V5 System Administrator's Guide in PostScript and HTML formats. You must have the krb5-server package installed.

+   - /usr/share/doc/krb5-workstation-<version-number>— The Kerberos V5 UNIX User's Guide in PostScript and HTML formats. You must have the krb5-workstation package installed.

# ## 17.7.2. Useful Websites

+   - http://web.mit.edu/kerberos/www — Kerberos: The Network Authentication Protocol webpage from MIT.

+   - http://www.nrl.navy.mil/CCS/people/kenh/kerberos-faq.html — The Kerberos Frequently Questions (FAQ).

+   - http://fthena-dist.mit.edu/pub/kerberos/unix.ps — The Postscript of Kerberos: An Authentication Service for Open Network Systems by Jeremy G. Steiner, Clifford Needham, and Jeffrey I. Schiller. This document is the original describing Kerberos.

+   - http://web.mit.edu/kerberos/dialogue.html — Designing an Authentication System: A Dialogue in Four Scenes by Bill Bryant in 1988, modified by Theodore Ts'o in 1997. This document is a conversation between two developers who are thinking about the creation of a Kerberos-style authentication system. The conversational style of the discussion made this good starting place for people who are unfamiliar with Kerberos.

+   - http://www.nrl.org/~jar/HowToKerberos.html How to Kerberize your site is a good reference for kerberizing a network.

+   - http://www.networkcomputing.com/netdesign/kerbl.html — Kerberos Network Design Manual is a thorough overview of the Kerberos system.