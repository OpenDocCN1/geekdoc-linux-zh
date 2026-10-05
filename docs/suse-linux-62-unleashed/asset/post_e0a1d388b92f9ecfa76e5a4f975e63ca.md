
[content]
# Automating Tasks
CHAPTER 22
649

# Emacs

Emacs is one of the most polarizing lightning rods for religious controversy among computer users. Emacs has many intelligent and zealous users who believe it is the ideal platform for all automation efforts. Its devotees have developed what was originally a screen editor into a tool with capabilities to newsgroup discussion, Web browsing, application development, general-purpose scripting, and much more. For the purposes of this chapter, what you need to know about Emacs follows:

- It's an editor that you ought to try at some point in your career.
- If you favor integrated development environments, Emacs can do almost anything you imagine. As an editor, it emulates any other editor, and its developers ensure that it always offers state-of-the-art capabilities in language-directed formatting, application integration, and development automation.

Even if the “weight” of Emacs (it may seem slow on startup and require quite a bit of education and configuration) weighs you against its daily use, keep it in mind as a paragon of how sophisticated programming makes common operations more efficient.

![](img/cbac72550c7126a22162e94d91a0c360_684_0.png)

> Note
The Emacs editor is included with SuSE Linux. You can use Emacs with or without the X Window system. Type the word emacs on the command line of your console or an X11 terminal window and press the Enter key. Run its built-in tutorial by pressing Ctrl+H and the T key.

# procmail

Computer use has exploded in the Internet era. The most indispensable, often used Internet function is email. Can email be automated?

Yes—and automating email is perhaps the single best return on your investment. Along with aliases, distribution lists, startup configurations, and the plethora of mail agents or clients with their feature sets, you'll want to learn about procmail. Suppose you receive a hundred messages a day, that fifth of them can be handled completely automatically, and it takes at least three seconds of your time to process a single piece of email; those are conservative estimates. A bit of procmail automation will save you at least a minute a day, or six hours a year. Even conservative estimates make it clear that an hour of setting up procmail pays for itself many times over.

# SuSE System Administration
PART III

With the man procmail pages, serious study of procmail starts with the page http://www.faqs.org/faqs/mail/filtering-faq, Nancy McGough's Filtering Mail FAQ. This gives detailed installation and debugging directions. You'll also find information about procmail in the Mail-HOWTO, found under the /usr/doc/howto/en directory.

Because your SuSE Linux machine will almost certainly have a correctly configured procmail, you can immediately begin to program your personal use of it. As a first experiment, create these files: ~/.procmailrc, with these contents:

```bash
VERBOSE=on
MAILDIR=$HOME/mail
SPAMDIR=$HOME/.procmail
LOGFILE=$SPAMDIR/log
INCLUDER=$SPAMDIR/rc.testing
```

~/.procmail/rc.testing, holding this code:

```bash
:0:
* Subject:.*HOT
SPAM.HOT
```

~./forward, with this:

```bash
"!IFS=" & -& exec /usr/bin/procmail -f !! exec 75 #YOUR_EMAIL_NAME
```

After you create these three, set necessary permissions with the following:

```bash
# chmod 644 ./forward
# chmod ax ./.
```

Now exercise your filter with the following:

```bash
# echo "This message 1." ! mail -s "Example of HOT SPAM." YOUR_EMAIL_NAME
# echo "This message 2." ! mail -s "Desired message." YOUR_EMAIL_NAME
```

What you now see in your mailbox is only one new item: the one with the subject Desired message. You also have a new file in your home directory, SPAM.HOT, holding the first message.

procmail is a robust, flexible utility that you program to achieve even more useful automations than this. When you gain familiarity with it, it will become natural to construct rules that, for example, automatically discard obvious spam, sort incoming mailing-list traffic, and perhaps even implement peter forwarding, remote system monitoring, or FAQ responding. This can save you considerable time each day.

# Internal Scripts

One of the most effective tools you have is to look for opportunities within your application. Scripting has become a pervasive theme, and almost all tools are scriptable. One of the most effective tools you have is to look for opportunities within your application. Scripting has become a pervasive theme, and almost all tools are scriptable.

# Concluding Challenge for an Automator

In this chapter, you've learned various ways of using your computer so that it serves you. You now know how to improve your skills, and you're ready for the next challenge: How do you take your skills to the next level?

[/content]
