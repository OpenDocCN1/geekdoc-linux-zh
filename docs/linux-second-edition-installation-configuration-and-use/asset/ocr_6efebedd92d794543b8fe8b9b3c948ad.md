```
250 (jupiter.galactic.network) pleased to meet you.
>>> MAIL From:<hofer@jupiter.galactic.network>..
250 <hofer@jupiter.galactic.network>.. Sender Ok
>>> RCPT To:<hofer@provider.de>
250 <hofer@provider.de> OK
>>> DATA
354 Enter mail, end with "." on a line by itself
> .
>>>
250 Mail accepted
hofer@jupiter.galactic.network... Sent (Mail accepted)
Closing connection to provider.de.
>>> QUIT
221 Closing connection
```

read mail
fetchmail: 1 message for hofer at pop.provider.de
reading message 1 of 1 (1699 bytes) . flushed
ppp0 link terminated

In principle, you can further automate your mail system. For example, you can configure /etc/crontab in such a way that offlinemail is called periodically (say, once an hour).