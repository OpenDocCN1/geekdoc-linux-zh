# 32.1.1 Mailing a User on the Same System

To send an email message to another user on the same system, give their username on the system instead of an email address.³

⇒ To send an email message to user mrs on your local system, type:

```
$ mail mrs RET
Subject: Are you going to the party tonight? RET
CTRL - D
Cc: RET
Null message body; hope that's ok
$
```

This command sends an email message to the user mrs on the local system. The email message itself is empty, but the subject is a short note asking whether user mrs will be attending a party.

NOTES: Besides being good for sending mail to users that you might share your system with, mail is useful for sending yourself mail, as a way to give yourself a reminder at your terminal (see Recipe 27.6.2 [Sending Yourself Email Reminders], page 550).

# 32.1.2 Mailing a File or the Output of a Command

The mail tool is also useful for mailing the contents of a text file or the text output of a command. To do this, give the email addresses you want to send to as arguments to mail, and use the standard input redirection operators to redirect the text to use as the message body (see Recipe 3.2 [Redirecting Input and Output], page 67).

⇒ To mail the contents of the text file traderoutes to the email address sofala@example.com, type:

```
$ mail sofala@example.com < traderoutes RET
```

# 32.1.3 Mailing a Directory

There are a few different methods for sending a directory of files in email.

³ Technically, you still are giving the email address, since email addresses take the form of username@hostname; when hostname is omitted, the localhost is assumed.