
FallbackMXhost=fallbackhost is the host Sendmail should use as a backup MX server for each host.

ForkEachJob Runs a separate process for every item delivered from the queue, which reduces the amount of memory needed to process the queue at the cost of speed.

ForwardPath=path Defines the path searched for .forward files. Multiple paths can be defined by separating them with colons. The default is $/.forward. $w:z/.forward.

HelpFile=path Defines the path to the help file.

HoldExtensive Tells Sendmail to queue mail for outgoing mailers that have the (expensive) mailer flag set. Normally, mail is delivered immediately.

HostsFile=path Defines the path to the hosts file. The default is /etc/hosts.

HostStatusDirectory=path Defines the directory in which host status information is stored.

IgnoreDots Causes Sendmail to ignore dots in incoming messages. Dots cannot be ignored in SMTP mail because they are used to mark the end of a mail message.

LDAPDefaultSpec=specification Defines the default specification used for LDAP databases.

LogLevel=n tells how much detail to store in the log file. n defaults to 9, which is plenty of detail.

MatchGECOS Normally, the username from the e-mail address is checked against the aliases database and the username of the passwd file to determine if the user is local. This option adds a check against the GECOS file of the passwd file.

MaxAliasRecursion=n Aliases point to other aliases before finally resolving to the actual mail address. This option defines how deep aliases can be nested before resolving to a mail address. The default for n is 10.

MaxDaemonChildren=n Direct Sendmail to refuse connections when n children are processing incoming mail. Normally, Sendmail sets no arbitrary limit on child processes.

MaxHeaders=bytes Defines the maximum length allowed for all of the headers together.

MaxHopCount=n Tells Sendmail to assume a message is looping when it has been processed more than n times. The default is 25.

MaxSize=n Sets the maximum message size advertised in response to the SMTP EHLO command. Messages larger than this size are rejected.

MaxMimeHeaderLength=size Defines the maximum length of MIME header fields.

MaxQueueRunsize=n sets the maximum number of items that can be processed in a single queue. The default is no limit.

MaxRecipientsPerMessage=n limits the maximum number of recipients for a single message. If it is not specified, there is no limit.

MeToo Tells Sendmail to send a copy of the message back to the sender.

MinFreeBlocks=n Tells Sendmail to reject incoming mail unless n blocks are free for the free queue.

MinQueueAge=n Tells Sendmail to skip processing of any jobs that have been in the queue for more than n minutes.

MustQuoteChars=characters Defines the list of characters added to the set @;:() that must be quoted when using the username part of an address. If MustQuoteChars is specified without a value for characters, it adds . and ' to the standard set of quoted characters.

NoRecipientAction=action Tells Sendmail what to do when a message has no valid recipient header. action can be:

- none Passes the message on unmodified.
- add-to Adds a To: header using the recipient addresses from the envelope.
- add-apparent-to Adds an Apparently-To: header.
- add-to-undisclosed Adds a To: undisclosed-recipients; header.
- add-bcc Adds an empty Bcc: header.

OldStyleHeaders Allows spaces to delimit names. Normally, commas delimit names.

OperatorChars=charlist Lists the operator characters used to determine tokens within addresses for rewriting.

Pidfile=path Specifies the path to the Sendmail PID file.

PostmasterCopy=username Tells Sendmail to send a copy of error messages to username. The default is not to send copies of error messages to the postmaster account.

PrivacyOptions=options Sets the SMTP protocol options. The options value is a comma-separated list containing one or more of these keywords:

- public Requires a valid HELO or EHLO command before the MAIL From: envelope header will be accepted.
- needmailhelo Requires a valid HELO or EHLO command before the EXPN command will be accepted.
- noxpn Disables the EXPN command.

needvrfyhelo Requires a valid HELO or EHLO command before the VRFY command will be accepted.

novrfy Disables the VRFY command.

restrictmailq Restricts use of the mailq command to users with group access to the queue directory.

restrictqrun Tells Sendmail that only the root user and the owner of the queue directory are allowed to run the queue.

norecipts Tells Sendmail not to return messages verifying successful delivery.

goaway Disables all SMTP status queries.

authwarnings Tells Sendmail to insert X-Authentication-Warning: headers in messages.

ProcessTitlePrefix=prefix Defines a string used on the heading of the process status reports.

QueueDirectory=path Defines the path to the queue directory.

QueueFactor=factor is a numeric value used with the difference between the current load and the load average limit and the message priority to determine if a message should be queued or sent immediately. The idea is to queue low-priority messages if the system is currently heavily loaded. It defaults to 600,000.

QueueLA=n Directs Sendmail to queue messages when the system load average n. The default is 8.

QueueSortOrder=sequence Defines the sequence in which the queue is sorted. Priority ordering is the default. The valid sequence values are:

- h Sort in hostname sequence.
- t Sort in submission time sequence.
- p Sort in message priority order.

RandFile=file Points to a file that provides pseudo-random data for certain encryption techniques. This is used only if the compile option HASURANDOM is not available.

RecipientFactor=factor Directs Sendmail to the lower of a job for each recipient, so that jobs with large numbers of recipients have lower priority. Defaults to 30,000.

RefuseLA=n Tells Sendmail to refuse incoming SMTP connections when the system load average exceeds n. The default is 12.

## Appendix C Sendmail Variables, Options, and Flags

ResolverOptions-options sets resolver options. Available options values are: debug, usevc, primary, recurse, defnames, stayone, and dns. The option can be preceded by a plus (+) to turn it on or a minus (-) to turn it off. One other, HasWildcardMX, is specified without a + or -. Simply adding HasWildcardMX turns the option on. See Linux DNS Server Administration by Craig Hunt (Sybert, 2006), for more information about resolver options.

RetryFactor=factor is used to decrease the priority of a job every time it is processed, so that mail that cannot be delivered keeps to the top of the queue. The default is 90,000.

RrtmpliesDsn if true, tells Sendmail to return a Return-Receipt-To: header as a request for delivery notification. The default is false.

RunAsUser=userid[:groupid] defines the user ID and group ID that Sendmail will run under of root. When Sendmail is running on a well-maintained firewall. On general purpose systems, this may decrease security because it requires that many files be readable or writeable by this user ID.

SafeFileEnvironment=directory Tells Sendmail to chroot to the specified directory before writing a file and to refuse deliver to symbolic links.

SaveFromLine Tells Sendmail to use unix-style From lines at the front of headers. Normally, they are discarded.

MIMrrors Tells Sendmail to send error messages in MIME format.
ServerCertFile=file identifies the file that contains the certificate Sendmail should use when this system acts as a mail server.

ServerKeyFile=file identifies the file that contains the private key Sendmail should use when this system acts as a mail server.

SwitchFilePath=path defines the path to a file that lists the methods used for various services. The SwitchFilePath contains entries that begin with the service name followed by the service method. Sendmail checks for services named aliases and hosts and supports dns, nis, nisplus, or files as possible methods, assuming that support for all of these is compiled into this copy of Sendmail. SwitchFilePath defaults to /etc/mail/service. switch on Sendmail 8.11. If a file does not exist, Sendmail uses the following service methods: aliases are looked up in the aliases files, and hosts are looked up first using DNS, then NIS, and finally the file. Most Linux systems have a built-in service switch feature configured by the nsswitch.conf file, so it is used and option ignored. See the Linux DNS Server Administration book for a description of the nsswitch.conf file.
