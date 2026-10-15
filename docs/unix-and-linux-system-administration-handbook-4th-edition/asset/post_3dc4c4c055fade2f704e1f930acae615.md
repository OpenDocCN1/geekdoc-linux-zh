
A better paradigm might be

```
# Basic system aliases -- these MUST be present.
mailer-daemon: "/dev/null"
postmaster: root
```

You should redirect root's mail to your site's sysadmins or to someone who logs in every day. The bin, sys, daemon, nobody, and hostmaster accounts (and any other pseudo-user accounts you set up) should have similar aliases.

In addition to a list of users, aliases can refer to

- A file containing a list of addresses
- A file to which messages should be appended
- A command to which messages should be given as input

These last two targets should push your "What about security?" button because the sender of a message totally determines its content. Being able to append that content to a file or deliver it as input to a command sounds pretty scary. Many MTAs either do not allow these targets or severely limit the commands and file permissions that are acceptable.

Aliases can cause mail loops. MTAs try to detect loops that would cause mail to be forwarded back and forth forever and return the errant messages to the sender. To determine when mail is looping, an MTA can count the number of Received lines in a message's header and stop forwarding it when the count reaches a preset limit (usually 25). Each visit to a new machine is called a "hop" in email jargon; returning a message to the sender is known as "bouncing" it. So a more typically jargonized summary of loop handling would be, "Mail bounces after 25 hops." Another way MTAs can detect mail loops is by adding a Delivered-To header for each host to which a message is forwarded. If an MTA finds itself wanting to send a message to a host that's already mentioned in a Delivered-To header, it knows the message has traveled in a loop.

## Getting aliases from files

The include: directive in the aliases file (or a user's .forward file) allows the list of targets for the alias to be taken from the specified file. It is a great way to let users manage their own local mailing lists. The included file can be owned by the user and changed without involving a system administrator. However, such an alias can also become a tasty and effective spam expander, so don't let email from outside your site be directed there. If users outside your site need to send mail to the alias, use mailing list software such as Mailman (covered on page 760) to help keep the system secure.

When setting up a list to use include:, the sysadmin must enter the alias into the global aliases file, create the included file, and chown the included file to the user that is maintaining the mailing list. For example, the aliases file might contain

```
sa-book: include:/usr/local/mail/ulsah.authors
```

The file ulsah.authors should be on a local filesystem and should be writable only by its owner. To be really complete, we should also include aliases for the mailing list's owner so that errors (bounces) are sent to the owner of the list and not to the sender of a message addressed to the list:

```
owner-sa-book: evi
```

See page 760 for more information about mailing lists and their interaction with the aliases file.

## Mailing to files

If the target of an alias is an absolute pathname (double-quoted if it includes special characters), messages are appended to the specified file. The file must already exist. For example:

```
cron-status: "/usr/local/admin/cron-status-messages"
```

It's useful to be able to send mail to files, but this feature arouses the interest of the security police and is therefore restricted. This syntax is only valid in the aliases file and in a user's .forward file (or in a file that's interpolated into one of these files with the include: directive). A filename is not understood as a normal address, so mail addressed to /etc/passwd@example.com would bounce.

If the destination file is referenced from the aliases file, it must be world-writable (not advisable), setuid but not executable, or owned by the MTA's default user. The identity of the default user is set in the MTA's configuration file.

If the file is referenced in a .forward file, it must be owned and writable by the original message recipient, who must be a valid user with an entry in the passwd file and a valid shell that's listed in /etc/shells. For files owned by root, use mode 4644 or 4600, setuid but not executable.

## Mailing to programs

An alias can also route mail to the standard input of a program. This behavior is specified with a line such as

```
autoftp: "|/usr/local/bin/ftpserver"
```

It's even easier to create security holes with this feature than with mailing to a file, so once again it is only permitted in aliases, .forward, or include: files, and often requires the use of a restricted shell.
