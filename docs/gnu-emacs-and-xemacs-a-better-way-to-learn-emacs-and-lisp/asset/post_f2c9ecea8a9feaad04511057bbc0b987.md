
![](img/c8827ea52a0796def3f6891892ed9d3a_403_0.png)

Figure 18.9 Customizing Gnus

## Selecting a Mail Back End

Gnus doesn't have a single method of processing mail messages; it has several, each of which has advantages and drawbacks. Some are more appropriate for users who have much free disk space, and others are more efficient if you have large quantities of mail. Before you begin using Gnus for mail, you need to decide on one of these back ends.

These back ends differ mainly in the method used to store messages. The Summary and Article buffers introduced in the news-reading sections of this chapter are for the most part identical whether you're reading news or reading mail with any of the back ends. All the commands described earlier can be used with mail messages too.

### Storing Mail on a Local Spool

The nnml back end is modeled on the way news servers store articles. The messages are split, one file per message, and are deposited in one or several directories. An active file and an overview file (similar to files that news servers use) provide an index that Gnus can use to quickly get at a particular message.

The drawback of nnml is that it uses many inodes, which are pointers used by the Linux ext2 filesystem to identify a file and its location on the hard disk. Each file uses one inode. Each filesystem has a limited number of inodes, which raises the dreaded specter of running out of them. This should be of concern to you only if you have vast quantities of mail or if you are on a shared filesystem administered by someone else.

This back end is a little slower when Gnus is absorbing a quantity of new mail, because the mail has to be split into its constituent messages and distributed to directories.

For many Gnus users, especially those unconcerned with maintaining compatibility with standard e-mail clients, nnml is the back end of choice.

### Using an MH-Style Spool

The nnml back end was developed for users accustomed to the venerable MH mail-handling system developed years ago at RAND. It is a lot like nnml but without the rapid message access provided by index files. Use this if you are accustomed to such systems and want to maintain compatibility; otherwise, any of the other back ends is preferable.

### The UNIX Mailbox Format

If you like the traditional mailbox format used by many other e-mail programs, the nnmbox back end should suit you. All messages are stored in one big file. Gnus can append new mail to such a file very quickly, but finding a message is slower than with nnml, because the whole file has to be searched for header identifiers. You might use this back end if it is important to you to be able to read the mailbox files with a traditional mailer such as Mutt or Pine.

### Mail Folders

nnfolder is like a hybrid between the nnml mail spool approach and the single-file nnmbox back end. Mail is kept in several mailbox-style files, but each mail group you have set up gets its own file. Searching for a message is faster than with the nnmbox back end, partly because the files tend to be smaller. An active file is maintained; this provides some indexing for your mail.

### The Rmail (Babyl) Format

Rmail users (but probably few others) might be interested in keeping their Gnus mail in Rmail’s native format. This is another “one big file” back end like nnmbox, so performance is similar.

## Informing Gnus

You can set up a mail back end either by writing Lisp in your `~/.gnus` file or by opening a Customize buffer and entering your choice there.

The following is a sample Lisp statement that can be adapted to your situation. It sets up a new secondary select method; the primary one is your news server. Substitute nnnbox or any of the other mail back ends for nnml in this expression if you like:

```lisp
(setq gnus-secondary-select-methods
      '((nnml "")))
```

## Mail Sources

Now for some Lisp that tells Gnus where your mail folders are. The first could be used to fetch mail from a POP server that requires a username and password:

```lisp
(setq nnmail-spool-file
      '(pop :server "pop3.mailserver.com" :user "myname"))
```

If you prefer to use a non-Emacs method of retrieving your mail (such as Fetchmail), all you need is a statement like this:

```lisp
(setq nnmail-spool-file
      '(file :path "/var/spool/mail/user"))
```

Perhaps you use procmail to split your mail into files depending on the contents of the message header. In that case, point Gnus at the directory with a statement patterned after this one:

