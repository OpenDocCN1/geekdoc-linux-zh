Chapter 4: Remote Hacking

73

# Encrypt E-mails

The GNU Privacy Guard set of tools can be used to facilitate the encryp\ntion of e-mails. Encourage users to encrypt e-mail containing sensitive\ninformation. Visit **http://www.gnupg.org** for more information on\nGNU Privacy Guard.

+   ▪ **Software Vulnerabilities**  Sendmail is the most popular MTA (Mail Trans-\nfer Agent) used on the Internet. Sendmail is known to have been suscep-\ntible to many remotely exploitable vulnerabilities.

+   ▪ **Sendmail Header Processing Buffer Overflow**  \n**Vulnerability** This vulnerability was caused by a buffer\noverflow condition in Sendmail’s header-parsing compo-\nnent. More specifically, Sendmail’s crackaddr (char *addr)\nfunction failed to correctly handle < and > characters in the\nstring containing the “From” address field in the mail header.\nFor more details, see **http://www.cert.org/advisories/CA-2003-07**\n.html and **http://security.focus.com/bid/6991**.

+   ▪ **Sendmail MIME Vulnerability** Sendmail version 8.8.3\nintroduced a new vulnerability caused by improper bounds\nchecking while performing MIME conversions on e-mail\nmessages. It was possible to exploit this vulnerability in order\nto run arbitrary commands on the Sendmail server by sending\npecially crafted messages that caused the Sendmail process to\noverwrite its internal stack space. See **http://onliners.securityfocus**\n**.com/bid/685** for more information.

+   ▪ **Sendmail HELO Buffer Overflow**  A buffer overflow in older\nversions of Sendmail caused it to crash when long strings were\nsent as a parameter to its HELO command. It was possible to\nremotely exploit this vulnerability in order to run arbitrary\ncommands on the Sendmail server. More info can be found\nat **http://www.eeye.com/html/Products/Retina/RTHS/**\n**/Mail_Servers/141.html**.

+   ▪ **Sendmail DNS Map TXT Record Buffer Overflow**\n**Vulnerability**  A buffer overflow vulnerability was found\nin the DNS handling of Sendmail code. This vulnerability was\ncaused by improper bounds checking on data returned from the\nname server. Since this vulnerability leads to a buffer overflow,\nit is possible to exploit this vulnerability to run commands on\nthe Sendmail server by making a malicious name server return\na response of arbitrary length. More information can be found\non **http://online.securityfocus.com/bid/5122**.

Remote Services