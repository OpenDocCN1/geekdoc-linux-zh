```
###+
### Declare constants/global variables
###−

our ($DF, $DU, %FILESYSTEMS, $QUOTA, $NO_FILES); ### Pre-declare global variables

$DF = '/bin/df'; ### Path to df command
$DU = '/usr/bin/du -ab'; ### Path and options to du

###+
### The following three constants store (1) the filesystems to check and their maximum allowable usage thresholds, (2) max user's disk quota, 50 MB and (3) the number of files to process, 15. You should change these values to suit your requirements and system configuration.
###−

%FILESYSTEMS = ('/home1' => 90, '/home2' => 85);
$QUOTA = 1_024_000 * 50; ### Use _ to make large numbers more readable
$NO_FILES = 15;

###+
### Start main program
###−

print STDERR "Disk usage check in progress, please wait ...\n";

my ($percent, $filesystem);
local *PIPE1; ### Pre-declare/localize filehandle

open (PIPE1, "$DF |") || die "Cannot create pipe: $!\n";
while (<PIPE1>) { ### Read line into $_
if (/(\d+)%(\s+(.+)?\s*$)/) { ### Match against $_ variable
($percent, $filesystem) = ($1, $2); ### Store matches

if (exists $FILESYSTEMS{$filesystem} && ### Does this element
### exist in hash?
$percent >= $FILESYSTEMS{$filesystem}) {

print STDERR ">> $filesystem has $percent usage <<\n";
process_filesystem ($filesystem); ### Invoke subroutine
### with $filesystem as arg.
}
}
}

close (PIPE1);
exit (0);
```