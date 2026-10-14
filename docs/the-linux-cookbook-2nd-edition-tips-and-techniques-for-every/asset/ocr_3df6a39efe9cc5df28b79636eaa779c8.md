# 27.6.1 Reminding Yourself When You Have to Leave

```
Leave
DEB: leave
RPM: leave
WWW: ftp://ftp.netbsd.org/pub/NetBSD/NetBSD-current/src/usr.bin/
```

Use the leave tool to remind yourself when you have to leave. Give as an argument the time when you have to go, using the format of hhmm, where hh is hours in 24-hour format and mm is minutes.

⇒ To remind yourself to leave at 8:05 p.m., type:
$ leave 2005 [RET]

When you run leave with no arguments, it prompts you to enter a time; if you just type [RET], leave exits without setting the reminder. This method is good for adding leave to scripts or to your .bashrc, so that you can interactively give a time to leave, if desired, when the script runs (see Recipe 3.7.3 [Using Shell Startup Files], page 86).

NOTES: leave will output a reminder on the terminal screen five minutes before the given time, one minute before the time, at the time itself, and then every minute subsequently until the user logs off.

# 27.6.2 Sending Yourself Email Reminders

Sending yourself a short email message is often effective for reminding yourself to do something during your next workday or next time you read mail; keeping a message in your inbox works as a constant reminder to get something done—provided you don’t abuse it and fill your inbox with lots of these “urgent” mails!

To quickly send an email reminder, give your email address (or just your username on your local system, if you check mail there) as an argument to the mail tool. You’ll be prompted to give a subject for the message, and if that isn’t enough space for the reminder, you can write as many lines as you need below it as the message body text. Type [CTRL]-[D] on a line by itself to send the mail.