This restarts syslogd after logrotate processes the /var/log/maillog file.

# Ensuring a stricter mode of operating and privacy

You can force sendmail to enforce strict adherence to the SMTP protocol when clients connect to your server, and you can control how users interact with sendmail. You do this by using an option line such as the following:

```
O PrivacyOptions=needvrfyhelo, restrictmailq, restrictqrun, goaway
```

The values for PrivacyOptions are shown in Table 9-3.

# Table 9-3 Privacy Options for sendmail

Table 9-3 Privacy Options for sendmail
| Option | Explanation |
|:-------------|:--------------------------------|
| public | Allow open access |
| needmailhelo | Client must use HELLO or EHLO before issuing a MAIL command |
| needexpnhelo | Client must use HELLO or EHLO before issuing an EXPN command |
| noexpn | Client cannot use EXPN command |
| needvrfyhelo | Client must use HELLO or EHLO before issuing a VRFY command |
| novrfy | Client cannot use VRFY command |
| notrn | Client cannot use TRN command |
| nover b | Client cannot use VERB command |
| restrictmailq | Restrict use of mailq command. When this option is set, only the superuser and the owner and group owners of the queue directory can run the mailq command |
| restrictqrun | Restrict the -q option. When this option is set, only the superuser and the owner of the queue directory can use this option |
| norereceipts | Do not return success code upon success |
| goaway | Do not allow SMTP status queries |
| authwarnings | Insert X-Authentication-Waming: headers in messages |