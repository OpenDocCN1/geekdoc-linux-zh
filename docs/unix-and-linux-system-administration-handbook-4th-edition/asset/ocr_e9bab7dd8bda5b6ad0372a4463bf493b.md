If amavisd hands the scanned message and results back to the MTA from which the message was originally received, filtering can be done in-line and the message rejected during the MTA's initial SMTP session. If amavisd instead queues messages for an internal mail hub, the filtering is off-line and naughty messages can be dropped or bounced.

See Chapter 21 for more information about SNMP.

amavisd is meticulous about not losing mail, not letting messages slip by without being checked, honoring individual recipients' wishes, and following the standards laid out in the various email-related RFCs. Despite being written in Perl, amavisd has pretty good performance. It scans each message only once, no matter how many recipients are associated with it. Logging can be quite extensive, and tools in the distribution can monitor filtering through SNMP. amavisd does not need to run as root and has a good security history.

# amavisd installation

Download the latest version of the software from jims.is/software/amavisd or grab a Linux package and skip the steps detailed in the INSTALL file at the top of the distribution hierarchy. The project home page has pointers to precompiled packages. amavisd expects to run as user and group vscan or amavis, so it might be easiest to create that user and group and then log in as vscan to get the software and install it. After you have amavisd installed and working correctly, change the account's login shell to /bin/false or some other restricted shell.

The file amavisd.conf-default contains a list of every possible configuration parameter and its default value. amavisd.conf-sample is a more typical commented sample config file. Finally, amavisd.conf is a minimal starting place (but still over 750 lines long!) with some comments for variables that must be changed. The configuration language is Perl.

# Basic amavisd configuration

Here is a basic amavisd configuration for a host called mail.example.com, where the MTA and amavisd are running on the same machine and using TCP and the SMTP protocol to communicate with each other.

```
use strict;

$myhostname = 'mail.example.com';
@local_domains_maps = ({'example.com'});
@mynetworks = qw[127.0.0.0/8 192.168.0.0/16];

$forward_method = 'smtp:[127.0.0.1]:10025';
$enable_db = 1;
$enable_global_cache = 1;
$max_servers = 5;
$DO_SYSLOG = 1;
$SYSLOG_LEVEL = 'mail.info';
$bypass_decode_parts = 1;
```