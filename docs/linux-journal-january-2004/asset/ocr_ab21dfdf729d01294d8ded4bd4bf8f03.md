skipping any quoted material.

# Reading Mail

In Emacs, read and reply to your incoming mail with rmail mode (M-X rmail) (Figure 6). You may want to create a summary buffer or automate it by modifying the rmail mode hook. This creates a buffer familiar to most users: one line per message with the date, source e-mail address, data size and subject. As you can see in Figure 7, the message in the rmail buffer is highlighted in green. The normal Emacs navigation keys work in the summary buffer.

![](bbox=[0.07, 0.26, 0.45, 0.38])

Figure 6. An E-mail Message in rmail Mode

![](bbox=[0.07, 0.41, 0.45, 0.58])

Figure 7. rmail Mode with a Summary

Emacs mail operates in a somewhat convoluted way in order to accommodate multiple operating systems. When you start an rmail buffer, it moves mail from your inbox file, typically in /var/spool/mail on Linux, into a file, ~/RMAIL. This is the file you normally edit. You can put e-mail into ~/RMAIL at any time with the G key. If you have a POP or IMAP account, try using fetchmail to put your mail in the inbox.

Emacs uses the Babyl mail file format. You can export individual messages as text files; entire rmail files can be exported in mailbox format.

Most mail readers use multiple mail files (directories, if they use maildir mail format). Emacs can shift from one rmail file to another, but you may not need to. Instead, you can create customized summaries using regular expressions and other search patterns. You can specify summaries based on recipients, a regular expression search within the subject or labels.

You can have multiple rmail files and associate each one with one or more inboxes. This means that folks with spam filters, such as SpamAssassin, already running or using procmail recipes to deliver their e-mail to separate files need not abandon that investment. Each time you visit an rmail file, Emacs gets any new mail from the associated input files.

You can reply and forward e-mail in rmail mode. Either

one opens up a mail mode buffer with the e-mail headers already completed. You can use Ctrl-C Ctrl-Y to yank in the message to which you are replying. If you want to reply to multiple e-mails, switch to the rmail buffer, select a different message, switch back and yank the new current message. To be RFC-compliant, you will have to set the quoting character by customizing mail-yank-prefix to use the string >.

Charles Curley (www.charlescurley.com) teaches Linux at two Wyoming colleges. He also writes software and articles and books, using open-source software tools such as Emacs.

# RESOURCES

Author's .emacs:
www.charlescurley.com/~ccurley/emacs.init.html

Emacs Beginner's HOWTO: www.tldp.org/HOWTO/Emacs-Beginner-HOWTO.html, or possibly already on your computer with the rest of the LDP docs.

Emacs' Built-in Help System: Ctrl-H

Emacs for Vi Users: grok2.tripod.com

"Emacs: the Free Software IDE", by Charles Curley, LJ June 2002: www.linuxjournal.com/article/5765

Emacs Wiki: www.emacswiki.org/cgi-bin/wiki.pl

fetchmail: www.catb.org/~esr/fetchmail

"Getting Started with Emacs", by Charles Curley, LJ, March 2003

GNU Emacs Home Page: www.fsf.org/software/emacs/emacs.html

GNU Emacs Lisp Reference Manual: www.gnu.org/manual/elisp-manual-20-2.5/elisp.html

GNU Emacs Tutorial (Old, but Still Useful): www.futureone.com/~sponge/tutorial/emacs/index.html

How do I make common modifications to my Gnu Emacs .emacs file? www.yak.net/fqa/124.html

Procmail: www.procmail.org

Programming in Emacs Lisp: An Introduction, by Robert J. Chassell: www.gnu.org/manual/emacs-lisp-intro/emacs-lisp-intro.html

SpamAssassin: spamassassin.org

Tips—emacs "Nifty ways to get your work done in /the/ editor": www.portico.org/index.php?catList=28

"very unofficial .emacs home", by Ingo Koch: www.dotemacs.de