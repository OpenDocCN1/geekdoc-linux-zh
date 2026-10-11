
# Appendix A

## Listing A.1 (Continued)

```bash
    exit 0
    else
        printf "&\n" "$SCRIPT:$LINENO: Unexpected options/parameters"
        exit 192
fi
fi

# Sanity checks
# -------------------------------

if [ ! -x "$p1ng" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $p1ng" >&2
    exit 192
fi
if [ ! -x "$v$mat" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $v$mat" >&2
    exit 192
fi
if [ ! -x "$4$#" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $4$#" >&2
    exit 192
fi
if [ ! -x "$f$ee" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $f$ee" >&2
    exit 192
fi
if [ -z "$LINES" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: LINES is not declared. Export LINES" >&2
    exit 192
fi
if [ $LINES -lt 35 ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Your display must be >= 35 lines high" >&2
    exit 192
fi
if [ -z "$COLUMNS" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: COLUMNS is not declared. Export COLUMNS" >&2
    exit 192
fi
if [ $COLUMNS -lt 80 ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Your display must be >= 80 columns wide" >&2
    exit 192
fi
if [ -z "$HOME_CURSOR" ] ; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot HOME the cursor" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$UP" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor UP" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$DOWN" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor DOWN" >&2
    printf "%s\n" "(Some terminfo/termcap databases have curl/do set" >&2
    printf "%s\n" " improperly)" >&2
    printf "%s\n" " (Try declaring down as DOWN=\${'s[B]}" >&2
    exit 192
fi
if [ -z "$LEFT" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor LEFT" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$RIGHT" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor RIGHT" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$SCOL" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot clear to end of line" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ ! -x "$hostname" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot find or execute $hostname" >&2
    exit 192
fi
declare -rx HOST=`uname -n`                 # name of computer

# Get the total amount of physical memory

MEM_TOTAL=`free | grep ""Mem" | tr -s " " | cut -d" -f2`

# Clear the screen

tput reset
tput clear
```

```bash
printf "%s - system monitor script  Please wait...\n" "$0"

# _________________________
# Main Loop
# _________________________

while true ; do

    # Get the system statistics with vmstat

    TMP="nice -20 $vmstat $INTERVAL 2 2>&1"
    if [ $? -ne 0 ] ; then
        alarm "printf "vmstat error: $g" "$TMP" | tail -1"
        VMSTAT=
    else
        VMSTAT="printf "\$s\n" "$TMP" | tail -1"
    fi
    LEN=${#VMSTAT}  # length of VMSTAT
    OLD=$

    # Reduce all spaces to single spaces. Trim leading spaces

    while [ $LEN -ne $OLD ] ; do
        OLD=$LEN
        VMSTAT="${VMSTAT//}  /  }"
        VMSTAT="printf "\$a\n" "$VMSTAT" | sed 's/\\/\\g'
        LEN=${#VMSTAT}
    done

    # Extract the vmstat columns into variables
    # Use only what we need

    #PROC_R="printf "\$8\n" "$VMSTAT" | cut -d, -f1"
    #PROC_B="printf "\$8\n" "$VMSTAT" | cut -d, -f2"
    PROC_W="printf "\$8\n" "$VMSTAT" | cut -d, -f3"
    MEM_SWPD="printf "\$8\n" "$VMSTAT" | cut -d, -f4"
    MEM_FREE="printf "\$8\n" "$VMSTAT" | cut -d, -f5"
    MEM_BUP="printf "\$8\n" "$VMSTAT" | cut -d, -f6"
    MEM_CACHE="printf "\$8\n" "$VMSTAT" | cut -d, -f7"
    #SWAP_SI="printf "\$8\n" "$VMSTAT" | cut -d, -f8"
```

```bash
#SWAP_SO=`printf "%s\n" $VMSTAT | cut -d' ' -f9`
#IO_BLKI=`printf "%s\n" $VMSTAT | cut -d' ' -f10`
#IO_BLK0=`printf "%s\n" $VMSTAT | cut -d' ' -f11`
SYS_SI=`printf "%s\n" $VMSTAT | cut -d' ' -f12`
SYS_CS=`printf "%s\n" $VMSTAT | cut -d' ' -f13`
CPU_US=`printf "%s\n" $VMSTAT | cut -d' ' -f14`
CPU_SY=`printf "%s\n" $VMSTAT | cut -d' ' -f15`
IDLE=`printf "%s\n" $VMSTAT | cut -d' ' -f16`

# Get ready to update the screen
TIME=`date '+%H:%M:%S'`
SYSTEM_OK=1
LOG_UPDATED=0

# Perform the network test
#
# (some ping's won't return an error if it fails so we'll double check by
# making sure "trip" is in the result. No "trip" means probably an error
# message.)
TMP=`$ping $LAN_HOST -C 1 2>&1`
TMP2=`$?`
TMP3=`printf "%s" "$TMP" | grep trip`
if [ $TMP2 -ne 0 -o -z "$TMP3" ]; then
    alarm "Ping to LAN host $LAN_HOST failed: network load unknown"
    NET=99
else
    NET=`printf "%s\n" "$TMP3" | cut -d' ' -f4 | cut -d' ' -f1`
    if [ $(NET/0.4) = "msec" ]; then
        NET=`printf "%s\n" "$TMP3" | cut -d' ' -f5 | cut -d' ' -f1`
    fi
fi

# Draw stats bar at the top of the screen
printf "%s" "$HOME_CURSOR"$INVERSE$TIME
printf "%s" "CPU: $CPU_US% user, $CPU_SY% sys, $IDLE% idle
printf "%s\n" "MEM: $MEM_TOTAL total, $MEM_FREE free $"INVERSE_OFF"

# Compute values for the vertical bar graphs & Alarm tests
# CPU busy is the 100% minus the idle percent
```

```bash
# Show an alarm if the CPU limit is exceeded three times
# or if the kernel usage exceeds 50%

CPU=100-IDLE
if [ $CPU_SY -gt 50 ]; then
    alarm "Kernel bottleneck - system CPU usage $CPU_SY%"
fi

if [ $CPU -gt $CPU_LIMIT ]; then
    if [ $CPU1 -gt $CPU1_LIMIT ]; then
        if [ $CPU2 -gt $CPU2_LIMIT ]; then
            alarm "CPU bottleneck - $CPU% busy"
        fi
    fi
fi

# Signs of heavy system loads

if [ $SYS_CS -gt $THRASHING ]; then
    alarm "System Thrashing - $SYS_CS context switches"
elif [ $PROC_W -gt 0 ]; then
    alarm "Swapped out $PROC_W processes"
fi

# Show an alarm if the net limit is exceeded three times

if [ $NET -gt $NET_LIMIT ]; then
    if [ $NET1 -gt $NET1_LIMIT ]; then
        if [ $NET2 -gt $NET2_LIMIT ]; then
            alarm "Network bottleneck - $NET ms"
        fi
    fi
fi

if [ $SYS_SI -gt $DISK_LIMIT ]; then
    alarm "Disk bottleneck - $SYS_SI device interrupts"
fi

# Physical memory is used memory / total memory
# Show an alarm if the limit is exceeded three times

MEM=100*\(MEM_TOTAL-MEM_FREE\)/MEM_TOTAL
if [ $MEM2 -gt $MEM2_LIMIT ]; then
    if [ $MEM1 -gt $MEM1_LIMIT ]; then
        if [ $MEM -gt $MEM_LIMIT ]; then
            alarm "virtual memory shortage - memory $MEM% in use"
        fi
    fi
fi
```

```bash
# Check temp directory space

TMP=`$df 2>&1`
if [ $? -ne 0 ] ; then
    alarm "`printf "%s" "$TMP" | tail -1`"
else
    TMP=`printf "%s" "$TMP" | grep "/tmp"`
    if [ -n "$TMP" ] ; then
        TMP=`printf "%s" "$TMP" | grep "100%"`
        if [ -n "$TMP" ] ; then
            alarm "$0: /tmp appears to be full"
        fi
    fi
fi

PAGE=$SYS_CS/80                              # top of Faults graph is 8000

# Draw vertical bar graphs

printf "\n"
cpu_graph "$CPU"
mem_graph "$MEM"
page_graph "$PAGE"
net_graph "`$((10*NET))`"                # 100% = 10 nanoseconds

printf "%s\n" "$DOWN10"
printf "%s\n" "CPU Used        Memory            Thrashing (CS)"
printf "%s\n" "    LAN Traffic"

DSK=$SYS_SI/DISK_GRAPH_TOP
disk_graph "$DSK"

printf "%s\n" "$DOWN10"
printf "%s\n" "Disk Traffic"

# Nothing new logged?  Then show all is well in log
# ($SYSTEM_OK is cleared in the alarm function)

[ -n "$SYSTEM_OK" ] && alarm "System OK"
```

```bash
# Show alarm history, but only if it has changed

if [ -n "$LOG_UPDATED" ] ; then
    printf "%s\n"  "$LOG1""$CEOL"
    printf "%s\n"  "$LOG2""$CEOL"
    printf "%s\n"  "$LOG3""$CEOL"
    printf "%s\n"  "$LOG4""$CEOL"
    printf "%s\n"  "$LOG5""$CEOL"
    printf "%s\n"  "$LOG6""$CEOL"
    printf "%s\n"  "$LOG7""$CEOL"
    printf "%s\n"  "$LOG8""$CEOL"
fi

# sit quietly for a while before generating next screen

nice sleep $SLEEP

done

exit 0
```

# Appendix B

## Summary of Bash Built-In Commands

- **alias**—Manages aliases.
- **bg**—Starts a suspended task in the background.
- **bind**—Manages keyboard mappings.
- **builtin**—Runs a built-in shell command.
- **cd**—Changes the directory.
- **command**—Runs a Linux command.
- **declare**—Declares variables.
- **dirs**—Displays `cd` directory stack.
- **disown**—Stops monitoring a background job.
- **echo**—Prints to standard output.
- **enable**—Turns the built-in shell commands on or off.
- **eval**—Runs a command after performing shell substitutions/expansions.
- **exec**—Leaves the shell and switches to a new program.
- **exit**—Exits Bash and returns a status code.
- **export**—Manages exported variables.
- **false**—Returns a non-zero status code.
- **fc**—Finds and edits command history lines.
- **fg**—Runs a suspended job in the foreground.
- **function**—Declares a function.
- **hash**—Manages a Bash command table.
- **history**—Manages the command history.
- **jobs**—Manages your background jobs.
- **let**—Evaluates expressions.
- **local**—Declares a local function variable.
- **logout**—Exits the shell when in interactive mode.
- **popd**—Discards a `cd` directory stack entry.
