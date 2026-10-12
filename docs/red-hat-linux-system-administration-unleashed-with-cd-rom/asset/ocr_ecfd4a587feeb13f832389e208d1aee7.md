```
# smtp/tcp
    fail_if_error,        # non-inet literals are
# errors
    check_for_local       # check for local host

# match-inet-hosts - match hosts in the TCP/IP network database
#
# On the mail hub we always want to use bind for host lookup
match-inet-hosts:
    driver=bind,          # match hosts on network
    transport=smtp;       # delivery is over smtp/tcp
    domain = mydomain.com # strip trailing domain
# before lookup
```

# Transports File

The smail documentation describes the transports configuration file. However, in a pure SMTP environment it is extremely unlikely that you will ever need one.

# Running smail

smail implements many of the same command-line options as sendmail. This is deliberate policy on the part of the authors so that other programs, such as majordomo, should not need to know which MTA is being run.

# Qmail

Qmail is intended as a smaller, simpler replacement for sendmail+MH. Because the extra complication of running MH or fetchmail or something of that kind is generally unnecessary, qmail is, to a certain extent, shooting at a target that is no longer there.

# Qmail Delivery Options

Qmail has its own way of delivering mail to local users. There are actually three different ways of dealing with it. MAILDIR format puts the mail in ~/Mail/ with each message in a separate file. This is a Good Thing from the point of view of avoiding file-locking issues, but a Bad Thing from the point of view of the MUA, which has to be patched to recognize this format. Patches are available for many popular MUAs. The second format is MAILFILE. Here the mail is all put into one file in the user's home directory, for example, ~/mbox. Many MUAs can read this format with no more than a command-line option to tell them where to look, but there are contention issues if you have two or more MUAs running at once. The contention problem clearly vanishes if your MUA uses POP or IMAP to