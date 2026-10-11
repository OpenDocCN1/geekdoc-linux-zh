At this point, you have a fresh installation of Qpopper that is ready to be populated with new POP3 users. The next section explains how to do just that.

# Using the Qpopper Software

As you add new users to your server, you also need to allow them to use APOP authen-tication to your POP3 server. This requires an entry in `/etc/pop.auth` for each new user. To add these entries, simply issue a `popauth` command like

```
```
[ramon]$ sudo popauth -user ramon
Changing only APOP password for ramon.
New password: mysecret
Retype new password: mysecret
```
```

Note that this example used the `sudo` command to run `popauth` as root, but in fact, the command could have been executed by user `pop` as well. If you need to revoke a user's POP3 access, simply delete that user from the database using the following command:

```
```
[ramon]$ sudo popauth -delete ramon
```
```

Once users have been added to `/etc/pop.auth`, they can change their own passwords, invoking the `popauth` utility as their own user, with no command-line options, as follows:

```
```
[ramon]$ popauth
Changing only APOP password for ramon.
Old password: mysecret
New password: newsecret
Retype new password: newsecret
```
```

This section discussed the POP3 protocol, its security shortcomings, and how you can get around them. The next section discusses the implementation of the IMAP proto-col, an alternative to POP3 that is gaining a great deal of popularity in the Linux server community.

# IMAP

While POP3 is still the most popular mail-retrieval protocol, one of its fundamental short-comings is the fact that messages have to be downloaded to the user's computer (the cli-ent) in order to have access to them. This makes it difficult for the user to select which messages they want to see before actually downloading them. It also makes it a challenge to read mail from multiple clients, while still keeping the mailbox in sync. The Internet Mail Access Protocol (IMAP) was developed in Stanford University circa 1986 to address

Application Security

PART 3