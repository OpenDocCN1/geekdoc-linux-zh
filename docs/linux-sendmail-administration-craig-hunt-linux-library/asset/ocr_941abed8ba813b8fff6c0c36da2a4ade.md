# The Generic Linux Configuration

The challenge in Chapter 4, "Creating a Basic Sendmail Configuration," was to find or create sendmail.cf file that is compatible with Sendmail 8.11. Because the Sendmail 8.11 distribution comes with a file generic-linux.cf that is already in the proper format to be as a sendmail.cf file, the first thing we tried to use the generic-linux.cf file without modification. The result was this error:

```
[root]# sendmail -v -t -C:/generic-linux.cf
./generic-linux.cf: line 66: fileclass:
  cannot open '/etc/mail/local-host-name'
  : No file or directory
```

The generic-linux.mc file that created the generic-linux.cf file has only five significant commands lines:

# **Listing 5** The Commands Contained in generic-linux.mc

```
[craig$ tail -5 generic-linux.mc
VERSIONID$id: generic-linux.mc,v 8.1 1999/09/24 22:48:05 gshapiro Exp $'
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

We know that the VERSIONID macro has no effect other than holding user-defined version control information. We also know that the OSTYPE macro and the two MAILER macros are required for a functioning system. This leads us to guess that removing the DOMAIN macro is the best place to start attacking the problem. Therefore, in Chapter 4 we created a simple m4 configuration file that used it to produce a sendmail.cf file compatible with Sendmail 8.11. It worked, and got Sendmail up and running.

Sometimes a quick solution based on an educated guess is all that you have time for. When you get some free time you are drawn back to the problem to find out why your guess worked and figure out if there is a better long-term solution to the problem. We need to know more about the macro sources called by the generic-linux.mc file in order:

+   - find out how the simple change worked for our problem
- see if there is a better way to solve our problem
- find out what features were lost by our quick and dirty solution
- learn more about configuring Sendmail