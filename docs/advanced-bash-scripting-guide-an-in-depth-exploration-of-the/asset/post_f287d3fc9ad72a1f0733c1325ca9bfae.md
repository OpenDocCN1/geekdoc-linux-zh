
# Advanced Bash-Scripting Guide

Default is home directory
CDFile - Set the default filename for the -f & -u options.
Default is cdfile

There are three variables defined in the file cdll which control the number of entries stored or displayed. They are in the section labeled 'Initialisation here' towards the end of the file.

- cd_maxhistory:
The number of history entries stored.
Default is 50.
- cd_maxpecial:
The number of special entries allowed.
Default is 9.
- cd_histcount:
The number of history and special entries displayed. 
Default is 9.

Note that cd_maxpecial should >= cd_histcount to avoid displaying special entries that can't be set.

Version: 1.2.1 Date: 24-MAY-2003

DOCUMENTATION

# Example A-34. A soundcard setup script

```bash
#!/bin/bash
# soundcard-on.sh

# Script author: Marcher ...
# http://www.thinkwiki.org/wiki
# /Script_for_configuring_CS4239_sound_chip_in_PnP_mode
# ABS guide made minor changes and added comments.
# Couldn't contact script author to ask for permission to use, but ...
# the script was released under the PDL,
# so the use here should be both legal and ethical.

# Sound-via-pnp-script for Thinkpad 600
# and and possibly other computers with onboard CS4239/CS4610
# that do not work with the PCI driver
# and are not recognized by the PnP code of snd-cs4236.
# Also for some 770-series Thinkpads, such as the 770x.
# Run as root user, of course.

# These are old and very obsolete laptop computers,
# but this particular script is very instructive,
# as it shows how to set up and handle device files.
```

```bash
# Search for sound card pnp device:

for dev in /sys/bus/pnp/devices/*
do
    grep CS0100 $dev | /dev/null && WSSDEV=$dev
    grep CS0110 $dev | /dev/null && CTLDEV=$dev
done
# On 770x:
# WSSDEV = /sys/bus/pnp/devices/00/07
# CTLDEV = /sys/bus/pnp/devices/00/06
# These are symbolic links to /sys/devices/pnp0/ 
```

# Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

# Activate devices:

# Activate devices:
# Thinkpad boots with devices disabled unless "fast boot" is turned off
# (in BIOS).

```bash
echo activate > $WSSDEV/resources
echo activate > $CTLDEV/resources
```

# Parse resource settings.

```bash
read | discard "state active" (see below).
read bla port1
read bla port2
read bla port3
read bla irq
read bla dma1
read bla dma2
```

# "The" labels are in the first field: "io," "state," etc.
# These are discarded.

```bash
# Hack; with PnPPorts: ports are port1: WSS, port2:
# OPL, port3: sb (unneeded)
# port:1, port2: sb, port3: WSS
# (ACPI BIOS seems to be wrong, the PnP-card-code in snd-cs4326.c
# used the PnPBIOS port order)
# Detect port order using the fixed OPL port as reference.
if [ ${port2%-*} = 0x38 ]; then
    #### Strip everything following hyphen in port address.
    # So, if port1 = 0x530
    # we're left with 0x530 -- the start address of the port.
    # PnPBIOS: usual order
    port=${port1%-}
    oport=${port2%-}
else
    # ACPI: mixed-up order
    port=${port3%-}
    oport=${port1%-}
fi
$ <WSSDEV/resources
# To see what's going on here:
# ------------------------------
```

```bash
cat /sys/devices/pnp0/00:07/resources

# state = active
io 0x530-0x537
io 0x388-0x38b
io 0x220-0x233
irq 5
dma 1
dma 0
```
# "bia" labels in first field (discarded).

```bash
read | discard first line, as above.
read bla port1
cport=${port1%-}
####
# Just want _start_ address of port.
) $CTLDEV/resources
```

# Advanced Bash-Scripting Guide

```bash
# Load the module:

modprobe --ignore-install snd-cs4236 port=$port cport=$cport \
fm_port=$cport irq=$irq dma=$dma d2=$dma isapnp=0 index=0
# See the modprobe manual.

exit $?
```

# Example A-35. Locating split paragraphs in a text file

