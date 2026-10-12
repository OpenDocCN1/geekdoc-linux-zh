spool/mqueue, by default). The filename prefixes present in this directory are described in Table 19-1 earlier in this chapter. The next lines relate to timeout values used by sendmail:

```
O Timeout.connect=1m
O Timeout.ident=0
O Timeout.queuereturn=5d
O Timeout.queuewarn=4h
```

Several options relating to timeouts while waiting for events can be specified, as shown in the preceding lines. (Many more that are commented out are not shown.) These values limit the amount of time sendmail spends waiting for an event to occur or complete. The actual time values can be specified in seconds, minutes, hours, or days (with each specified as an integer followed by s, m, h, or d, respectively). An explanation for each is given in Table 19-3. Each timeout option is in the form Timeout.event, where event is replaced by the timeout events listed in the table.

# Table 19-3: Timeout Events

| Timeout Events | Waiting for . . . |
|---|---|
| aconnect | the successful delivery of e-mail to a recipient |
| auth | the reply to an SMTP AUTH request |
| command | the next command |
| connect | the acceptance of a connection |
| control | the whole socket transaction to finish |
| datablock | the read of the DATA block to complete |
| datafinal | acknowledgment of the final dot or End-of-File marker |
| datainit | acknowledgment of the DATA command |
| fileopen | an NFS file open command to complete |
| helo | a HELO or EHLO |
| hoststatus | the results of a host status check |
| iconnect | the initial connect(2) system call to complete |
| ident | the results of an identification protocol response |
| initial | the initial greeting message |
| lhlo | a reply to an LMTP LHLO command |
| mail | acknowledgment of the MAIL command |
| misc | acknowledgment of other SMTP commands |
| queuereturn (any priority) | the message delivery to complete (a bounce message will be delivered) |