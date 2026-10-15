```
#
###################################
use Getopt::Std;
# Variables
$varpath="/export/home/users/erikk/work/baselines/var/dirwatch";
# get directory to watch
getopt('d');
if($opt_d eq '')
{
    usage();
}
open(MY_DIRS, " du -sk $opt_d/* |")
    or die "$0: du failed: $!";
while(<MY_DIRS>)
{
    chop;
    @myrec = split(" ", $_);
    $dirname = "dw_" . $myrec[1];
    $dirname =~ s/\/\//g;
    if($opt_k)
    {
        # use KB
        $mysize = $myrec[0];
    }
    else
    {
        # use MB
        $mysize = int($myrec[0]/1024);
    }
    open(MY_LOG, ">>$varpath/$dirname")
        or die "$0: error using file: $!";
    print MY_LOG "$mysize\n";
    close(MY_LOG);
}
close(MY_DIRS);
sub usage()
{
```