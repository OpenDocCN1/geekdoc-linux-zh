| Option | Explanation |
|---|---|
| OldStyleHeaders=True | Toggle old/new header format. No change required. |
| OperatorChars=.:% @ ! ^ / [ ] + | List of token delimiter characters. No change required. |
| PrivacyOptions=needvrfyhelo, restrictmailq, restrictqrun,goaway | See the "Securing sendmail" section on ensuring privacy later in this chapter for details. |
| QueueDirectory=/var/spool/mqueue | The fully qualified pathname of the queue directory. |
| QueueLA=8 | When the system's load average exceeds the specified number, do not send messages but instead queue them. |
| QueueSortOrder=Host | Sets the queue sort order. The default value allows sendmail to sort the queue using the host names of the recipients. You can change this to Priority to sort mail using priority header, or you can set this to Time to sort by submission time. |
| RecipientFactor=30000 | This value is used to penalize the priority of a message that has a large number of recipients. |
| RefuseLA=12 | When the system's load average exceeds the specified value, refuse incoming connections. |
| RetryFactor=90000 | This value is used to lower message retry priority. No change recommended. |
| RunAsUser=mail | This value sets the username sendmail uses for all its child processes. In other words, sendmail child processes that are forked to service the actual requests do not run as the superuser; this therefore enhances security. No change recommended. |
| SendMimeErrors=True | When set to True, error messages are set using MIME formats. No change required. |
| SevenBitInput=False | When set to True, a message is converted into 7-bit data. Do not change the default value. |
| O SmtpGreetingMessage=$j Sendmail $v/$Z; $b | Sets the greeting message that sendmail issues when a connection is made. If you do not like to tell the world about the version of sendmail you use, remove the $v/$Z variables from this line. This might provide fewer clues for someone who is trying to exploit any security holes. |
| StatusFile=/var/log/sendmail.st | The fully qualified pathname of the status file. |