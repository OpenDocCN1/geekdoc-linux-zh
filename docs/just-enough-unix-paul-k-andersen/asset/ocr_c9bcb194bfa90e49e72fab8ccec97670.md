You will see how to use Mail and Mailx in the next chapter.

# 13.5 Electronic Mail

One of the most popular features of the UNIX operating system is electronic mail (e-mail or E-mail), which allows you to exchange text messages with other users. There are three standard UNIX mail programs:

+   * Original UNIX mailer `mail`. Although superseded by more powerful mail programs, `mail` is still available on most UNIX systems.
+   * Berkeley mail program `Mail`. This program has more features and is easier to use than the original `mail` program.
+   * System V mailer `mailx`. The `x` stands for “extended.” The `mailx` program is based on Berkeley `Mail`.

Of these, the original `mail` program is not often used. (In fact, some systems are set up so that the `mail` command calls up one of the other mailers.) In addition to these standard mail programs, your system may offer a choice of other mailers:

+   * `elm`. Written by Dave Taylor in 1986, the `elm` mailer is a powerful, menu-driven alternative to the standard UNIX mail programs.
+   * `pine`. From the same people who wrote the `pico` text editor, `pine` is intended to be an easy-to-use alternative to `elm`. (The name `pine` stands for “pine is not e.l.m.”)
+   * `RMAIL`. The `RMAIL` program is built into some versions of the `emacs` text editor.
+   * `mh`. Unlike the other mailers listed here, `mh` is actually a collection of programs rather than a single program. It originated at the Rand Corporation, and is especially useful for handling high volumes of mail. A related program called `xmh` provides a graphical interface to `mh` that runs under the X Window System.

# 13.6 Internet Mail Addresses

Whichever mail program you prefer, you need to know how to address mail to other users. An Internet mail address consists of the recipient’s login name, followed by the “at” symbol (@), and the domain name of the recipient’s host computer:

```
obadi ah@fairway.ecn.purdue.edu
```

Here, the login name is `obadi ah`, and the complete domain name for the host computer is `fairway.ecn.purdue.edu`. This is the address that someone outside Purdue University would use to send mail to `obadi ah`. However, a user at Purdue University would not need the entire address. Table 1 shows some of the variations in mailing addresses. The general rule of thumb is this:

> *You may omit those parts of the address that are identical to your own.*