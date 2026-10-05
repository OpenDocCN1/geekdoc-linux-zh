
## Appendix C Sendmail Variables, Options, and Flags

Table C.4 Possible Settings for the DontBlameSendmail Option (continued)

| Keyword | What It Tells Sendmail |
| --- | --- |
| WriteStatsToHardLink | Write to the status file if it is really a hard link. |
| WriteStatsToSymLink | Write to the status file if it is really a symbolic link. |

DontExpandCnames Disables the conversion of nicknames to canonical names.

DontInGroups Limits the mail delivery agent run for a user to the group associated with that user in the /etc/passwd file. It is used to reduce the load on NIS servers.

DontProbeInterfaces If set to true, stops Sendmail from adding the names and addresses of the network interfaces to class w. The default is false, so interface names and addresses are stored in w.

DontPruneRoutes Prevents Sendmail from explicit mail routes. Normally, Sendmail makes a route as direct as possible. However, optimizing the route may be appropriate for systems located behind a firewall.

DoubleBounceAddress=address Tells Sendmail where to send the report of an error that occurs when sending an error message. The default for address is postmaster.

EightBitMode=action Specifies how undeclared eight-bit data is handled. The possible actions are s--strict, reject undeclared eight-bit data; m--mime, convert the data to MIME format; and p--pass, send the data through unaltered.

ErrorHeader=file-message Specifies the file or message that is prepended to outgoing error messages. If file-or-message is the path to a file, it must begin with a slash. If this option is not defined, nothing is prepended to error messages.

ErrorMode=action tells Sendmail how to handle error messages. If this option is not defined, error messages are printed. The valid actions are:

- Print error messages.
- Return an exit status but no error message.
- Mail the error message back to the sender.
- Write the error messages to the user's terminal.
- Mail the error message back, but always give zero exit status.

FallbackMXhost=fallbackhost fallhost is the host Sendmail should use as a backup MX server for every host.

ForkEachJob Runs a separate process for every item delivered from the queue, which reduces the amount of memory needed to process the queue at the cost of speed.

ForwardPath=path Defines the path searched for .forward files. Multiple paths can be defined by separating them with colons. The default is $z/. Sw=$z/, forward.

HelpFile=path Defines the path to the help file.

Expensive Tells Sendmail to queue mail for outgoing mailers that have the (expensive) mail flag set. Normally, mail is delivered immediately.

HostsFile=path Defines the path to the hosts file. The default is /etc/hosts.

HostStatusDirectory=path Defines the directory in which status information is stored.

IgnoreDots Causes Sendmail to ignore dots in incoming messages. Dots are ignored in SMTP mail because they are used to mark the end of a mail message.

LDAPDefaultSpec=specification Defines the default specification used for LDAP databases.

LogLevel=n Tells Sendmail how much detail to store in the log file. n defaults to 9, which is normally plenty of detail.

MatchGECOS, the username from the e-mail address is checked against the alias database and the username of the passwd file to determine if the user is local. This option adds a check against the GECOS field of the passwd file.

MaxAliasRecursion=n Aliases point to other aliases before finally resolving to the actual mail. This option defines how deep aliases can be nested resolving to a mail address. The default for n is 10.

MaxDaemonChildren=n Tells Sendmail to refuse connections when n children are processing incoming mail. Normally, Sendmail sets no arbitrary limit on child processes.

MaxHeadersLength=bytes Defines the maximum length allowed for all of the headers taken together.

MaxCount=n Tells Sendmail to assume a message is looping when it has been processed more than n times. The default is 25.

MaxSizeSize=n Sets the maximum message size advertised in response to the ESMMTP EHLO command. Messages larger than this size are rejected.

MaxMimeHeaderLength=size Defines the maximum length of MIME header fields.

MaxQueueRunSize=n Sets the maximum number of items that can be processed in a single queue run. The default is no limit.

MaxRecipientsPerMessage=n limits the maximum number of recipients for a single message. If it is not specified, there is no limit.

MeToo Tells Sendmail to send a copy of the message back to the sender.

MinFreeBlocks=n Tells Sendmail to reject incoming mail unless n disk blocks are free for the queue.

MinQueueAge=n Tells Sendmail to skip any jobs that have been in the queue for fewer than n minutes.

MustQuoteChars=[] Defines the list of characters added to the set. If MustQuoteChars is specified without a value for characters, it adds . and ' to the standard set of quoted characters.

NoRecipientAction=action Tells Sendmail what to do when a message has no valid recipient header. action can be:

- none Passes the message on unmodified.
- add-to Adds a To header using the recipient addresses from the envelope.
- add-apparently-to Adds an Apparently-To: header.
- add-to-undisclosed Adds a To: undisclosed-recipients; header.
- add-bcc Adds an empty Bcc: header.

OldStyleHeaders Allows spaces to delimit names. Normally, commas delimit names.

OperatorChars=chars Lists the operator characters used to determine tokens within address rewriting.

Pidfile=path Specifies the path to the Sendmail PID.

PostmasterCopy=username Tells Sendmail to send a copy of error messages to username. The default is not to send copies of error messages to the account.

PrivacyOptions=options Sets the SMTP protocol options. The options value is a comma-separated list containing one or more of these keywords:

- public Allows all commands to be used.
- needmailhelo Requires a valid HELO or EHLO command before the MAIL From: header will be accepted.
- needexpnhello Requires a valid HELO or EHLO command before the EXPN command will be accepted.
- noexpn Disables the EXPN command.

needvrfyhelo Requires a valid HELO and EHLO command before the VRFY command will be accepted.

novrf Disables the VRFY command.

restrictmail Restricts use of the mailq command to users with group access to the queue directory.

restrictqrun Tells Sendmail that only the root user and the owner of the queue directory are allowed to run the queue.

norecept Tells Sendmail not to return messages verifying successful delivery.

goaway Disables all SMTP status queries.

authwarnings Tells Sendmail to insert X-Authentication-Warning: headers in the messages.

ProcessTitlePrefix=prefix Defines a string used on the heading of the process status reports.

QueueDirectory=path Defines the queue directory.

QueueFactor=factor is a numeric value used with the difference between the current load and the load average limit with the message priority to determine if a message should be queued or sent immediately. The idea is to queue priority messages if the system is currently heavily loaded. It defaults to 600,000.

QueueLA=n Directs Sendmail to queue messages when the system load average exceeds n. The default is 8.

QueueSort=sequence Defines the sequence in which the queue is sorted. Priority ordering is the default. The valid sequence values are:

- h Sorts in hostname sequence.
- t Sorts in submission time sequence.
- p Sorts in message priority order.

RandFile=file Points to a file that contains pseudo-random data for encryption techniques. This is used only if the compile option HASURANDOM is not available.

RecipientFactor=factor Directs Sendmail to the lower of a job by each recipient, so that jobs with large numbers of recipients have lower priority. Defaults to 30,000.

RefuseLA=n Tells Sendmail to refuse incoming SMTP connections when the system load average exceeds n. The default is 12.
