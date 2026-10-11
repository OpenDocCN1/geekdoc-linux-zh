# **Listing A.1  Continued**

```
```
printf "\$s - system monitor script  Please wait...\n" "$0"

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
```