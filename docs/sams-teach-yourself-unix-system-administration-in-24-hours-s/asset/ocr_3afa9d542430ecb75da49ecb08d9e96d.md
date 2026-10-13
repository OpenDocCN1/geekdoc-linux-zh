Having said that, it’s important to state that we are not going to dig into the famously complicated sendmail.cf configuration file. An arcane language unto itself, typical sendmail.cf files can be huge. The default size of this file in Red Hat Linux is 1,490 lines, in Mac OS X it’s 1,214 lines, and on Solaris 8 it’s 1,191 lines. If you must learn more, I suggest you check out the book sendmail (O’Reilly), by Brian Costales and original sendmail programmer Eric Allman.

Alright, so what are we going to cover? How to work with and use sendmail and its powerful alias facility to ensure that your users have a pleasant and painless e-mail experience, day in and day out.

Here’s what you’ll learn this hour:

+   - Using sendmail to test mail connectivity
+   - Mail logs and mail queues
+   - Creating sendmail aliases
+   - sendmail aliases within Mac OS X

# Testing Mail Connectivity with sendmail

A logical place to start exploring the complexities of sendmail, where you’re essentially in a maze of twisty passages, is to learn how to use the sendmail flags to test mail connectivity for your server.

![](bbox=[0.22, 0.8, 0.32, 0.88])

> The twisty passage bit is a reference to the great 70s Adventure program, written in Fortran for Unix. The first interactive fiction game that I ever played, it has been an inspiration for generations of cool D&D-style games since.

# Task 20.1: Using sendmail to Verify Connectivity

The sendmail program has a wide variety of flags, most of which start with b or o if they’re to be used when the program runs as a daemon. Commonly, you’ll see options like -bd to run in daemon mode, -bp to print the mail queue, and -bi to initialize the alias database.

```
# sendmail -bg -d0.1 < /dev/null
Version 8.11.6
```