# TABLE 20.3 continued

| Parameter | Description |
| --- | --- |
| pathnews domain | The path to the news binaries, which is already set for your Red Hat system. The complete domain name of your Internet domain. This parameter is blank until you fill it. |
| mailcnd | The command that innd uses to send mail messages. Usually this should be the innmail program. |
| server | The name of a default NNTP server. |
| maxconnections | The maximum number of incoming NNTP connections your server will support, based on your network's bandwidth. |
| fromhost | The domain that the INN system uses to construct email addresses. It should be set to your local system address. |
| moderatmailer | The email address where messages posted to moderated newsgroups are sent if there is no corresponding entry in the moderators file. |
| status | Frequently (in seconds) innd should create a status report. A value of 0 disables this feature. (A value of 0 is not recommended if you want to receive status reports, but it's the default Red Hot setting. Set whatever you feel comfortable with.) |
| timer | How frequently (in seconds) innd should report performance statistics to the logfiles. A value of 0 disables this feature. (A value of 0 is not recommended, but it's the default Red Hot setting. Set whatever you feel comfortable with.) |

The inn.conf file is a text file that you can modify by using any standard text editor. At a minimum, you should ensure that the organization, domain, mailcnd, mta, server, and fromhost parameters are specified. Listing 20.1 shows sample inn.conf file entries for a test server.

# LISTING 20.1 Sample inn.conf Configuration File Entries

| | |
| --- | --- |
| mta: | /usr/bin/sendmail -oi -oem %s |
| organization: | Hoyt's MaximumNews |
| ovmethod: | tradiz |
| domain: | maximumhoyt.com |
| mailcnd: | /usr/bin/innmail |
| status: | 3600 |
| timer: | 3600 |

The sample configuration in Listing 20.1 uses the standard Sendmail MTA for the mailer and the traditional indexed method for and it creates new status reports every hour.