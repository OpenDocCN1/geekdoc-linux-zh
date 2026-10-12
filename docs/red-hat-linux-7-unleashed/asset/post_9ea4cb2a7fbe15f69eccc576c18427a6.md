
Expect is an extension to Tcl, so it is fully programmable with Tcl capabilities. For information about Tcl and Tk from its author, Dr. John Ousterhout, visit http://www.sun.com/960710/cover/ousterhout.html. For more information about Expect, visit http://expect.nist.gov.

> **Tip**
>
> You'll also find the `autoexpect` command included with Red Hat Linux. This command watches an interactive session at the console and then creates an executable program to execute the console session. See Chapter 11 for an example of how to use `autoexpect` to automate an FTP session.

## Perl

Some consider Perl the most popular scripting language for Red Hat Linux, apart from the shell. Its power and brevity take on particular value in automation contexts.

> **Note**
>
> For more information about Perl, or to get the latest release, browse http://www.perl.com or http://www.perl.org.

For example, assume that `/usr/local/bin/modified_directories.pl` contains this code:

```perl
#!/usr/bin/perl
# Usage: modified_directories.pl DIR1 DIR2 ... DIRn
# Output: a list of all directories in the file systems under
#    DIR1 ... DIRn, collectively. They appear, sorted by the
#    interval since their last activity, that is, since a file
#    within them was last created, deleted, or renamed.
# Randal Schwartz wrote a related program from which this is
# descended.
use File::Find;
$directory_list = @ARGV;
# "-M" abbreviates "time since last modification", while
#    "-d" "... is a directory." 

find ( sub { 
   $modification_lapse{$File::Find::name} = -M if -d $File::Find::name, 
   @directory_list );

for ( sort { 
   $modification_lapse{$a} <=> $modification_lapse{$b} } keys
$modification_lapse) {
    # Tabulate the results in nice columns.
    printf "%5d: %s\n", $modification_lapse[$_], $_;
}
```

Also assume that you adjoin an entry such as this to your crontab:

```
20 2 * * * /usr/local/bin/modified_directories.pl /
```

In this case, each morning you'll receive an email report on the date each directory on your host was last modified. This can be useful both for spotting security issues when read-only directories have been changed (they'll appear unexpectedly at the top of the list) and for identifying dormant domains in the filesystem (at the bottom of the list) that might be liberated for better uses.

## Other Tools

Many other general-purpose scripting languages effectively automate operations. Apart from Perl and Tcl, Python deserves the most attention for several reasons, such as its portability and extensibility.

The next sections describe Python and two other special-purpose tools important in automation: Emacs and procmail.

## Python

Python can be of special interest to Red Hat Linux users. Python is object-oriented, modern, clean, portable, and particularly easy to maintain. If you are a full-time system administrator looking for a scripting language that will grow with you, consider Python. The official home page for Python is http://www.python.org.

## Emacs

Emacs is one of the most polarizing lightning rods for religious controversy among computer users. Emacs has many intelligent and zealous users who believe it to be the ideal platform for all automation efforts. Its devotees have developed what was originally a screen editor into a tool with capabilities to manage newsgroup discussion, Web browsing, application development, general-purpose scripting, and much more. For the purposes of this chapter, what you need to know about Emacs follows:

- It’s an editor that you ought to try at some point in your career.
- If you favor integrated development environments, Emacs can do almost anything you imagine. As an editor, it emulates any other editor, and its developers ensure that it always offers state-of-the-art capabilities in language-directed formatting, application integration, and development automation.

Even if the “weight” of Emacs sways you against its daily use (it may seem slow on startup and can require quite a bit of education and configuration), keep it in mind as a paragon of how sophisticated programming makes common operations more efficient.

> **Note**
>
> The Emacs editor is included with Red Hat Linux. You can use Emacs with or without the X Window System. Type the word `emacs` on the command line of your console or an X11 terminal window and press the Enter key. Run its built-in tutorial by pressing `Ctrl+H` and then pressing the `T` key.

## procmail

The most indispensable, most often used Internet function is email. Can email be automated?

Yes—and it’s perhaps the single best return on your invested time to do so. Along with aliases, distribution lists, startup configurations, and the plethora of mail agents or clients with their feature sets, you’ll want to learn about procmail. Suppose you receive a hundred messages a day, that a fifth of them can be handled completely automatically, and that it takes at least three seconds of your time to process a single piece of email; those are conservative estimates. A bit of procmail automation will save you at least a minute a day, or six hours a year. Even conservative estimates make it clear that an hour of setting up procmail pays for itself many times over.

Along with the `man procmail` pages (`man -k procmail` for a list), serious study of procmail starts with the page http://www.faqs.org/faqs/mail/filtering-faq, Nancy McGough’s Filtering Mail FAQ. This gives detailed installation and debugging directions. You’ll also find information about procmail in the Mail-HOWTO (if you installed the HOWTOs). Because your Red Hat Linux machine will almost certainly have a correctly configured procmail, you can immediately begin to program your personal use of it. As a first experiment, create exactly these files.

1. `~/.procmailrc`, with these contents:

```
VERBOSE=on
MAILDIR=$HOME/mail
PMDIR=$HOME/.procmail
LOGFILE=$PMDIR/log
INCLUDERC=$PMDIR/rc.testing
```

2. `~/.procmail/rc.testing`, holding this code:

```
:0;
* "Subject:"HOT
SPAM:HOT
```

Then run:

```
# chmod 600 ~/.procmailrc ~/.procmail/rc.testing
# chmod a+x ~
```

Now exercise your filter with the following:

```
# echo "This message 1." | mail -s "Example of HOT SPAM." YOUR_EMAIL_NAME
# echo "This message 2." | mail -s "Desired message." YOUR_EMAIL_NAME
```

What you now see in your mailbox is only one new item: the one with the subject Desired message. You also have a new file in your home directory, `SPAM.HOT`, holding the first message.

procmail is a robust, flexible utility you can program to achieve even more useful automations than this. When you gain familiarity with it, it will become natural to construct rules that, for example, automatically discard obvious spam, sort incoming mailing-list traffic, and perhaps even implement pager forwarding, remote system monitoring, or FAQ responding. This can save you considerable time each day.

## Internal Scripts

One more element of the automation attitude is to be on the lookout for opportunities within every application you use. Scripting has become a pervasive theme, and almost all common applications have at least a rudimentary macro or scripting capability. IRC users know about bots, Web browsers typically expose at least a couple of scripting interfaces, all modern PPP clients are scriptable, and even such venerable tools as `vi` and `ftp` have configuration, shortcut, and macro capabilities that enormously magnify productivity. Even the `apm` and `cardmgr` (for PCMCIA cards) can run scripts on certain actions. If you use a tool regularly, take a few minutes to reread its presentation in this volume; chances are you’ll come up with a way to make your work easier and more effective.

## Concluding Challenge for an Automater—Explaining Value

You’ve become knowledgeable and experienced in scripting your computer so that it best serves you. You know how to improve your skills in script writing. You’ve practiced different approaches enough to know how to solve problems efficiently. The final challenge in your automation career is this: How do you explain how good you have become?
