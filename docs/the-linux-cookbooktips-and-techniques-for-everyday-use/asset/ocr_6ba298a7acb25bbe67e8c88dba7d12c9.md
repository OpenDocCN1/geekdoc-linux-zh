• To output records containing the text `scott` anywhere in the record, type:

```
M-x bbdb RET scott RET
```

There are additional functions that let you narrow your search to a particular field: `bbdb-name`, `bbdb-company`, `bbdb-net`, and `bbdb-notes`, which respectively search the name, company, email address, and notes fields.

• To output records matching the regexp `*.edu` in the email address, type:

```
M-x bbdb-net RET ^\\.edu RET
```

# 28.6 Reminding Yourself of Things

Sometimes, it's useful to make a reminder for yourself that you'll see either later in your current login session, or the next time you log in. These recipes describe the best ways to do this.

*NOTE:* When you want to give yourself a reminder for a future appointment, use `calendar` (see section [Managing Appointments](#)).

+   - [28.6.1 Sending Yourself Email Reminders](#) — Sending yourself email.
+   - [28.6.2 Reminding Yourself When You Have to Leave](#) — Telling you when it's time to go.
+   - [28.6.3 Running a Command on a Delay](#) — Running a command on a delay.

# 28.6.1 Sending Yourself Email Reminders

Sending yourself a short email message is often effective for reminding yourself to do something during your next workday or next time you read mail; keeping a message in your INBOX works as a constant reminder to get something done—provided you don't abuse it and fill your INBOX with lots of these "urgent" mails!

To quickly send an email reminder, give your email address (or just your username on your local system, if you check mail there) as an argument to `mail` tool. You'll be prompted to give a subject for the message, and if that isn't enough space for the reminder, you can write as many lines as you need below it as the message body text; type `C-d` on a line by itself to send the mail.