# RECOMMENDATIONS

We recommend that you run `tiger` on newly installed systems to identify anything that needs to be hardened prior to putting them in a production environment. Also run `tiger` regularly on running systems to look for changes. Tune `tiger` first by running it several times from the command line until your configuration is set as you like it to be and you have made any necessary system changes. Then install and run `tiger` via `tiger.cron`. Run additional audit tools such as `tripwire`. Protect your log files and use a secure server or read-only media if possible.

# SUMMARY

We attempted to cover many configuration options of the `tiger` scripts. `tiger` is a complex set of scripts and programs but can help bring fundamental system vulnerabilities to your attention.

# FOR FURTHER READING

+   1. Farrow, Rik, UNIX System Security: How to Protect Your Data and Prevent Intruders, Reading, Massachusetts, Addison-Wesley, 1991.

# Mailing List for `tiger`

To subscribe to the `tiger` mailing list, send e-mail to `tiger-request@net.tamu.edu` with the subject `subscribe`.

# `sendmail` Resources

For further information regarding `sendmail`, read the excellent book

+   1. Costales, Bryan, with Eric Allman, `sendmail`, 2d ed., Cambridge, Massachusetts, O'Reilly & Associates, Inc., 1997.

Also check the related web site

http://www.sendmail.org/