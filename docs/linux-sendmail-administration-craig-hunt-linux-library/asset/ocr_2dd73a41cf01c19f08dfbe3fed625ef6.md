# Appendix C Sendmail Variables, Options, and Flags

ResolverOptions-options sets resolver options. Available options values are: debug, usevc, primary, recurse, defnames, stayone, and dns. The option can be preceded by a plus (+) to turn it on or a minus (-) to turn it off. One other, HasWildcardMX, is specified without a + or -. Simply adding HasWildcardMX turns the option on. See Linux DNS Server Administration by Craig Hunt (Sybert, 2006), for more information about resolver options.

RetryFactor=factor is used to decrease the priority of a job every time it is processed, so that mail that cannot be delivered keeps popping to the top of the queue. The default is 90,000.

RrtmpliesDsn if true, tells Sendmail to return a Return-Receipt-To: header as a request for delivery service notification. The default is false.

RunAsUser=userid[:groupid] defines the user ID and group ID that Sendmail will run under of root. When Sendmail is running on a well-maintained firewall. On general purpose systems, this may decrease security because it requires that many files be readable or writeable by this user ID.

SafeFileEnvironment=directory Tells Sendmail to chroot to the specified directory before writing a file and to refuse deliver to symbolic links.

SaveFromLine Tells Sendmail to use unix-style From lines at the front of headers. Normally, they are discarded.

MIMEErrors Tells Sendmail to send error messages in MIME format.
ServerCertFile=file identifies the file that contains the certificate Sendmail should use when this system acts as a mail server.

ServerKeyFile=file identifies the file that contains the private key Sendmail should use when this system acts as a mail server.

SwitchFilePath=path defines the path to a file that lists the methods used for various services. The SwitchFilePath contains entries that begin with the service name followed by the service method. Sendmail checks for services named aliases and hosts and supports dns, nis, nisplus, or files as possible methods, assuming that support for all of these is compiled into this copy of Sendmail. SwitchFilePath defaults to /etc/mail/service. switch on Sendmail 8.11. If a file does not exist, Sendmail uses the following service methods: aliases are looked up in the aliases files, and hosts are looked up first using DNS, then NIS, and finally the file. Most Linux systems have a built-in service switch feature configured by the nsswitch.conf file, so it is used and option ignored. See the Linux DNS Server Administration book for a description of the nsswitch.conf file.