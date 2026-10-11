# **Mailing Lists**

Several mailing lists are available on the subject of Linux. Some of these are generic while others apply to a specific distribution.

You can join a mailing list mirror of `comp.os.linux.announce` by sending email to `Linux-Announce-Request@NEWS-DIGESTS.MIT.EDU` with the word `subscribe` in the body of the message. Sending an empty message to the same address will get you help on using the mailing list (including instructions on how to leave).

There are several Linux mailing lists hosted at `major@dombo@ver.rutgers.edu`. Send a message with the word `lists` in the body to find out what lists are available. Sending a message with the word `help` will get you instructions for subscribing and unsubscribing to the lists. Most of these lists are technical and are not intended for new users' questions.

Be sure to follow the rules of Net etiquette. Don't pose a question to a newsgroup or mailing list until after you have researched it. Often your question has already been posed and answered. Check the documentation (HOWTOs, FAQs, and man pages) first, then check the archives at `http://www.deja.com/` before you post.

If you do post, include as much relevant information about your system and your problem as possible, such as general information on the version(s) of your software and a brief summary of your hardware configuration. Learn to appreciate the value of hacking your system, and how to fix problems yourself.

# **Searching for Information**

There are many other ways to find information about commands when you need help. Some of the most frequently used commands are `whereis`, `whatis`, `which`, and `apropos`.

# **whereis**

The `whereis` command is used to find files but also will show you the location of the file's binary, source files, and any associated manual pages. One limitation of `whereis` is that the search is limited to known directories that are coded into the program. Its syntax is

```
```
whereis [options] filename
```
```

If you wanted to see where to find `passwd` or its related man pages, you would type

```
```
whereis passwd
```
```

`passwd: /usr/bin/passwd /etc/passwd /etc/passwd.OLD /usr/man/man1/passwd.1 /usr/man/man5/passwd.5`