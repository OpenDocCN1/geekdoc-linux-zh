pom, and you want to know what it does. You can type man -f pom to get a short, one line description. In this case, the result is

```
pom(6) - display the phase of the moon
```

As in the full man page, the number in parenthesis tells you what category of the man pages this command is in. As you might remember, category 6 is games.

You can also search for commands based on their summaries. The short descriptions of commands are stored in what is known as the whatis database. To search this database for a command that has to do with "mail," you might use the apropos mail command (equivalent to man -k mail):

```
# apropos mail
biff(1)      - be notified if mail arrives and who it is from
forward(5)   - mail forwarding instructions
from(1)      - print names of those who have sent mail
mail(1)      - send and receive mail
mail.local(8) - store mail in a mailbox
mailaddr(7)  - mail addressing description
mailq(1)     - print the mail queue
smrsh(8)     - restricted shell for sendmail
```

You can also use the whatis command to search only for whole-word matches. For instance, whatis mail (or man -f mail) would have returned a list like the one shown here, but without the smrsh entry.

# The GNU Info System

As you might have already figured out, the man pages are rather obtuse and often seem to be written for users who probably don't need them. New users often don't find the man pages very useful. Because of this, the GNU project came up with the info system.

The info system works similar to the man pages except that info pages are usually much more detailed and helpful to new users.

To read an info page, simply type info followed by the name of the command. Note that not all commands have info pages. If you request an info page for a command that does not have an info page, info will load the man page for that command instead.

Like the man page viewer, you can use the Page Up or Page Down keys, the arrow keys, and the spacebar to navigate through the info page. However, the info system also supports hyperlinks similar to links in Web pages. To use them, simply use the arrow keys to move the cursor over a link and then press the Enter key.