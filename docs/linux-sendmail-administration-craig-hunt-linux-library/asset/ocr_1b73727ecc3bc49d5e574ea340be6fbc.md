MaxQueueRunsize=n sets the maximum number of items that can be processed in a single queue. The default is no limit.

MaxRecipientsPerMessage=n limits the maximum number of recipients for a single message. If it is not specified, there is no limit.

MeToo Tells Sendmail to send a copy of the message back to the sender.

MinFreeBlocks=n Tells Sendmail to reject incoming mail unless n blocks are free for the free queue.

MinQueueAge=n Tells Sendmail to skip processing of any jobs that have been in the queue for more than n minutes.

MustQuoteChars=characters Defines the list of characters added to the set @;:() that must be quoted when using the username part of an address. If MustQuoteChars is specified without a value for characters, it adds . and ' to the standard set of quoted characters.

NoRecipientAction=action Tells Sendmail what to do when a message has no valid recipient header. action can be:

+   - none Passes the message on unmodified.
- add-to Adds a To: header using the recipient addresses from the envelope.
- add-apparent-to Adds an Apparently-To: header.
- add-to-undisclosed Adds a To: undisclosed-recipients; header.
- add-bcc Adds an empty Bcc: header.

OldStyleHeaders Allows spaces to delimit names. Normally, commas delimit names.

OperatorChars=charlist Lists the operator characters used to determine tokens within addresses for rewriting.

Pidfile=path Specifies the path to the Sendmail PID file.
PostmasterCopy=username Tells Sendmail to send a copy of error messages to username. The default is not to send copies of error messages to the postmaster account.

PrivacyOptions=options Sets the SMTP protocol options. The options value is a comma-separated list containing one or more of these keywords:

+   - public Requires a valid HELO or EHLO command before the MAIL From: envelope header will be accepted.
- needmailhelo Requires a valid HELO or EHLO command before the EXPN command will be accepted.
- noxpn Disables the EXPN command.