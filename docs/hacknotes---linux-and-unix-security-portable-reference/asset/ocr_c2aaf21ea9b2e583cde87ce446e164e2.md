# Chapter 4: Remote Hacking 73

# Encrypt E-mails

The GNU Privacy Guard set of tools can be used to facilitate the encryption of e-mails. Encourage users to encrypt e-mail containing sensitive information. Visit http://www.gnupg.org/ for more information on GNU Privacy Guard.

Software Vulnerabilities Sendmail is the most popular MTA (Mail Transfer Agent) used on the Internet. Sendmail is known to have many susceptible to remotely exploitable vulnerabilities.

+   - Sendmail Header Buffer Overflow Vulnerability This vulnerability was caused by a buffer overflow condition in Sendmail's header-parsing component. More specifically, Sendmail's crackaddr *addr failed to correctly handle < > characters in the string containing "From" address field in the mail header. For more details, visit http://www.cert.org/advisories/CA-2003-067.html and http://securityfocus.com/bid/6991.

+   - Sendmail MIME Vulnerability Sendmail version 8.8.3 introduced a new vulnerability caused by improper bounds checking while performing MIME conversions on e-mail messages. It was possible to exploit this vulnerability in order to run arbitrary commands on the Sendmail server by sending specially crafted messages that caused the Sendmail process to overwrite its internal stack space. See http://online.securityfocus.com/bid/685 for more information.

+   - Sendmail HELO Buffer Overflow A buffer overflow in older versions of Sendmail caused to crash when long strings were sent as a parameter to its HELO command. It was possible to remotely exploit this vulnerability in order to run arbitrary commands on the Sendmail server. More info can be found at http://www.eyee.com/html/Products/Retina/RTHs/Mail_Servers/141.html.

+   - Sendmail DNS Map TXT Record Buffer Overflow A buffer overflow vulnerability was found in the DNS handling of Sendmail code. This vulnerability was caused by improper bounds checking on data returned from the name server. This vulnerability leads to a buffer overflow, it is possible to exploit this vulnerability to run commands on the Sendmail server by making a malicious name server return a response of arbitrary length. More information can be found at http://online.securityfocus.com/bid/5122.