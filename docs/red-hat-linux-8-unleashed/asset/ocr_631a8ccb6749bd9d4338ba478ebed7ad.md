# CHAPTER 19 Handling Electronic Mail

extremely useful program to use in shell scripting because it can take all the information it
eeds to send mail from the command line. No user interaction is required. It is also
useful for sending quick notes because it starts up quickly and doesn't require going
through menus to send a message.

# Using mail

To begin sending a message in mail, simply type mail at the shell prompt, followed by the
email address that you want to send mail to; for example, mail@cheetah.org. mail
will then prompt you for the subject of the message. Enter the subject and press Enter. The
cursor will then move down to the next blank line. You can now start entering the body
of message. When you have finished, press Ctrl+D on a blank line to exit the mail
program and send the message. (You might be prompted for Cc: If you do not want to
send carbon copies to anyone, simply press Here.) The message will be handed off to the
MTA, and your shell prompt will return. Abandon the number and message you are currently
writing, press Ctrl+C.

If you want to retrieve your email using the mail program, simply type mail at the shell
prompt. The system will respond with something similar to the following:

```
Mail version 0.1 6/6/93. Type ? for help.
/var/mail/user: 1 message unread
>U 1 user@cheetah.org      Tue 25 07:15 18/551      "Meeting tomorrow"
>N 2 spam@lamer.com         Tue 25 08:25 18/542      "A large and
>obnoxious spam message"
>N 3 user@cheetah.org      Tue 25 09:21 17/524      "Meeting has
>been rescheduled
>N 4 user5@lion.org         Tue 25 09:24 17/528      "Issues regarding
>software build
&
```

The prompt is mail's way of prompting you for input.

The first column in the list of messages is a flag that indicates the status of the message.
For example, U means that the message is unread. N means that the message is new. The
rest of the columns are self-explanatory.

To read one of these messages, simply type the message and press Enter.

For example,

```
& 4
```

```
Message 4
```

```
From user5@lion.org      Tue 25 09:24:35 2001
Date: Tue, 25 Sep 2001 09:24:34 -0500
From: user5@lion.org
```