
## Listing A.1 Continued

```bash
declare -rx CEOL='tput el' # clear to end of the line
declare -rx INVERSE='tput smso' # reverse video on
declare -rx INVERSE_OFF='tput rmso' # reverse video off
declare -rx UP10='$SUSSUSSUPSUSPSSUSSUPSUSPSSUSSUP$'
declare -rx DOWN10='$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$'

# VMSTAT fields

declare -ix PROC_R= # Ready processes
declare -ix PROC_B= # Blocked processes
declare -ix PROC_W= # Swapped out processes
declare -ix MEM_SWAPd= # Active virtual mem (KB)
declare -ix MEM_FREE= # Free virtual mem (KB)
declare -ix MEM_BUF= # Buffer space (KB)
declare -ix MEM_CACHE= # Disk cache (KB)
declare -ix SWAP_SI= # Swapped in processes
declare -ix SWAP_SO= # Swapped out processes
declare -ix IO_BLKI= # Blocks sent to IO devices
declare -ix IO_BLKO= # Blocks received from IO devices
declare -ix SYS_S= # interrupts (incl. the clock)
declare -ix SYS_CS= # Context switches
declare -ix CPU_US= # User CPU usage
declare -ix CPU_SY= # System CPU usage
declare -ix IDLE= # CPU idle time

# Misc Global Variables

declare TIME=`date '+%H:%M:%S'` # current time
declare TMP= # temporary results
declare TMP2=
declare TMP3=
declare -i CPU= # current CPU busy (percent)
declare -i MEM= # current virtual memory (percent)
declare PAGE= # current context switches
declare NET= # current network speed (msec/second)
declare LEN= # length of a string
declare OLD= # for fixing vmstat results
declare -i DSK= # disk activity (interrupts)
declare -i MEM_TOTAL=0 # Total virtual memory

# Functions

# VERTICAL BAR
# Draw a vertical bar graph 10 characters high. The bar is drawn with `#`
# and the blank areas with `.`.
#
# Parameter 1 - the value of the graph , a percent
# Parameter 2 - the old value of the bar , to speed drawing
#

function vertical_bar {

    declare -i DOTCNT  # number of periods to draw
    declare -i CNT     # number of number signs to draw

    # If the new bar is equal to the old one in this spot , don't bother
    # redrawing since it hasn't changed--unless it's zero since we may be
    # drawing this column for the first time.

    if [ $1 -ne 0 ] ; then
        if [ $1 -eq $2 ] ; then
            printf "%s" "$RIGHT""$RIGHT"
            return

        fi
    fi

    # Convert the magnitude of the bar to a number between 0 and 10
    # Round to the nearest integer
    # Constrain the percent to 0..10 if it is out of range

    if [ $1 -gt 100 ] ; then
        CNT=10
    elif [ $1 -lt 0 ] ; then
        CNT=0
    else
        CNT=$((($1+5) / 10))     # 0..100 rounded to 0..10
    fi

    # Draw the vertical bar. DOTCNT is the number of periods to draw
    # to fill in the graph.

    DOTCNT=10-CNT
    while [ $((DOTCNT--)) -gt 0 ] ; do
        printf "%s" ".""$DOWN""$LEFT"
    done
    while [ $((CNT--)) -gt 0 ] ; do
        printf "%s" "#""$DOWN""$LEFT"
    done

    printf "%s" "$SUP10" "$RIGHT""$RIGHT"

}

readonly -f vertical_bar
declare -t vertical_bar


# CPU GRAPH
#
# Update the vertical bar CPU usage graph.
# Parameter 1 - the new bar height to add to the graph
# ______________________________________

function cpu_graph {

 if [ -z "$1" ]; then # debug
        alarm "$FUNCNAME received a null string"
        return
fi
LAST="$SCPUB"
CPU8="$SCPUB"
CPU7="$SCPU6"
CPU6="$SCPU5"
CPU5="$SCPU4"
CPU4="$SCPU3"
CPU3="$SCPU2"
CPU2="$SCPU1"
CPU1="$1"

        vertical_bar "$SCPU8" "$LAST"
        vertical_bar "$SCPU7" "$SCPUB"
        vertical_bar "$SCPU6" "$SCPUB"
        vertical_bar "$SCPU5" "$SCPUB"
        vertical_bar "$SCPU4" "$SCPU5"
        vertical_bar "$SCPU3" "$SCPU4"
        vertical_bar "$SCPU2" "$SCPU3"
        vertical_bar "$SCPU1" "$SCPU2"

        printf "%s" "$RIGHT""$RIGHT"

}

readonly -f cpu_graph
declare -t cpu_graph

```

```bash
# MEM GRAPH
# # Update the vertical bar memory graph
# Parameter 1 - the new bar height to add to the graph
# ______________________

