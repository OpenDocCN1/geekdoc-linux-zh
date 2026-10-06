# Part V ♦ Running Servers

+   7. Next, Exim needs to be configured to deliver messages using Maildrop. Use your preferred text editor to open /etc/exim4/update-exim4.conf and adding the following line at the end of the file:
dc_localdelivery='maildrop_pipe'

+   8. Tell Exim to load the most recent configuration change:

```
# invoke-rc -d exim4 reload
```

+   9. Finally, install Courier IMAP and Courier POP:
# apt-get install courier-imap courier-pop

Select "no"' when asked whether or not the installer should create directories for Web-based administration.

Your system should now be capable of receiving messages. You should also be able to connect to your server using a mail client such as Thunderbird or Evolution. This is a good time to test mail delivery, even if you're planning to follow the directions in the next section to enable virus and spam filters. More information about configuring a mail client to connect to your server can be found in the "Configuring Mail Clients" section in this chapter.

# Installing ClamAV and SpamAssassin

Installing and configuring the virus and spam filtering mechanisms is more involved than installing Exim and Courier, but should still go smoothly as you follow the steps carefully. Keep in mind, however, that this will add a lot of complexity to the system, it is a good idea to make sure the Exim mail server is working first so that you don't have many things to check if the system doesn't work expected.

> The version of ClamAV included with Debian 3.1 (aka "Sarge") uses an older virus-scanning engine. Because the updated engine is not likely to make it into an update time some years because of the Debian upgrade policies, a group of developers have created special sets of ClamAV packages that are designed for easy installation on Sarge. For more information about how to use these packages instead of the stock versions, see http://volatile.debian.net/. You may choose to do this from the start, or to add the appropriate URIs to your APT configuration and do an upgrade. In either case, the configuration process detailed in this section will be the.

Here's how to install ClamAV and SpamAssassin, and then configure Exim to use them for scanning messages:

+   1. Install the ClamAV and SpamAssassin packages:
# apt-get install clamav-daemon clamav-testfiles \ spamassassin spamc