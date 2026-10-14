```
B. Display Disk Space
C. Display Home Space Utilization
Q. Quit
""

read -p "Enter selection [A, B, C or Q] > "
case "$REPLY" in
  q|Q) echo "Program terminated."
       exit
       ;;
  a|A) echo "Hostname: $HOSTNAME"
       uptime
       ;;
  b|B) df -h
       ;;
  c|C) if [[ "$(id -u)" -eq 0 ]]; then
           echo "Home Space Utilization (All Users)"
           du -sh /home/*
       else
           echo "Home Space Utilization ($USER)"
           du -sh "$HOME"
       fi
       ;;
  *)   echo "Invalid entry" >&2
       exit 1
       ;;
esac
```

Here, we modify the case-menu program to use letters instead of digits for menu selection. Notice how the new patterns allow for entry of both uppercase and lowercase letters.

# Performing Multiple Actions

In versions of bash prior to 4.0, case allowed only one action to be performed on a successful match. After a successful match, the command would terminate. Here we see a script that tests a character:

```
#!/bin/bash

# case4-1: test a character

read -n 1 -p "Type a character > "
echo
case "$REPLY" in
```