| Option | Explanation |
|---|---|
| MaxDaemonChildren=40 | Maximum number of forked child processes at any time. |
| MaxHopCount=30 | Maximum length of time a message can be processed before it is rejected. |
| MaxMessageSize=5000000 | Maximum size of a message, in bytes. Messages larger than this size won't be accepted. |
| MeToo=False | When an alias contains the sender herself, sendmail automatically removes the sender from the expansion. If this option is set to True, the sender receives the mail in such a case. You might want to set this to True because you might reduce some tech-support calls from users who want to receive mail even if it originated from themselves. |
| MinFreeBlocks=100 | Minimum number of free blocks that must be present before sendmail will accept a message. This enables you to ensure that someone can't wipe out your disk space by mail bombing (i.e., sending multiple copies of large mail messages) to your server. You might want to increase this to a number higher than the default. |
| MinQueueAge=10m | A message must be in the queue for at least the specified number of minutes before it is processed. |
| NoRecipientAction=add-to-undisclosed | When a message does not contain an appropriate recipient header, the specified action is taken. The default value creates a To: undisclosed-recipients header. |
| OldStyleHeaders=True | Toggle old/new header format. No change required. |
| OperatorChars=.:!*'"/[\]#+ | List of token delimiter characters. No change required. |
| PrivacyOptions=needvrifyhelo, restrictmailq, restrictrctrout, gonawy | See the section on ensuring privacy under "Securing sendmail" in this chapter for details. |
| QueueDirectory=/var/spool/mqueue | The fully qualified path name of the queue directory. |

Continued