
# Chapter 11. Email

For more information on LDAP, see Chapter 13 Lightweight Directory Access Protocol (LDAP).

## 11.3.2. Fetchmail

Fetchmail is an MTA which retrieves email from remote servers and delivers it to the local MTA. Many users appreciate the ability to separate the process of downloading their messages located on a remote server from the process of reading and organizing them in an MTA. Designed with the needs of dial-up users in mind, Fetchmail connects and downloads all of the email messages to the mail spool using any protocols, including the POP3 and IMAP. It can even forward email messages to an SMTP server, if necessary.

Fetchmail is configured for each user through the use of a .fetchmailrc file in the user's home directory.

Using preferences in the .fetchmailrc file, Fetchmail checks for email on a remote server and pulls it off. If it attempts to deliver it to port 25 on the local machine, using the local MTA to place the email in the correct user's spool. If Proxym is available, it can then be used to fetch the email and place it in a mailbox so it can be read by an MTA.

### 11.3.2.1. Fetchmail Configuration Options

Although it is possible to pass any options on the command line to check for email on a remote server when executing Fetchmail, a .fetchmailrc file is much easier. All of the configuration options go in the .fetchmailrc and it is possible to override them at the time Fetchmail is run by specifying that option on the command line.

A user's .fetchmailrc file is divided into three particular types of configuration options:

- global options — Gives Fetchmail instructions that control the operation or provide settings for every account checks for mail.
- server options — Specifies information about the server being polled, such as the hostname, as well as preferences for a specific email server, such as the port to check or number of seconds to wait before timing out. These options affect every user used with that server.
- user options — Contains information, such as username and password, necessary to authenticate and check for email using a particular server.

Global options appear at the top of the .fetchmailrc file, followed by one or more server options, each of which designate a different server that Fetchmail should check. User options follow server options for each account checking their mail. Like server options, user options may be specified for a particular server as well as to check multiple accounts on the same server.

Server options are called in service of the .fetchmailrc file of a special verb option, poll or skip, which precedes any of the server information. The poll action tells Fetchmail to use this server option when it is run, which actually checks it for email the various user options. User options after a skip action, are not checked unless this server hostname is specified when Fetchmail is invoked. The skip option sets up test configurations in .fetchmailrc and only checks that server when desired, without affecting any working configurations.

A sample .fetchmailrc file looks like this:

```
set postmaster "user"
set bouncemail
poll pop.domain.com proto pop3
user 'user' there with password 'secret' is user here
```

mail.domain.com

```
user 'user5' there with password 'secret2' is user here
user 'user7' there with password 'secret3' is user here
```

In this example, the global options are set so the user is sent as a last resort (postmaster option) and all errors are sent to the postmaster of the sender (bouncemail option). The set action tells Fetchmail this line contains a global option. Then, two servers are specified, one set to check using POP3, other for trying various protocols to find which. Two users are checked using the second server option, but all email sent to user's mail pool. This allows multiple mailboxes to be checked on multiple servers, while appearing in a single MUA inbox. Each user's specific information begins with the user action.

# Note

Users are not required to place their password in the .fetchmailrc file. Omitting the password <password> section causes Fetchmail to ask for a password when it is launched.

Fetchmail contains many global, server, and local options. Many of these options are rarely used or only apply to very specific situations. The fetchmail page explains each option in detail, but the most common ones are listed here.

## 11.3.2. Global Options

Each option should be placed on a single line after a set action.

- daemon <seconds> — Specifies daemon-mode, where Fetchmail stays in the background and polls for mail at the interval specified.
- postmaster — Specifies a local user to send mail in case of delivery problems.
- syslog — Specifies the log for errors and status messages. By default, this is /var/log/mailog.

## 11.3.3. Server Options

Server options should be placed on their own line in .fetchmailrc after a poll or skip action.

- auth <auth-type> — Specifies the type of authentication to use. By default, password authentication is used, but protocols support other types of authentication, including kerberos_v5, kerberos_v4, and ssh. If any authentication is used, Fetchmail tries methods that do not require a password, then methods mask the password, and finally attempts to send the password unencrypted to the server.
- interval <number> — Polls the specified server every <number> times that it checks for all configured servers. This option is used for mail servers where the user rarely receives messages.
- port <port-number> — Overrides the default port.
- proto <protocol> — Specifies a protocol, such as pop3 or imap, to check for messages.
- timeout <seconds> — Specifies the interval of server inactivity after which Fetchmail gives up on a connection attempt. If this value is not set, a default of 300 seconds is assumed.

## 11.3.2.4. User Options

User options may be placed on their own line beneath a server option or on the same line as the server option. In either case, the defined options must follow the user option (defined below).

- fetchall — Orders Fetchmail to download all messages in the queue, including messages that have already been viewed. By default, Fetchmail only pulls new messages.
- fetchlimit <number> — Only allows a certain number of messages to be retrieved before stopping.
- flush — Tells Fetchmail to delete all previously viewed messages in the queue before retrieving new messages.
- limit <max-number-bytes> — Specifies that only messages below a particular size may be retrieved. This is useful with slow network links, when a large message takes too long to download.
- password <password> — Specifies the password to be used for this user.
- preconnect `<command>` — Executes the specified command before retrieving messages for this user.
- postconnect `<command>` — Executes the specified command after retrieving messages for this user.
- ssl — Activates SSL encryption.
- user `<username>` — Sets the username by Fetchmail to retrieve messages. This option should be listed before any other user options.

## 11.3.2.5. Fetchmail Command Options

Most Fetchmail may be used on the command line, when executing the .fetchmailrc configuration options. Most users will not use it with a configuration file. Most will not use these options on the command line, as it is easier to leave them in the .fetchmailrc file to be used when Fetchmail is run.

However, there may be times when it is desirable to run the fetchmail command with other options for a particular purpose. It is possible to issue command options to temporarily override a .fetchmailrc setting that is causing an error, as any options specified at the command line override configuration files.

## 11.3.2.6. Informational or Debugging Options

Certain options used after the fetchmail command can supply important information.

-- config — Displays every possible option based on information from .fetchmailrc and Fetchmail defaults. No email is retrieved for any users using this option.
- -s — Executes Fetchmail in silent mode, preventing any messages, other than errors, from appearing after the fetchmail command.
- -v — Executes Fetchmail in verbose mode, displaying every communication between Fetchmail and the remote servers.
- -V — Displays detailed version information, lists its global options, and shows settings to be used with each user, including the email protocol and authentication method. No email is retrieved for any users using this option.
