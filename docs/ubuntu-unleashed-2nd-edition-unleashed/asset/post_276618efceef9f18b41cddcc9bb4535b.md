
an MTA (see the following note), but does not handle deliveries between systems and does not provide an interface to the user.

## NOTE

Procmail or Spamassassin are examples of MTAs; both provide filtering services to the MTA while they store messages locally and then make them available to the MUA or email client for reading by the user.

The MDA uses the POP3 or IMAP protocols for this process. In a manner similar to a post office box at the post office, POP3 and IMAP implement a “store and forward” process that alleviates the need to maintain a local mail server if all you want to do is read your mail. For example, dial-up Internet users can intermittently connect to their ISP’s mail server to retrieve mail using Fetchmail—the MDA recommended by Ubuntu (see the section “Using Fetchmail to Retrieve Mail” later in this chapter).

## The Mail User Agent

The mail user agent, or MUA, is another necessary part of the email system. The MUA is a mail client, or mail reader, that allows the user to read and compose email and provides the user interface. (It is the email application itself that most users are familiar with as “email.”) Some popular UNIX command-line MUAs are elm, pine, and mutt. Ubuntu also provides modern GUI MUAs: Evolution, Thunderbird, Mozilla Mail, Balsa, Sylpheed, and KMail. For comparison, common non-UNIX MUAs are Microsoft Outlook, Outlook Express, Pegasus, Eudora, and Netscape Messenger.

The Microsoft Windows and Macintosh MUAs often include some MTA functionality; UNIX does not. For example, Microsoft Outlook can connect to your Internet provider’s mail server to send messages. On the other hand, UNIX MUAs generally rely on an external MTA such as Sendmail. This might seem like a needlessly complicated way to do things, and it is if used to connect a single user to her ISP. For any other situation, however, using an external MTA allows you much greater flexibility because you can use any number of external programs to handle and process your email functions and customize the service. Having the process handled by different applications gives you great control over how you provide email service to users on your network, as well as to individual and small office/home office (SOHO) users.

For example, you could do the following:

- Use Evolution to read and compose mail
- Use Sendmail to send your mail
- Use xbiff to notify you when you have new mail
- Use Fetchmail to retrieve your mail from a remote mail server
- Use Procmail to automatically sort your incoming mail based on sender, subject, or many other variables
- Use Spamassassin to eliminate the unwanted messages before you read them

## Basic Postfix Configuration and Operation

Because Postfix is the Ubuntu-recommended MTA, the following sections provide a brief explanation and examples for configuring and operating your email system. As mentioned earlier, however, Postfix is an extremely complex program with many configuration options. As such, this chapter only covers some of the basics. For more information on Postfix, as well as other MTAs, see the "Reference" section at the end of this chapter.

Postfix configuration is handled by files in the /etc/postfix directory with much of the configuration being handled by the file main.cf. The actual syntax of the configuration file, main.cf, is fairly easy to read (see the following example):

```
# See /usr/share/postfix/main.cf.dist for a commented, more complete version
# Debian specific: Specifying a file name will cause the first
# line of that file to be used as the name. The Debian default
# is /etc/mailname.
#myorigin = /etc/mailname

smtpd_banner = $myhostname ESMTP $mail_name (Ubuntu)
biff = no

# appending .domain is the MUA's job.
append_dot_mydomain = no

# Uncomment the next line to generate "delayed mail" warnings
#delay_warning_time = 4h

# TLS parameters
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_use_tls=yes
smtpd_tls_session_cache_database = btree:${queue_directory}/smtp_scache
smtpd_tls_session_cache_database = btree:${queue_directory}/smtp_scache

# See /usr/share/doc/postfix/TLS_README.gz in the postfix-doc package for
# information on enabling SSL in the smtp client.

myhostname = optimus
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
```
