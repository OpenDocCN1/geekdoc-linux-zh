```
# transmitted and retransmitted
# segments and write it to a file
# SOLARIS
#
# author: Erik Keller
#
# parameters: none
#
########################################

# Variables
$varpath = "/export/home/users/erikk/work/baselines/var*";
$thelogfile = "base_retrans.log";

# open netstat -s Solaris version
open(MY_NETSTAT, "netstat -s | head -19 |" ) or die "$0: problems running netstat: $!";
while(<MY_NETSTAT>)
{
    chop;
    if(/tcpOutDataSegs/)
    {
        @tcpout = split(" ", $_);
        if(length($tcpout[1]) >= 2)
        {
            $tcpout[1] =~ s/-/ /;
            $tcpoutsegs = $tcpout[1];
        }
        else
        {
            $tcpoutsegs = $tcpout[2];
        }
    }
    if(/tcpRetransSegs/)
    {
        @tcpret = split(" ", $_);
        if(length($tcpret[1]) >= 2)
        {
            $tcpret[1] =~ s/-/ /;
            $tcpretsegs = $tcpret[1];
        }
        else
        {

```