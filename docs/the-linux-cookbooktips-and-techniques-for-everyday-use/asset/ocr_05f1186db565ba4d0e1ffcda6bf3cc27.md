BSD UNIX hackers at Berkeley, and when one of them wrote a mail notification tool, he thought of Biff---hence the name. (Biff, the dog, died in August 1993.)

# 31.3.3 Counting How Many Messages You Have

```
@sf(Debian): `elm-me+`
@sf(WWW): ftp://ftp.uu.net/networking/mail/elm
```

Use messages to count the number of mail messages in a folder or file. Give the name of a mail folder as an argument; with no arguments, it counts the mail you have waiting in your INBOX.

+   - To see how many email messages you have waiting, type:
+     $ messages RET

+   - To count the number of email messages in the mail folder `~/email/saved`, type:
+     $ messages ~/email/saved RET

# 31.3.4 Seeing Who Your Mail Is From

```
@sf(Debian): `elm-me+`
@sf(WWW): ftp://ftp.uu.net/networking/mail/elm
```

Use frm to output a list of sender names and subjects for your mail. Give the name of a mail folder as an option; with no options, frm reads your INBOX.

+   - To output a list showing sender names and subjects of your incoming mail, type:
+     $ frm RET

+   - To output a list showing sender names and subjects of the mail in the file `~/email/saved`, type:
+     $ frm ~/email/saved RET