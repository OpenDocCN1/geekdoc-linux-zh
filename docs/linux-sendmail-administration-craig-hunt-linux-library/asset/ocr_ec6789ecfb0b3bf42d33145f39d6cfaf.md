# Chapter 11 Stopping Spam

Windows clients that can't run their own Sendmail program. Blocking relaying at the server causes the client to get an error. For example, a client running Netscape Messenger would get a pop-up box saying “An error occurred while sending mail. The mail server responded: Relaying denied. Please check the recipients and try again.” There is nothing wrong with the recipients. What’s wrong is that the user configured the “Outgoing mail SMTP server” with the name of your server, and your server is running the default Sendmail configuration, which denies all relaying.

To create a mail server, you must allow some level of relaying. Use the Sendmail feature that relaxes the relay restrictions just enough to get the job done. Don’t overdo it, or you will open the door to spammers. There are several relay features from which you can choose.

Class R can be used to extend relay services to specific clients. As described in Chapter 6, there are three ways to store hostnames in class R. Individual values can be stored in class R using the RELAY_DOMAIN macro. A file can be loaded into class R either the confRFILE option or the RELAY_DOMAIN_FILE macro. “The relay-domains File” of Chapter 6 for more information about these commands.

Listing 11.2 shows a simple relay-domains file and the effect it has on mail delivery. Listing 11.2 contains output from two different systems. The prompt [ed@ox] shows the mail delivery attempts from the user logged on the system ox.mammals.org before and after changes were made to the configuration of the mail server wren.foobirds.org. The changes made to were are indicated by the [root@w]# prompt. The “Relaying denied” error in the first test is highlighted in bold italic. Lines were deleted to keep the listing to a reasonable length, but everything important is still there.

# Listing 11.2 Enabling Relay with Class R

```
[ed@ox]$ sendmail -jfill@robin.foobirds.org < /dev/null
jill@robin.foobirds.org... Connecting to wren.foobirds.org.
via smtp...
... Lines deleted ...
>>> Mail From:<ed@ox.mammals.org>
250 2.1.0 <ed@ox.mammals.org>... Sender ok
>>> RCPT To:<jill@robin.foobirds.org>
550 5.7.1 <jill@robin.foobirds.org>... Relaying denied
... Lines deleted
>>> QUIT
221 2.0.0 wren.foobirds.org closing connection
```