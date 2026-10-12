```
/var/log/maillog {
    postrotate
        /usr/bin/killall -HUP syslogd
    endscript
}
```

This command restarts syslogd after logrotate processes the /var/log/maillog file.

# Ensuring a stricter mode of operating and privacy

You can force sendmail to enforce stricter adherence to the SMTP protocol when clients connect to your server, and you can also control how users interact with sendmail. This is done using an option line such as the following:

```
O PrivacyOptions=needvrfyhelo,restrictmailq,restrictqrun,goaway
```

The values for PrivacyOptions are shown in Table 13-3.

Table 13-3 PrivacyOptions for sendmail

| Option | Explanation |
|---|---|
| public | Allows open access. |
| needmailhelo | Client must use HELO or EHELO before issuing a MAIL command. |
| needexpnhelo | Client must use HELO or EHELO before issuing an EXPN command. |
| noexpn | Client cannot use EXPN command. |
| needvrfyhelo | Client must use HELO or EHELO before issuing a VRFY command. |
| novrfy | Client cannot use VRFY command. |
| notrn | Client cannot use ETRN command. |
| noverb | Client cannot use VERB command. |
| restrictmailq | Restrict use of mailq command. When this option is set only the root user and the owner and group users of the queue directory can run the mailq command. |
| restrictqrun | Restricts the -q option. When this option is set, only the root user and the owner of the queue directory can use this option. |
| noreceipts | Do not return success code upon success. |