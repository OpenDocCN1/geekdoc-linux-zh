

symbolic names:
keyword substitution: kv
total revisions: 2;      selected revisions: 1
description: check df output for volumes filled > 70%
filtering complete
----------------------------------------
revision 1.2    locked by: erikk;
date: 2004/08/03 10:29:54;  author: erikk;  state: Exp;  lines: +7 -2
added variables for executables
================================================================================
===
erikk@unixhost>

The -r (revision) option is intended to give access to a certain revision, and if no specific revision is supplied, the information regarding the last check-in is displayed. To query a specific revision, for example, revision 1.1, the command would be used like so: rlog -r1.1.

If you intend to use the script on another *NIX system, variables enable you to keep the needed changes to a minimum. This doesn't seem to be necessary for the script at hand, but scripts tend to grow in complexity over time. Utilizing variables is one way to enhance portability and maintainability. Nobody forces you to use variables to call the needed programs. It is just good practice; after all, then you have only one line to change if needed.

## 2.2.3 Extending the Script

The script is now ready to be deployed on all systems where its functionality is useful. The drawback is that you are required to log into every system, run the script, and act on the output. If the script would run automatically at predefined times and write the output to a file, the task would be definitely simpler. Listing 2.14 extends the functionality of the script by having the output written to a file.

### LISTING 2.14 df_check.sh Output to File

```
#!/bin/sh
#
# $Id: df_check.sh,v 1.3 2004/08/05 08:18:18 erikk Exp erikk $
################################################################
#
#       file:            df_check.sh
#       purpose:         script to monitor the status
#                        of mounted volumes
#
#       author:      Erik Keller
#
#       parameters:
#
########################################################

# Variables
DF="/usr/bin/df"
GREP="/usr/bin/grep"
AWK="/usr/bin/awk"
SYSNAME=`/bin/uname -n`
REPORT=/export/home/users/erikk/work/df_check/${SYSNAME}_dfrep.txt

echo Systemname: $SYSNAME > $REPORT

$DF -h | $GREP % | $AWK '$5 >= 70 {print $6,": ",$5}' >> $REPORT

# EOF
```

Obvious additions in Listing 2.14 are the variables $SYSNAME and $REPORT. $SYSNAME contains the name of the system the script is run on by redirecting the output of uname -n using back ticks. Its primary use is to create a descriptive name for the resulting file containing the report. That filename (including the path) is stored in the second variable aptly called $REPORT. To deploy the script on another system, changing the variables that point to the programs and adjusting the path for the file to be created is sufficient.

However, one issue lingers; the script is functional but not very readable. Shouldn't that be addressed, as well?

Listing 2.15 shows how the script could look when fit for deployment.

### LISTING 2.15 Final df_check.sh Script

```
#!/bin/sh
#
# $Id: df_check.sh,v 1.3 2004/08/05 08:18:18 erikk Exp erikk $
########################################################
#
#       file:          df_check.sh
#
#       purpose:       script to monitor the status
#                      of mounted volumes
#
#     author:        Erik Keller
#
#     parameters:
#
##################################################

# Variables
# Used programs
DF="/usr/bin/df"
GREP="/usr/bin/grep"
AWK="/usr/bin/awk"

# OS info
SYSNAME=`uname -n`
OSNAME=`uname -s`
OSVERSION=`uname -r`
OSBUILD=`uname -v`

# destination
REPORTPATH=/export/home/users/erikk/work/df_check
REPORTFILE=${SYSNAME}_dfrep.txt
REPORTDEST=${REPORTPATH}/${REPORTFILE}

# Report header
echo Systemname: $SYSNAME > $REPORTDEST
echo Operatingsystem: $OSNAME \
$OSVERSION \
$OSBUILD >> $REPORTDEST
echo ------------------------ >> $REPORTDEST

# Diskfree report
$DF -h | $GREP % |
$AWK '$5 >= 70 {print $6, ":", $5}' \
>> $REPORTDEST

# EOF
```

As you can see, the script is now easier to customize and easier to read. The path and the filename are separated to avoid mistakes made while changing one of them, and the commands are sliced into smaller chunks using the continuation character \ (don’t forget: there can’t be any characters between \ and the carriage return (CR); otherwise, the continuation will not work). The new information regarding the name of the operating system ($SYSNAME), its version information ($OSVERSION), and the build details ($OSBUILD) are not essential to the deployment of the

