of the first field. The numbering of the array fields starts with 0, just like in most other programming languages. This means the first field is on address 0, the second field on address 1, and so forth. Thus, the information you are looking for is in field 0 and field 2. Listing 2.21 presents the script and its output.

# LISTING 2.21 Perl Script to Extract Usernames and IDs

```
#!/usr/bin/perl
# $Id: ulist1.pl,v 1.1 2004/08/10 10:57:03 erikk Exp erikk $
#
#####################################################################
#
#    file:      ulist1.pl
#
#    purpose:   lists all users
#               and their respective IDs
#
#
#    author:    Erik Keller
#
#####################################################################

# Variables

# list passwd first
# open the file
open(MY_PWFILE, "/etc/passwd") or die
    "$0: couldn't open file: $!";

# loop through the file and print the records
while(<MY_PWFILE>)
{
    chop;
    @my_records = split(":",$_);
    print "$my_records[0]\t$my_records[2]\n";
}

# close the file
close(MY_PWFILE);

# EOF

erikk@unixhost:> ./ulist1.pl
```