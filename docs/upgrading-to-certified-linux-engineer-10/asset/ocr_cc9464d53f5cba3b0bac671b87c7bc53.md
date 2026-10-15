# Command Syntax

SMTP commands provide direct communication between the sender and recipient. The most commonly used SMTP commands are described in the following table.

# Table 12-1

| Command Syntax | Description of the Arguments |
|---|---|
| HELO hostname | hostname contains the complete host name of the SMTP sender. |
| MAIL FROM: reverse-path | reverse-path contains the relay path for source route relaying and the sender's address. |
| RCPT TO: forward-path | forward-path contains the relay path for source route relaying and the recipient's address. |
| DATA data | data constitutes the contents of the mail (the actual message). |
| RSET | /. |
| VRFY string | string contains a user or mailbox name. |
| EXPN string | string contains a mailing list identifier. |
| HELP [string] | string contains any SMTP command. |
| NOOP | /. |
| QUIT | /. |

Commands can be written in lower case or upper case: SMTP commands are not case sensitive. For example, the SMTP recipient will treat the following commands in the same way: MAIL FROM, Mail From, mail from, Mail FrOm.