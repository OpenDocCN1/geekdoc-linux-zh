After you have all your rules in place, you can run the remove modules script in Listing 36.2. You’ll get errors on modules in use, but those not used will be removed. If you want to remove all the modules, you’ll first need to flush all the tables and remove any user-defined chains.

> **Note**
> 
> The `rmmod -a` command is supposed to remove unused modules, but will look at all modules. If you only want to look at removing specific modules, you’ll be better off using the script in Listing 36.2.

# LISTING 36.2  REMOVE MODULES SCRIPT

```
```perl
#!/usr/bin/perl -w
# Written by D. Bandel
# licensed under the GPL v2.0
# crude hack to unload lots of modules quickly

use strict;
use File::Basename;

my ($file,$path,$suff,$uname,$dir,$subdir,$count);

chomp($uname=`uname -r`);
#subdirs containing the modules we want removed
my @subdirs=("ipv4","ipv6");
#a kludge to remove modules with dependencies. It's this or
#keep a list of failed modules and retry only those
my @count=("1","2","3");
foreach $count (@count) {
    foreach $subdir (@subdirs) {
        #complete path to modules
        $dir="/lib/modules/$uname/kernel/net/$subdir/netfilter/";
        my @list=`ls $dir`;
        foreach $file (@list) {
            ($file,$path,$suff)=fileparse($file,".o");
            if (`lsmod | grep $file`) {
                # the work is done here:
                `rmmod $file 2>&1 /dev/null`;
            }
        }
    }
}
```
```

The instructions for modules.pl above apply to this script, which should be named rmmodules.pl. If you run the script once after all the netfilter rules are in place, it will remove unused modules. You can then see which modules are required and which aren’t (and save some memory in the process). You will want to keep the ip_nat_ftp module if you’re using the nat table. The preceding script can remove this module, but you’ll need it if you want to be able to do active FTP sessions from masqueraded hosts. If you want to remove the modules, you’ll need to flush all rules from all tables and delete all user-defined chains from all tables.