```lisp
(setq nnmail-spool-file
      '(directory :path "/var/mail"))
```

You can list more than one mail source in an `nnmail-spool-file` variable definition. For example, the preceding statements could be combined. This would tell Gnus to gather mail from both the single mailbox file and the files in the directory:

```lisp
(setq nnmail-spool-file
      '((directory :path "/var/mail")
        (file :path "/var/spool/mail/user")))
```

Make sure you keep the parentheses balanced in a statement like this.

## Splitting Mail

Many e-mail users appreciate the convenience of having mail separated into folders categorized by subject or origin. Procmail used in conjunction with Fetchmail is a popular means to this end on Linux systems. Gnus can do this as well, using a regular-expression-matching scheme similar to the one Procmail uses.

Here is an example that creates several new mail groups:

```lisp
(setq nnmail-split-methods
 '(("kernel" "Sender:.+linux-kernel.*")
    ("family" "From:.*Ayers.*")
    ("xemacs" "X-Mailing-List:.+xemacs-beta.*")
    ("misc" ".*")))
```

The last group (misc) should always be present, because it is the catchall group where mail that didn't pass the first three tests ends up. If you leave it out, you might lose mail. Maybe Gnus would save the messages somehow, but I don't feel inclined to run a test!

Each item in this list of splits is a two-element list. The first part is the name you want the group to have, and the second part is a regular expression that is intended to match one of the header lines in a message.

Here is an English translation of the regular expression in the next-to-last item:

> Any message that has at the beginning (^) of a header the characters "X-Mailing-List:," followed by a single character (the period matches a space), followed by zero or more characters (*), followed by "xemacs-beta," followed by zero or more characters (*)

Sometimes it takes some experimentation to come up with a regular expression that matches every message you think it should. You can examine the header lines in an e-mail message by opening it directly in Emacs (not using a mail mode such as Gnus), or by simply pressing t in an Article buffer. Look at several messages from the source you are trying to filter, and try to find a header line that is common to all of them but distinctive enough that other messages won't match as well.

This is just the tip of the iceberg when it comes to Gnus splitting mail. See the "Fancy Mail Splitting" section of the Gnus Info manual for interesting but complex mail-splitting esoterica.

## Expiring Mail

You can tell Gnus to expire messages in certain mail folders, in which case messages are deleted a week after you receive them. This time lag can be changed with a Lisp statement like this:

```lisp
(setq nnmail-expiry-wait 9)
```

You can also change this variable in the nnmail-expire Customize group.

You can manually expire a message at any time by pressing E in the Summary buffer. If it’s a big file and you want to dispose of it at once rather than wait until the expiration happens, just press B Delete.

The following Lisp statement can be used as a template to fine-tune expiration periods for several mail folders. Check your parentheses well!

```lisp
(setq nnmail-expiry-wait-function
      (lambda (group)
        (cond
         ((string= group "family") 60)
         ((string= group "junk") 1)
         ((string= group "main") 'never)
         (t 9))))
```

This chunk of Lisp creates a lambda (nameless) function, the main body of which is a conditional statement that says if the string “family” matches a mail folder’s name, wait 60 days before expiring the messages. The expiry action to take with the main folder is never, which disables expiry completely for that folder. Don’t forget the single quote before never, because it prevents the Lisp interpreter from trying to make sense of the word. It needs to be passed unaltered to Gnus. Another valid entry rather than an integer or the word never is immediate, which signals Gnus that you want all messages in a folder expired right now.

## Attachments and MIME

All you need to do to attach a file to an outgoing message is press Ctrl-c Ctrl-a (or use the menu). You are asked for a file name (Tab completion comes in handy) and a MIME type. A default type is suggested.

When you receive a message with a MIME attachment, Gnus should know what to do with it. If you’d rather use external viewers for images, or if you need to have a certain type of MIME type passed to another application, you can use keyboard commands.

The MIME-related commands are numerous, but these few will handle most of your needs:
