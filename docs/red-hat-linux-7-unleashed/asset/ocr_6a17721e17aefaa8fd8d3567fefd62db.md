Expect is an extension to tcl, so it is fully programmable with tcl capabilities. For information about tcl and tk from its author, Dr. John Ousterhout, visit http://www.sun.com/960710/cover/ousterhout.html. For more information about Expect, visit http://expect.nist.gov./

> Tip
> 
> You'll also find the autoexpect command included with Red Hat Linux. This command watches an interactive session at the console and then creates an executable program to execute the console session. See Chapter 11 for an example of how to use autoexpect to automate an FTP session.

# Perl

Some consider Perl the most popular scripting language for Red Hat Linux, apart from the shell. Its power and brevity take on particular value in automation contexts.

> Note
> 
> For more information about Perl, or to get the latest release, browse http://www.perl.com or http://www.perl.org.

For example, assume that /usr/local/bin/modified_directories.pl contains this code:

```
```perl
#!/usr/bin/perl
# Usage: `modified_directories.pl DIR1 DIR2 ... DIRn`
# Output: a list of all directories in the file systems under
#    DIR1 ... DIRn, collectivelу. They appear, sorted by the
#    interval since their last activity, that is, since a file
#    within them was last created, deleted, or renamed.
# Randal Schwartz wrote a related program from which this is
# descended.
use File::Find;
$directory_list = @ARGV;
# "-M" abbreviates "time since last modification", while
#    "-d" "... is a directory." 

find ( sub { 
   $modification_lapse{$File::Find::name} = -M if -d , 
   @directory_list );

for ( sort { 
   $modification_lapse{$a} <=> $modification_lapse{$b} } keys
```