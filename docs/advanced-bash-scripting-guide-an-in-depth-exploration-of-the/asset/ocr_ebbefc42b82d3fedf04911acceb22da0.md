# Advanced Bash-Scripting Guide

+   * Using shell scripts for CGI programming may be problematic. Shell script variables are not "typesafe", and this can cause undesirable behavior as CGI is concerned. Moreover, it is difficult to "cracker-proof" shell scripts.
* Bash does not handle the double slash (/) string correctly.

Bash scripts written for Linux or BSD systems may not run on a commercial UNIX machine. Such scripts often employ the GNU set of commands and filters, which have greater functionality than their generic UNIX counterparts. This is particularly true of such text processing utiles as it.

Sadly, updates to Bash itself have broken older scripts that *used to work perfectly fine*. Let us recall how risky it is to use undocumented Bash features_.

Danger is near thee --

> Beware, beware, beware, beware.

Many brave hearts are asleep in the deep.

So beware --

Beware.

--A.J. Lamb and H.W. Petrie