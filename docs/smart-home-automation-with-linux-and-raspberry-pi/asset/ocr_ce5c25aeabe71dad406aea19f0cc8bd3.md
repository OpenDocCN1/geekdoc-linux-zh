determine, because the use of POP3 means you will no longer see the ads on their web pages. But when it is available, it is usually found in the settings part of the service. All of the major companies provide this service, although not all are free.

+   - Hotmail provides POP3 access by default, making it unnecessary to switch on, and after many years of including this only on its subscription service, now Hotmail provides it for free. The server is currently at `pop3.live.com`.
+   - Google Mail was the first to provide free POP3 access to e-mail, from `pop.gmail.com`. Although now most accounts are enabled by default, some older ones aren’t. You therefore need to select Settings and Forwarding and POP/IMAP. From here you can enable it for all mail or any newly received mail.
+   - Yahoo! provides POP3 access and forwarding to their e-mail only through its Yahoo! Plus paid-for service. A cheat is available on some services (although not Yahoo!) where you forward all your mail to another service (such as Hotmail or Gmail) where free POP services are available!

Previously, there was a project to process HTML mail directly, eliminating the need to pay for POP3 services. This included the now defunct `http://httpmail.sourceforge.net`. Such measures are (fortunately) no longer necessary. Once you know the server on which your e-mail lives, you can download it. This can be either for reading locally, for backup purposes, or for processing commands sent in e-mails. Although most e-mail software can process POP3 servers, I use getmail.

```
```sh
apt-get install getmail4
```
```

I have this configured so that each e-mail account is downloaded to a separate file. I’ll demonstrate with an example, beginning with the directory structure:

```
```sh
mkdir ~/.getmail
mkdir ~/externalmail
touch ~/externalmail/gmail.mbox
touch ~/externalmail/hotmail.mbox
touch ~/externalmail/yahoo.mbox
```
```

and then a separate configuration file is created for each server called `~/.getmail/getmail.gmail`, which reads as follows:

```
```ini
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = my_email_address@gmail.com
password = my_password

[destination]
type = Mboxrd
path = ~/externalmail/gmail.mbox

[options]
verbose = 2
message_log = ~/.getmail/error.log
```
```

If you’d prefer for them to go into your traditional Linux mail box, then you can change the path to the following:

```
```sh
path = /var/mail/steev
```
```