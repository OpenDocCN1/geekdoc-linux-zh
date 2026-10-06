# Choosing Email Software

Linux supports quite a few email servers. Chances are, one of the major servers will be installed on your system by default. If not and you want to install one, you'll have to pick one. You may want to change your email server if you need to configure it in advanced ways; some servers are easier to configure than others or specific options that others don't. Four email servers are most popular on Linux:

Sendmail The sendmail program (http://www.sendmail.org) was for many years the dominant email server package on the Internet. In recent years it's lost some of its dominance to the other servers described here, as well as to Windows email servers. Nonetheless, sendmail remains a popular server. It's very powerful, but it's also difficult to configure because its configuration formats are arcane.

Postfix (http://www.postfix.org) was designed as a modular replacement for sendmail—rather than a single program that does everything (as sendmail is designed); Postfix uses multiple programs, each of which handles its own task. This design improves security, at least in theory. Postfix tends to be easier to configure than sendmail, and it is the default email server on many Linux distributions.

Exim Also Exim (http://www.exim.org) is a monolithic server, like sendmail, it has a much simpler configuration format and is so easier to configure. Linux distributions use Exim as the default server.

qmail The fourth major email server, qmail (http://www.qmail.org), is a modular server with security as a design goal. Postfix and Exim, qmail is easier to configure than them. It's not the standard email server in any Linux distribution because its license is a bit strange and complicates qmail with distribution; however, many system administrators like qmail enough that they replace their distributions' standard email servers with qmail.

You learn which email server on your Linux distribution runs several ways to. The two most reliable are to ps (described in Chapter 2, “Managing Software”) to look for running processes or use your package management tools (also described in Chapter 2) to see which package is installed. In either case, you may need to check for each of the programs in turn. For instance, you might see these like:

# $ ps ax | grep send

| 31129 ps | R+ | 0:00 grep send |
| $ ps ax ? | Ss | 0:45 /usr/lib/postfix/master |
| 31132 ps | S+ | 0:00 grep post |

The search for a process containing the string send failed, but the search for post returned a process called /usr/lib/postfix/master—thus, it appears that Postfix is running on this system.