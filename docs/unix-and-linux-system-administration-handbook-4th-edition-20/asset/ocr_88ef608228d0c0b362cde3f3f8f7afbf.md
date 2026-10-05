# Chapter 20 Electronic Mail

Lots of options are available that control what users can and cannot do in their .forbid forwards. The option names begin with forbid_ or allow_. They're important to prevent users from running shells, loading libraries into binaries, or using the embedded Perl interpreter when they shouldn't. Check for new forbid_ options when you are sure to use when they can't get too fancy in their .forbid forwards.

# Transports

Routers decide where messages should go, and transports actually take them there. Local transports typically append to a file, pipe to a local program, or speak the LMTP protocol to IMAP servers. Remote transports speak SMTP to their counterparts across the Internet.

There are five Transports: appendfile, lmtp, smtp, autoreply, and pipe; we define appendfile and smtp. The autoport is typically used to send vacation messages, and the pipe transport hands messages as input to a command through a UNIX pipe. As with routers, you must define instances of transports, and it's fine to have multiple instances of the same type of transport. Order is significant for routers, but not for transports.

# The appendfile transport

The appendfile driver stores messages in mbox, mbx, Maildir, or mailstore in a specified file or directory. You must have included the appropriate mailbox formats when you compiled; they are commented out of the EDITIME file by default. The following example defines the my_local_delivery transport (an instance of the appendfile transport) referred to in the localousers router definition on page 821.

```
my_local_delivery:
driver = appendfile
file = /var/mail/$local_part
delivery_date_add
envelope_to_add
return_path_add
group = mail
mode = 0660
```

The various *add lines adds headers to the message. The group and mode clauses ensure that the transport agent can write to the file.

# The smtp transport

The smtp transport is the workhorse of any mail system. Here, we define two instances, one for the standard SMTP port (25) and one for the mail submission port (587).