A configuration file outside of /etc/sendmail.cf is usually stored as a straight text file but then converted into a database format so that Sendmail can refer to it quickly.

There are very few binaries related to Sendmail. The server application itself is a single file called sendmail and is located at /usr/sbin/sendmail. It should be started at boot time through a startup script, as described in Chapter 7.

Sendmail comes with a few peripheral programs such as smrsh, which can really help your day-to-day sysadmin operations. The smrsh tool has especially notable features.

As we’ve seen, Sendmail is one very powerful program that can handle some remarkable configurations. Take advantage of its flexibility and let only your creativity limit what you do with it.