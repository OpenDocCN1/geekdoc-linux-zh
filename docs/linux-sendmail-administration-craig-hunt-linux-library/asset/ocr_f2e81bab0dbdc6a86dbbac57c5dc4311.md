POP3 is defined in RFC 1939 (“Post Office Protocol—Version 3”). It is a simple request/response protocol like SMTP. The client sends a command to the server and the server responds to the command. Table 1.3 shows the set of POP3 commands defined in RFC 1939.

# Table 1.3 POP3 Commands

| Command | Function |
|---|---|
| USER username | The username required for the login. |
| PASS password | The user’s password required for the login. |
| STAT | Requests the number of unread messages/bytes. |
| RETR msg | Retrieves message number msg. |
| DELE msg | Deletes message number msg. |
| LAST | Requests the number of the last accessed. |
| LIST [msg] | Requests the size of message msg or of all messages. |
| RSET | Undeletes all messages and resets the message number to 1. |
| TOP msg n | Prints the headers and the first n lines of message msg. |
| NOOP | Does nothing except request an OK response from the remote server. |
| APOP mailbox string | Identifies a mailbox and provides an MD5 digest string for authentication. Used as an alternative to USER/PASS. |
| UIDL [msg] | Requests the unique ID for the specified message number, or a listing of unique IDs for all messages. |
| QUIT | Ends the POP3 session. |