```bash
#!/bin/bash
# find-splitpara.sh
# Finds split paragraphs in a text file,
# tags the line numbers.

ARGCOUNT=1      # Expect one arg.
OFF=0           # Flag states.
ON=1
WRONGARGS=85

file="$1"      # Target filename.
linen=1         # Line number. Start at 1.
Flag=$OFF       # Blank line.

if [ $# -ne "$ARGCOUNT" ]; then
  echo "Usage: `basename $0`"
  exit $WRONGARGS
fi

file_read () {
  # Scan file for pattern, then print line.
  while read line; do
    if [[ "$line" =~ ^[a-z] ]] && [ $Flag -eq $ON ]; then
      # Line begins with lowercase character, following line.
      echo -n "$linen:"
      echo "$line"
    fi
    if [[ "$line" =~ ^$ ]]; then
      # If blank line,
      Flag=$ON # set flag.
    else
      Flag=$OFF
    fi
    ((linen++))
  done < "$file"
}
file_read
```

# Advanced Bash-Scripting Guide

```bash
exit $?

# ----------------------------------------------------------------------
# This is line one of example, bla.
# This is line two, and line should follow on next line,
# there is a blank line separating two parts of the paragraph.
# ----------------------------------------------------------------------
# Running this script on file containing the above paragraph
# yields:
# a blank line separating two parts of the paragraph.
# There will be additional output for all other split paragraphs
# in the target file.
```

```bash
#!/bin/bash
#-sort.bash: Insertion sort in Bash
# Heavy use of Bash features:
# (string) slicing, merging, etc
# URL: http://www.linux.org/doc/insertion-sort.bash
# Author: Juan Carlos <carlos@igacion.gov>
# Lightly formatted by ABS.
# License: GPL2
# Used in ABS Guide with author's permission (thanks!)
# Test with: ./insertion-sort.bash -t
# Or: bash-sort.bash -t
# The following *doesn't* work:
# Why not? Hint: Bash-specific features are disabled
# when running by 'script.sh'

# ${DEBUG:=0} - Debug, override with: DEBUG=1 ./scriptname
# Parameter substitution -- set 0 if previously set.

# Global array: "list"
typeset -a list
# Load whitespace-separated numbers from stdin.
if [ "$1" = "-t" ]; then
    DEBUG=1
else
    read -a list <<< $(head -w24 /dev/urandom) # Random list. # process substitution
fi
numelem=${#list[*]}

# Shows the list, marking the element whose index is $1
# by surrounding it with the two chars passed as $2.
# Whole line prefixed with $3.
showlist() {
    echo "$3${list[@]:0:1} ${2:0:1}${list[$1]}:2:1} ${list[$1]:$1+1}"
}
```

# Example A-36. Insertion sort

# # Advanced Bash-Scripting Guide

```bash
# Loop _pivot_ from second to end of list.
for ((i=1;i<numelem; i++)); do
    ((DEBUG))show list "[$i]"
    # Current pivot_ back to first element.
    for ((j=i; j>=0; j--)); do
        # Search for the first elem. less than "pivot"
        while [[ ${list[$j-1]} -le ${list[$i]} ]]; do
            ((j--))
        done
        ((j)) && break # No insertion was needed for this element.
        # Move list(pivot) to the left of list[j]:
        list=(${list[@]:0:j} ${list[$i]} ${list[@]:j+1})
        ((j+1))
        # ${list[$i]:j+1}:-(j+1)} ${list[@]:i+1} (i+1,last)
    done
    ((DEBUG))show j "<="
done
```

```bash
echo "------"
echo -e "\Result:\n${list[$1]}"
```

exit $?

# Example-A.37. Standard Deviation

```bash
#!/bin/bash
# sd.sh Standard Deviation
```

# The Standard Deviation indicates how consistent a set of data is.
# It shows to what extent the individual data points deviate from the
# arithmetic mean, i.e., how they "bounce around" (or cluster).
# It is essentially the average deviation-distance of the
# data points from the mean.

# To calculate the Standard Deviation:
# Find the arithmetic mean (average) of all the data points.
# Subtract each data point from the arithmetic mean,
# and square that.
# Add all of the individual difference-squares in #2.
# Divide the sum in #3 by the number of data points.
# This is known as the "variance".
# The square root of #4 gives the Standard Deviation.

```bash
count=0 # Number of data points; global.
sc=9 # Scale to be used by bc. Decimal places.
E_DATAFILE=90 # Data file error.
```

```bash
# Set data file
if [ -z "$1" ]; then # Specify filename as cmd-line arg;
then
    dataFile="$1" # ASCII text file,
else
    # # one (numerical) data point per line!
    dataFile=sample.dat # See data file, below.
 fi
```
