# Table F-1: Commands for the mailx Program (cont.)

| Command | Description |
|---|---|
| mbox [msg_list] | Marks the current message or the specified messages to be moved to your mbox file. This is helpful if you have set the hold variable in your .mailrc file. |
| more [msg_list] | Displays the messages in msg_list using the defined pager program in PAGER. Identical to the page subcommand. |
| More [msg_list] | Similar to the more subcommand, but also displays the ignored header fields. See more and ignore subcommands. |
| new [msg_list]
New [msg_list] | Marks each message in the msg_list as not having been read. Identical to the unread and Unread subcommands. |
| page [msg_list] | Displays the messages in msg_list using the defined pager program in PAGER. Identical to the more subcommand. |
| Page [msg_list] | Similar to page but also displays the ignored header fields. Identical to the More subcommand. |
| pipe [msg_list] [shell_cmd]
pi [msg_list] [shell_cmd]
| [msg_list] [shell_cmd] | Pipes the msg_list through the shell_cmd. The message is treated as being read. If no arguments are given, the current message is piped through the command given in cmd. If the page option is set, a formfeed is inserted after each message. |
| next
n
+
Return | Displays the next message. |
| Print [message]
P [message]
Type [message]
T [message] | Displays the current message or the specified message, including any header fields specified by the ignore command. |
| print [message]
p [message]
type [message]
t [message] | Displays the current message or the specified message without any header fields specified by the ignore command. |