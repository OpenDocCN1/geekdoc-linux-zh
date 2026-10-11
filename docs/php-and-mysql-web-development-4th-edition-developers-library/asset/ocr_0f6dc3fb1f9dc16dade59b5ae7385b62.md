# # Perl DBI API Reference

This appendix describes the Perl DBI application programming interface. The API consists of a set of methods and attributes for communica­ting with database servers and ac­cessing databases from Perl scripts. The appendix also describes MySQL-specific extensions to DBI provided by DBD:MySQL, the MySQL database driver.

DBI is currently at version 1.601, although most of the material here ap­plies to earlier versions as well. I as­s­sume here a minimum version of DBI 1.40, which requires at least Perl 5.6.0 (and 5.6.1 is preferred to 5.6.0). I also as­s­sume a min­imum version of DBD:MySQL 3.0000_0. Changes in DBI or DBD:MySQL be­ha­vior introduced after those minimum versions are noted. For mysql­_server­_­prepare support, it is best to use DBD:MySQL 3.0009 or higher because there were some changes to the default value of this feature in some of the preceding releas­es.

To determine your versions of DBI and DBD:MySQL, run this program:

```
#!/usr/bin/perl
# dbi-version.pl play DBI and DBD:MySQL versions
use strict;
use warnings;
use DBI;
print "DBI::VERSION: $DBI::VERSION\n";
use DBD:MySQL;
print "DBD:MySQL::VERSION: $DBD:MySQL::VERSION\n";
```

Some DBI methods and attributes are not discussed here, either because they do not apply to MySQL or because they are ex­peri­mental methods that may change as they are devel­op®d or may even be dropped. Some MySQL-specific DBD methods are not dis­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­­. If you want more in­for­ma­tion about new or obsolete methods, see the DBI doc­umen­tion or the MySQL DBD doc­umen­tion, which you can get by running the following com­mands:

```
% perldoc DBI
% perldoc DBI::FAQ
% perldoc DBD:MySQL
```