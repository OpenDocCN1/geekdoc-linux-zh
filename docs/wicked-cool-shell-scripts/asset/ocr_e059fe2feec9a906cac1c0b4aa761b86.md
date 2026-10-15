# Running the Script

This script should be passed the path to a standard Apache-format error log as its only argument, shown in Listing 10-6. If invoked with a -1 length argument, it will display length number of matches per error type checked rather than the default of five entries per error type.

# The Results

```
$ weberrors error_log
Input file error_log has 768 entries.
Entries from [Mon Jun 05 03:35:34 2017] to [Fri Jun 09 13:22:58 2017]

File does not exist errors:
 94 /var/www/vhosts/default/htdocs/mnews.htm
 36 /var/www/vhosts/default/htdocs/robots.txt
 15 /var/www/vhosts/default/htdocs/index.rdf
 10 /var/www/vhosts/default/htdocs/clientaccesspolicy.xml
 5 /var/www/vhosts/default/htdocs/phpMyAdmin

Script not found or unable to stat errors:
 1 /var/www/vhosts/default/cgi-binphp5
 1 /var/www/vhosts/default/cgi-binphp4
 1 /var/www/vhosts/default/cgi-binphp.cgi
 1 /var/www/vhosts/default/cgi-binphp-cgi
 1 /var/www/vhosts/default/cgi-binphp

Additional error messages in log file:
 1 script '/var/www/vhosts/default/htdocs/wp-trackback.php' not found or unable to stat
 1 script '/var/www/vhosts/default/htdocs/sprawdz.php' not found or unable to stat
 1 script '/var/www/vhosts/default/htdocs/phpmyadminitting.php' not found or unable to stat

And non-error messages occurring in the log file:
 6 /usr/lib64/python2.6/site-packages/mod_python/importer.py:32: DeprecationWarning: the md5 module is deprecated; use hashlib instead
 6 import md5
 3 [Sun Jun 25 03:35:34 2017] [warn] RSA server certificate CommonName (CN) 'Parallels Panel' does NOT match server name!
 1 sh: /usr/local/bin/zip: No such file or directory
 1 sh: /usr/local/bin/unzip: No such file or directory
```

Listing 10-6: Running the weberrors script on Apache error logs

# #76 Avoiding Disaster with a Remote Archive

Whether or not you have a comprehensive backup strategy, it’s a nice insurance policy to back up a few critical files with a separate off-site archive system. Even if it’s just that one key file with all your customer addresses, your