function mem_graph {

    # Sanity check

    if [ -z "$1" ] ; then # debug
        alarm "$FUNCNAME received a null string"
        return
    fi

    # Insert new value into the graph

    LAST=$MEM8
    MEM8=$MEM7
    MEM7=$MEM6
    MEM6=$MEM5
    MEM5=$MEM4
    MEM4=$MEM3
    MEM3=$MEM2
    MEM2=$MEM1
    MEM1="$1"

    # Draw the bars

    vertical_bar "$MEM8" "$LAST"
    vertical_bar "$MEM7" "$MEM8"
    vertical_bar "$MEM6" "$MEM7"
    vertical_bar "$MEM5" "$MEM6"
    vertical_bar "$MEM4" "$MEM5"
    vertical_bar "$MEM3" "$MEM4"
    vertical_bar "$MEM2" "$MEM3"
    vertical_bar "$MEM1" "$MEM2"

    printf "%s" "$RIGHT""$RIGHT"
}
readonly -f mem_graph
declare -t mem_graph

# PAGE GRAPH
# Update the vertical bar page fault graph
# Parameter 1 - the new bar height to add to the graph

function page_graph {
    # Sanity check
    if [ -z "$1" ]; then # debug
        alarm "$FUNCNAME received a null string"
        return
    fi

    # Insert new value into the graph

    LAST="$PAG8"
    PAG8="$PAG7"
    PAG7="$PAG6"
    PAG6="$PAG5"
    PAG5="$PAG4"
    PAG4="$PAG3"
    PAG3="$PAG2"
    PAG2="$PAG1"
    PAG1="$1"

    # Draw the bars

    vertical_bar "$PAG8" "$LAST"
    vertical_bar "$PAG7" "$PAG8"
    vertical_bar "$PAG6" "$PAG7"
    vertical_bar "$PAG5" "$PAG6"
    vertical_bar "$PAG4" "$PAG5"
    vertical_bar "$PAG3" "$PAG4"
    vertical_bar "$PAG2" "$PAG3"
    vertical_bar "$PAG1" "$PAG2"
    printf "%s" "$RIGHT""$RIGHT"
}

readonly -f page_graph
declare -t page_graph

# NET GRAPH
# Update the vertical bar page network traffic
# Parameter 1 - the new bar height to add to the graph
#
----------------------

function net_graph {

    # Sanity check

    if [ -z "$1" ] ; then # debug
        alarm "$FUNCNAME received a null string"
        return
    fi

    # Insert new value into the graph

    LAST="$SNET8"
    NET8="$SNET7"
    NET7="$SNET6"
    NET6="$SNET5"
    NET5="$SNET4"
    NET4="$SNET3"
    NET3="$SNET2"
    NET2="$SNET1"
    NET1="$1"

    # Draw the bars

    vertical_bar "$SNET8" "$LAST"
    vertical_bar "$SNET7" "$SNET8"
    vertical_bar "$SNET6" "$SNET7"
    vertical_bar "$SNET5" "$SNET6"
    vertical_bar "$SNET4" "$SNET5"
    vertical_bar "$SNET3" "$SNET4"
    vertical_bar "$SNET2" "$SNET3"
    vertical_bar "$SNET1" "$SNET2"

    printf "%s" "$RIGHT" "$RIGHT"

}
readonly -f net_graph
declare -t net_graph

# DISK GRAPH
#
# Update the vertical bar page disk interrrupts
# Parmmeter 1 - the new bar height to add to the graph
#
function disk_graph {
# Sanity check
if [ -z "$1" ] ; then # debug
alarm "$FUNCNAME received a null string"
return
fi
# Insert new value into the graph
LAST="$DSK8"
DSK8="$DSK7"
DSK7="$DSK6"
DSK6="$DSK5"
DSK5="$DSK4"
DSK4="$DSK3"
DSK3="$DSK2"
DSK2="$DSK1"
DSK1="$1"
# Draw the bars
vertical_bar "$DSK8" "$LAST"
vertical_bar "$DSK7" "$DSK8"
vertical_bar "$DSK6" "$DSK7"
vertical_bar "$DSK5" "$DSK6"
vertical_bar "$DSK4" "$DSK5"
vertical_bar "$DSK3" "$DSK4"
vertical_bar "$DSK2" "$DSK3"
vertical_bar "$DSK1" "$DSK2"
printf "%s" "$RIGHT""$GRIGHT"
}
readOnly -f disk_graph
declare -t disk_graph
# ALARM
#

# Add a message to the alarm log. Duplicate messages are discarded.
# Parameter 1 = the message to add
#
________

function alarm {
    # Anything logged this time around means system isn't OK, even if it was
    # a repeated message that was suppressed

    SYSTEM_OK=

    # Ignore repeated alarms
    [ "$1" = "$LASTLOG" ] && return
    LASTLOG=$1

    # Add the log message to the list of alarms
    LOG8="$LOG7"
    LOG7="$LOG6"
    LOG6="$LOG5"
    LOG5="$LOG4"
    LOG4="$LOG3"
    LOG3="$LOG2"
    LOG2="$LOG1"
    LOG1="$TIME - "$1"

    LOG_UPDATED=1
}
readonly -f alarm
declare -t alarm

#
________
# Main Script Begins Here
#
________

# Usage/Help
#
________

if [ $# -gt 0 ] ; then
    if [ "$1" = "-h" -o "$1" = "-help" ] ; then
        printf "$\n" "$SCRIPT::$LINE0: Show system resource usage graphs"
        printf "$\n" "There are no parameters for this script"
        printf "\n"
```
