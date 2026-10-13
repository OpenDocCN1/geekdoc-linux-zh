daily basis, you might want to automate the process as much as you can. Listing 8-6 shows a Perl script called makesite that you often can use to create a virtual domain.

# Listing 8-6 The makesite Script

```
#!/usr/local/bin/perl -w

use strict;

#
# Purpose: makesite creates virtual sites.
# It uses a set of templates to create DNS and HTTPD
# configuration files.
#
# Note: this is a very *simple* script.
#
####################################################

use Time::localtime;

my $site = $ARGV[0] or $syntax;
my $MAKESITE_DIR = '/scratch/dns/makesite';
my $USER = 'httpd';
my $GROUP = 'httpd';
my $PERMISSION = '2770';
my $BASE_DIR = '/tmp';
my $HTDOCS = 'htdocs';
my $CGIBIN = 'cgi-bin';
my $NAMED_PATH = '/var/named';
my $NAMED_FILE_EXT = '.db';
my $NAMED_TEMPLATE = "$MAKESITE_DIR/named.template";
my $NAMED_CONF = '/etc/named.conf';
my $HTTPD_CONF = 
'/usr/local/apache/etc/httpd.conf';
my $VHOST_TEMPLATE = "$MAKESITE_DIR/httpd.template";
```