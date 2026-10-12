Otherwise, this line is ignored. The option is set to False by default because this behavior violates RFC 1123. The next lines relate to the log level:

```
```text
# log level
O LogLevel=9
```
```

The LogLevel option sets the priority and severity of logging messages sent to the syslog facility. Values range from 0 (only severe errors are reported) to 98 (maximum debugging information is logged, along with all the more important messages). Unless you need to view copious amounts of debugging information while tracking down a mail delivery problem, the default value of 9 provides a suitable level of detail. The next lines relate to how messages are sent to the message sender:

```
```text
# send to me too, even in an alias expansion?
#O MeToo=True
```
```

The MeToo option selects sendmail's behavior when the sender of a message is also on the mailing list's distribution list. Unless a value of True is specified, the sender does not receive the message (based on the assumption that if the sender wrote the message, the sender doesn't need to see it again). The next lines have to do with evaluating addresses:

```
```text
# verify RHS in newaliases?
O CheckAliases=False
```
```

If the value is set to True, the CheckAliases option evaluates addresses on the left side of the colon and guarantees a valid delivery agent for addresses on the right side. The default value is False. The next lines relate to old-style headers:

```
```text
# default messages to old style headers if no special punctuation?
O OldStyleHeaders=True
```
```

Lists of recipients were originally delimited by spaces. More recently, commas have been used because recipient names frequently contain spaces. When set to True, the OldStyleHeaders option allows comma-delimited lists, but unquoted spaces are converted to commas. If the option is set to False (the default), uncommitted spaces are converted to the character specified by the BlankSub option. The next lines relate to SMTP daemon options:

```
```text
# SMTP daemon options
# DaemonPortOptions=Name=MTA
O DaemonPortOptions=Port=smtp, Addr=127.0.0.1, Name=MTA

# SMTP client options
#O ClientPortOptions=Address=0.0.0.0
```
```

The DaemonPortOptions option can be used to restrict the port number and network on which sendmail will listen for incoming connections, the number of simultaneous incoming connections, and the size of the TCP/IP send and receive buffers.