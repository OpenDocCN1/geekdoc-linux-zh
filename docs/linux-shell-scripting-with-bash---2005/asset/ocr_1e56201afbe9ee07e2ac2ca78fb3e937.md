The script shown in Listing 16.6 strips the official time from the NRCC and compares it to the time on the local computer.

# Listing 16.6\quad\quad compare\_time.sh

```
```bash
#!/bin/bash
#
#  compare_time.sh: compare our time against National Research
#  Council of Canada's atomic clock.

shopt -s -o nounset

# Global declarations

declare -rx SCRIPT=$0##*/    # name of our script
declare -rx lynx="/usr/bin/lynx"   # lynx command
declare -rx date="/bin/date"    # data command

declare  OUR_TIME      # our time as reported by date(1)
declare  TIME_PAGE     # the content of the NRCC web page
declare  TIME_LINE     # the page line with the time on it
declare  OFFICIAL_TIME   # the correct time from the line

declare -rx NRCC="time5.nrc.ca/webclock_e.shtml"  # NRCC web site

# Sanity Check

if test ! -x "$date" ; then
    printf "$$SCRIPT: the command $$date is not available -- aborting\n" >&1
    exit 192
fi
if test ! -x "$lynx" ; then
    printf "$$SCRIPT: the command $$lynx is not available -- aborting\n" >&1
    exit 192
fi

# Get the Time

OUR_TIME=`$$date --universal '+%H:%M:%S'`
TIME_PAGE=`$$lynx -dump -nolist "http://$$NRCC"`
if [ -z "$$TIME_PAGE" ] ; then
    printf "$$SCRIPT: the web page $$NRCC has moved -- aborting\n" >&1
    exit 192
fi
TIME_LINE=`printf "$$e\n" "$$TIME_PAGE" | grep UTC | head -1`
if [ -z "$$TIME_PAGE" ] ; then
    printf "$$SCRIPT: the format of the web page $$NRCC has changed --\)\
```
```