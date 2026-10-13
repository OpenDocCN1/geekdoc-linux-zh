```
250-XUSR
250 HELP
>> MAIL From:<kabir@picaso.nitec.com> SIZE=77
250 <kabir@picaso.nitec.com>... Sender ok
>> RCPT To:<kabir@integrationlogic.com>
250 <kabir@integrationlogic.com>... Recipient ok
>> DATA
354 Enter mail, end with "." on a line by itself
>>
.
250 TAA16439 Message accepted for delivery
kabir@integrationlogic.com... Sent
(TAA16439 Message accepted for delivery)
Closing connection to mail.integrationlogic.com.
>> QUIT
221 wormhole.integrationlogic.com closing connection
```

The lines that start with >> are sent by the local sendmail server (picaso.nitec.com) to the remote sendmail server which is (mail.integrationlogic.com). This is very close to what I demonstrated earlier via a Telnet connection.

# Using the sendmail debug flag

Use the -dX option (where X is a debug level) along with -bv to see what action sendmail will take for a particular address. For example,

```
sendmail -bv -d0 kabir@nitec.com
```

produces the following output on my sendmail server:

```
Version 8.9.3
Compiled with: MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7 NAMED_BIND NETINET NETUNIX NEWDB NIS QUEUE SCANF SMTP USERDB XDEBUG

========== SYSTEM IDENTITY (after readcf) ===========
(short domain name) $w = picaso
(canonical domain name) $j = picaso.nitec.com
```