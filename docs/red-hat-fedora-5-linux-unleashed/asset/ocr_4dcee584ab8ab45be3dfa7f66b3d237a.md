to perform a task normally requiring a number of command lines. For example, you can create a short script, named `greplog`, like this:

```
```shell
#!/bin/sh
#  name:  greplog
#  use: mail grep of designated log using keyword
#  version:  v.01 0@Aug02
#
#  author: bb
#
#  usage: greplog [keyword] [logfilepathname]
#
#  bugs: does not check for correct number of arguments

# build report name using keyword search and date
log_report=/tmp/$1.logreport.`date '+%m%d%y'`

# build report header with system type, hostname, date and time
echo "==================================================" \
      >$log_report
echo "        SYSTEM MONITOR LOG" >>$log_report
echo uname -a >>$log_report
echo "Log report for" `hostname -f` `on ` `date '+%c'`   >>$log_report
echo "==================================================" \
      >$log_report ; echo "" >>$log_report

# record log search start
echo "Search for->" $1 "starting" `date '+%r'` >>$log_report
echo "" >>$log_report

# Get and save grep results of keyword ($1) from logfile ($2)
grep -i $1 $2 >>$log_report

# build report footer with time
echo "" >>$log_report
echo "End of" $log_report `at ` `date '+%r'` >>$log_report

# mail report to root
mail -s "Log Analysis for $1" root <$log_report

# clean up and remove report
rm $log_report
exit 0
```
```

In this example, the script creates the variable `$log_report`, which will be the filename of the temporary report. The keyword ($1) and first argument on the command line is used