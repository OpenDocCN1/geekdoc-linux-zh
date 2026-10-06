You'll be asked a number of questions about how ClamAV should be configured. Here's how to answer them:

+   **Virus update method** — This is the method that freshclam (part of ClamAV) will use to download updated databases. The recommended option is to run freshclam as a daemon.

+   **Local database mirror site** — This is the site that freshclam will retrieve the virus information updates from. The second part of the site is the two-letter country code. Select your country code or that of a nearby country if yours isn't available.

+   **HTTP proxy information** — Do not enter anything here unless you are required to use a proxy server to access Web servers. If your connection is suitable for running a mail server, you probably don't need to use a proxy server.

+   **Notify clam after updates** — Select "yes”

2. Add the clamav to the Debian-exim group and restart the ClamAV daemon. This allows ClamAV access to read the files in Exim's mail queue:

```
# gpasswd -a clamav Debian-exim
# invoke rc-d clamav-daemon restart
```

3. Replace the report template used by SpamAssassin with one that will fit better in a message header. Use a text editor to add these lines to the end of /etc/spassassin/local.cf:

```
clear_report_template
YES_NO, score=SCORE_, required=REQD, summary=
report_SUMMARY_
```

4. Configure the SpamAssassin background daemon to run automatically and not to attempt to create preferences for users. Change the following options in /etc/default/spamassin:

```
ENABLED=1
OPTIONS="--max-children 5*
```

5. Start the SpamAssassin daemon:

```
# invoke rc-d spamassin-start
```

6. Create the entries that will be included in Exim's ACL (Access Control List) for scanning message data. Use a text editor to create a file named /etc/ex4/acl_check_data_local that contains the following:

```
deny message = $malware_name detected in message
demime = *
malware = *
```