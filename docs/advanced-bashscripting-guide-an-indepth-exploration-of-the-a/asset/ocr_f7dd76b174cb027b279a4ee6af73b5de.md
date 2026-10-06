# Advanced Bash–Scripting Guide

```
{
  echo "$(date)  $*&7  # This *appends the date to the file.
  # See below.
}
```

```
case $LOG_LEVEL in
1) exec $3&2 4> /dev/null 5 >/dev/null;
2) exec $3&2 5 >/dev/null;
3) exec $3&2 4>& 5>&2;
*) exec $3 >/dev/null 4> /dev/null 5 >/dev/null;
esac
```

```
FD_LOGARS=6
if [[ $LOG_VARS ]]
then exec 6 >/var/log/vars.log
else exec 6 >/dev/null
# Bury output.
fi
```

```
FD_LOGEVENTS=7
if [[ $LOG_EVENTS ]]
then
# exec 7>(exec ' 'print strftime(), $0)' >> /var/log/event.log)
# Above line will not work in Bash, version 2.04.
exec 7> /var/log/event.log
# Append to "event.log".
log
# Write time and date.
else exec 7> /dev/null
# Bury output.
fi
```

```
echo "DEBUG3: beginning" >${FD_DEBUG3}
ls -1 $5 2>&4  # command1 &5>&4
echo "Done"  # command2
```

```
echo "sending mail" >${FD_LOGEVENTS}  # Writes "sending mail" to fd #7.
```

```
exit 0
```

16.3. Applications 235