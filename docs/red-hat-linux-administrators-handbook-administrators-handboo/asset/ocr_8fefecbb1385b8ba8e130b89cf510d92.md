| Parameter | Description |
|---|---|
| NoRecipientAction=add-to-undisclosed | When a message does not contain an appropriate recipient header, the specified action is taken. The default value creates a To: undisclosed-recipients header. |
| OldStyleHeaders=True | Toggle old/new header format. No change required. |
| OperatorChars=-%?()! /\|+ | List of token delimiter characters. No change required. |
| PrivacyOptions=needstify,hello, restrictmail, restrictdivr,qoway | See the section on ensuring privacy under "Securing Sendmail" in this chapter for details. |
| QueueDirectory=/var/spool/mqueue | The fully qualified path name of the queue directory. |
| QueueLA=8 | When the system's load average exceeds the specified number, do not send messages but instead queue them. |
| QueueSortOrder=Host | Sets the queue sort order. The default value allows sendmail to sort the queue using the host names of the recipients. You can change this to Priority to sort mail by priority header, or to Time to sort by submission time. |
| RecipientFactor=30000 | Used to penalize the priority of a message that has a large number of recipients. |
| RefuseLA=12 | When the system's load average exceeds the specified value, refuse incoming connections. |
| RetryFactor=80000 | Used to lower priority. No change recommended. |
| RunAsUser=mail | Specifies the username sendmail uses for all of its child processes. In other words, sendmail child processes that are forked to service the actual requests do not run as the superuser; thus, this enhances security. No change recommended. |
| SendMimeErrors=True | When set to True, error messages are set using MIME formats. No change required. |
| SevenBitInput=False | When set to True, a message is converted into seven-bit data. Do not change the default value. |
| O SmtpGreetingMessage= S] Sendmail Svr/SZ, Sb | Sets the greeting message that sendmail issues when a connection is made. If you don't want to tell the world the version of sendmail you use, remove the $v$ variables from this line. This might provide fewer clues for someone who is trying to exploit any security holes. |
| StatusFile=/var/log/sendmail.st | The fully qualified path name of the status file. |
| SuperSafe=True | Toggle super safe mode. Default setting is recommended. |
| TempFileMode=0600 | Sets the default mode for the temporary files in the queue. |
| Timeout.command=30m | Default timeout value for SMTP commands. |
| Timeout.connect=3m | Default timeout value for connection. |
| Timeout.datablock=1h | Default timeout value for data blocks. |
| Timeout.datafinal=1h | Default timeout value for final '.' in the data. |