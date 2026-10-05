# Windows compliance with email and web standards

Although Windows has no stand-alone (i.e., X) native port of xterm, a neat little program called rxvt comes awfully close. It is part of the Cygwin system, downloadable from cygwin.com. If you Cygwin's X server, you can use the real xterm.

Cygwin is distributed by the GNU General Public License and contains an extensive complement of common UNIX commands as well as a portant library that implements the POSIX APIs under Windows. Cygwin's reconciliation of the UNIX and Windows command-line and filesystem conventions is well thought out and manages to bring many of the creature comforts of a UNIX shell feel at home, Cygwin makes it easy to get UNIX software running under Windows. See cygwin.com for more details.

The MKS Toolkit is a commercial alternative to Cygwin. See MKS's web site at mksoftware.com for more information.

A growing list of UNIX software now runs natively on Windows, including Apache, Perl, Bind, PHP, MySQL, Vim, Emacs, Gimp, midrange, and Python. Before attempting to force an application to work on Windows with something Cygwin, find out if a native implementation is available.

# 30.5 WINDOWS COMPLIANCE WITH EMAIL AND WEB STANDARDS

In an ideal world, everybody would use open standards to communicate and happiness would abound. But this is not an ideal world, and many have accused Windows of being a mess of proprietary protocols and broken implementations of Internet standards. Partly true, perhaps, Windows can play nicely in some parts of the world. Two of these areas are email and web service.

In the world history of the web, a number of corporations have tried to embrace and extend the web in ways that would allow them to look competition and give their own business a mighty boost. Microsoft is still engaged in this battle at the browser level with numerous extensions peculiar to Internet Explorer. However, Windows and Windows browsers are relatively platform agnostic.

Microsoft provides its own web server, IIS, but the adoption of IIS has historically lagged that Apache running on Linux by a significant margin. Unless you are locked to a server-side technology such as ASP; or your vendor's product requires IIS, there is no compelling to use Windows machines as web servers.

For email, Microsoftにつ Exchange Server as the preferred technology.. be told, Exchange Server's capabilities do outshine those of Internet-standard mail systems, particularly when the mail clients consist of boxes running Microsoft Outlook. But fear not: Exchange Server can also speak SMTP for inbound and outbound mail, and it can serve mail to UNIX clients through the standard IMAP and POP protocols.

![](bbox=[0.945, 0.715, 0.995, 0.83])