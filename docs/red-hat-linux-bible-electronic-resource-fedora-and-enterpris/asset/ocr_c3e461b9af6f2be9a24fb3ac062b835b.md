```
#O CACertPath
#O CACertFile
#O ServerCertFile
#O ServerKeyFile
#O ClientCertFile
#O ClientKeyFile
```

The CACertPath option lets you indicate a directory that contains CA certificates. CACertFile lets you indicate an individual CA certificate. ServerCertFile and ServerKeyFile let you identify the CA certificate and associated private key, respectively, that sendmail should use when it is acting as a server. ClientCertFile and ClientKeyFile let you identify the CA certificate and associated private key that sendmail should use when it is acting as a client.

# Message precedences

Precedences can be associated with e-mail messages in an attempt to give some messages higher authority for transferring than others. The Message precedences section of the sendmail.cf file sets how different message precedences are handled. The following lines appear at the beginning of the section:

```
Pfirst-class=0
Pspecial-delivery=100
Plist=-30
Pbulk=-60
Pjunk=-100
```

The previous lines equate precedence values with the possible precedence names in message headers. The meaning of each precedence name is indicated in Table 19-4. The numbers by themselves aren’t significant, except in relation to other precedence names. Also note that incoming mail is processed immediately by default, so these priority values apply only to messages in the queue.

Table 19-4: Precedence Names

| Name | Meaning |
| :--- | :--- |
| special-delivery | A high-priority message that should be delivered from the queue before any others. |
| first-class | Unless overridden in the message header, this is the default priority. |
| list | This precedence name should be used for most messages emanating from mailing lists. |
| bulk | A relatively noncrucial broadcast message. This also indicates that if there are delivery troubles, the body of the message will not be included in bounce notices. |
| junk | Worthless e-mail that is possibly the output of a program or a test message. The body is also discarded from bounce notices. |