keep the mail you've already read in the /var/spool/mail/hermie file, so it moves read mail to a separate file called mbox in your own home directory.

To access the messages in the mbox file, you have to use the command

```
mail -f mbox
```

Kind of annoying, ain't it? But at least the mail program looks and acts the same regardless of which mail file you're working with.

# OTHER MAIL COMMANDS

Let's get back into the mail program and have some fun with the two messages that we didn't read before with this scenario (again, bold type represents your input):

```
mail

Mail version 5.6 6/1/95. Type ? for help.
"/var/spool/mail/hermie": 1 message 1 new
>U 1 D.Rhodes@spam.net Mon Feb 10 15:37 "Make Money Fast!"
U 2 Chris@qwerty.com Mon Feb 10 15:37 "Tennis, Anyone?"
& 2
Message 2:
Date: Mon, 10 Feb 1997 15:37:52 -0500
From: Chris@qwerty.com
To: hermie@fritz.com
Subject: Tennis, Anyone?
Wanna whack a few a 4:30 today? -Chris
& reply
Subject: Re: Tennis, Anyone?
Sure, I'll see you on the lower courts at 4:30.
'D
EOT
& header
U 1 D.Rhodes@spam.net Mon Feb 10 15:37 "Make Money Fast!"
>U 2 Chris@qwerty.com Mon Feb 10 15:37 "Tennis, Anyone?"
& delete 1
& q
Saved 1 message in /home/hermie/mbox
```

We've introduced several new commands here, so let's take a closer look at the five operations that were performed in this mail session: