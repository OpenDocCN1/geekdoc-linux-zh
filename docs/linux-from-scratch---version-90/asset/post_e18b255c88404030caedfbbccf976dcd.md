
# Appendix D. Boot and sysconfig scripts
version-20190524

## D.1. /etc/rc.d/init.d/rc

The rc script is the first script called by init and initiates the boot process.

```bash
#!/bin/bash
################################################################
# Begin rc
# Description : Main Run Level Control Script
# Authors
  : Gerard Beekemans - gerard@linuxfromscratch.org
  : DJ Lucas - djluc@linuxfromscratch.org
# Update
  : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Version
  : LFS 7.0
################################################################

/lib/lsb/init-functions

print_error_msg() {
  log_failure_msg
  # $i is set when called
  MSG="$FAILURE\/nYou should not be reading this error message.\n\n"
  MSG="$MSG)$i it means that an unforeseen error took place in\n"
  MSG="$MSG)${i},\n"
  MSG="$MSG)$which exited with a return value of $(error_value).\n"

  MSG="$MSG)If you are able to track this error down to a line of one of"
  MSG="$MSG)the files provided by the ${DISTRO_MINI} book,"\n"
  MSG="$MSG)please be so kind to inform us at ${DISTRO_CONTACT}.\n"
  log_failure_msg "$MSG"
}

log_info_msg "Press Enter to continue..."
  wait_for_user
}

check_script_status() {
  # $i is set when called
  if [ ! -f ${i} ]; then
    log_warning_msg "${i} is not a valid symlink."
    SCRIPT_STAT="1"
  fi
}

if [ ! -x ${i} ]; then
  log_warning_msg "${i} is not executable, skipping."
  SCRIPT_STAT="1"
fi

run()
{
    if [ -z $interactive ]; then
        ${1} $($2)
        return $?
    fi

    while true; do
        read -p "Run $($1) $($2) (Yes/no/continue)? " -n 1 run
        echo
        case $($1) in
            c | C)
                interactive=""
                $($1) $($2)
                ret=$?
                break;
                ;;
            n | N)
                return 0
                ;;
            y | Y)
                $($1) $($2)
                ret=$?
                break;
                ;;
        esac
    done
    return $$
}

# Read any local settings/overrides
[ -r /etc/sysconfig/rc.site ] && source /etc/sysconfig/rc.site
DISTRO=$DISTRO-"Linux from Scratch"
DISTRO_CONTACT=$DISTRO_CONTACT-"lfs-dev@linuxfromscratch.org (Registration required)
DISTRO_MINI=$DISTRO_MINI-"LFS"
IPROMPT=$IPROMPT-"no"

# These 3 signals will not cause our script to exit
trap "" INT QSTOP

```bash
[ "${1}" != "" ] && runlevel=$($1)

if [ "${runlevel}" == "" ]; then
    echo "Usage: $0 <runlevel>" >&2
    exit 1
fi
```

```bash
previous=$(PRELEVEL)
[ "$(previous)" = "" ] && previous=N
```

```bash
if [ ! -d /etc/rc.d/$(runlevel).d ]; then
  log_info_msg "/etc/rc.d/$(runlevel).d does not exist."
fi
```

```bash
if [ "$runlevel" = "6" -o "$runlevel" = "0" ]; then iPROMPT="no"; fi
```

```bash
if [ "$iPROMPT" = "yes" -a "$runlevel" = "S" ]; then
# The total length of the distro message string, with escape codes
len=$(echo "Welcome to ${DISTRO}" | wc -c)
welcome_message=${welcome_message:-"Welcome to ${DISTRO}$((NORMAL)}"}

# The total length of the interactive string, with escape codes
ilen=$(echo "Press to enter interactive startup" | wc -c)
image_message=${i_message:-"Press ${FAILURE}$(NORMAL) to enter interactive startup"}

# dcol and icol are spaces before the message to center the message
# on screen, it is the amount of time for the user to press a key
wcol=$(( (COLUMNS) - $len ) / 2 )
icol=$(( (COLUMNS) - $ilen ) / 2 )
time=$(( -t3 ))

echo -e "\n"
echo -e "\033[${wcol}$(welcome_message)"
echo -e "\033[${icol}#{i_message}$(NORMAL)}"
echo -e ""
read -t ${time} -n 1 interactive 2>/dev/null

# Make lower case
[ "$interactive" = "I" ] && interactive="i"
[ "$interactive" != "i" ] && interactive="i"

# Read the start file if it exists from runlevel S
[ -r /var/run/interactive ] && source /var/run/interactive

# Attempt to stop all services started by the previous runlevel,
# and killed in this runlevel
if [ "${previous}" != "N" ]; then
  for i in $(ls -v /etc/rc.d/$(runlevel).d/K* 2>/dev/null)
  do
    check_script_status
    if [ "$SCRIPT_STAT" = "1" ]; then
      SCRIPT_STAT="0"
      continue
    fi

    suffix=${i#/etc/rc.d/rc$runlevel.d/K[0-9][0-9]
    prev_start=/etc/rc.d/rc$previous.S[0-9][0-9]$suffix
    sysinit_start=/etc/rc.d/rc$d/S[0-9][0-9]$suffix

    if [ "$runlevel" != "0" -a "$runlevel" != "6" ]; then
      if [ ! -f "${prev_start}" -a ! -f "${sysinit_start}" ]; then
        MSG="$(MSG)WARNING:\n$(i) cannot be"
        MSG="$(MSG)executed because it was not"
        MSG="$(MSG)not started in the previous"
        MSG="$(MSG)runlevel (${previous})"\n    log_warning_msg "$MSG"
        continue
      fi

    run${i} stop
    error_value=${?}

    if [ "${error_value}" != "0" ]; then print_error_msg;
    fi

    if [ "${previous}" != "N" ]; then export IN_BOOT=1; fi
    if [ "$runlevel}" != "6" -a n "${FASTBOOT}" ]; then
      touch /fastboot
    fi

    # Start all functions in this runlevel
    for i in $(ls -v /etc/rc.d/rc$runlevel).d/S* 2>/dev/null);
    do
      if [ "${previous}" != "N" ]; then
        suffix=${i#/etc/rc.d/rc$runlevel.d/K[0-9][0-9]}
        stop=/etc/rc.d/rc$runlevel.d
        prev_start=/etc/rc.d/rc$previous.S[0-9][0-9]$suffix

        [ -f "${stop}" ] && continue
      fi
      # (Note: logic seems incomplete here based on OCR text)
    done
  fi
fi
```
[content]
# Standard console
NORMAL="3[0;39m"
SUCCESS="3[1;32m"
WARNING="3[1;33m"
FAILURE="3[1;31m"
INFO="3[1;36m"
BRACKET="3[1;34m"
# console grey
# Success is green
# Warnings are yellow
# Failures are red
# Information is light cyan
# Brackets are blue

# Use a colored prefix
BMPREFIX=""
SUCCESS_PREFIX="${SUCCESS} *${NORMAL}"
FAILURE_PREFIX="${FAILURE}******${NORMAL}"
WARNING_PREFIX="${WARNING} ***${NORMAL}"
SKIP_PREFIX="${INFO} S ${NORMAL}"
SUCCESS_SUFFIX="${BRACKET} OK ${BRACKET}${NORMAL}"
FAILURE_SUFFIX="${BRACKET} FAIL ${BRACKET}${NORMAL}"
WARNING_SUFFIX="${BRACKET} WAR ${BRACKET}${NORMAL}"
SKIP_SUFFIX="${BRACKET} SKIP ${BRACKET}${NORMAL}"

BOOTLOG=/rin/bootlog
KILLDEADAY=3
SCRIPT_STAT=""

# Screen Dimensions
# Find current screen size
if [ -z "${COLUMNS}" ]; then
COLUMNS=$(stty size)
COLUMNS=${COLUMNS## *}
fi

# When using remote connections, such as a serial port, stty size returns 0
if [ "${COLUMNS}" = "0" ]; then
COLUMNS=80
fi

# Measurements for positioning return messages
COL=$((${COLUMNS} - 8))
WCOL=$((${COL} - 2))

# Set Cursor Position,, via echo
SET_COL="3[${COL}G" # at the ${COL} char
SET_WCOL="3[${WCOL}G" # at the ${WCOL} char
CURS_UP="3[${UP}A3[${COL}G" # Up one line, at the ${COL}th char
CURS_ZERO="3[0}G"

####################################################################
# start_daemon())
# Usage: start_daemon [-f] [-n nicelevel] [-p pidfile] filename [args...]
# Purpose: This runs the specified program as a daemon
####################################################################
