# Appendix B The sendmail Command

# Table B.2 Debugging Level Settings (continued)

| Setting | Information Displayed |
|---|---|
| 62.8 | The state of all file descriptors before each delivery. |
| 62.10 | The state of all file descriptors after each delivery. |
| 91.100 | Log via syslog each time a connection is cached or un-cached. |
| 99.100 | Same as using the -bD switch. |

> **NOTE** The Table heading says “Information Displayed.” However, three of the debug levels, 18.100, 51.104 and 52.100, do not just display information. Those three levels change how Sendmail operates.

This book has attempted to reduce the complexity of Sendmail by focusing on common Sendmail administration tasks and the tools you really need to use to get those tasks done. There is really no way to reduce the complexity of all these debug levels except to say that only the few levels covered in Chapter 10 are really useful. If you feel you must dig deeper into Sendmail debug levels, I recommend you get the book *sendmail* by Bryan Costales and Eric Allman (O'Reilly, 2nd ed., 1997).