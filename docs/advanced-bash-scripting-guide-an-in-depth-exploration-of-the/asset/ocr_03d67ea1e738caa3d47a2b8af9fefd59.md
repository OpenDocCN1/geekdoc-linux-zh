# Advanced Bash-Scripting Guide

```
3) exec 3>&2 4>&2 5>&2;
*) exec 3 >dev/null 4 >dev/null 5 >dev/null;
esac
FD_LOG_VARS=6
if [[ $LOG_VARS ]];
then exec 6>> /var/log/vars.log # Bury output.
else exec 6 >/dev/null
fi
FD_LOGGEVENTS=7
if [[ $LOG_EVENTS ]];
then # exec 7 >(awk '{print strftime(), $0}' >> # Above line fails in versions of Bash more recient than 2.04. Why?
# exec 7>> /var/log/event.log Append to "event.log"
log # Write time and date.
# Bury output.
else exec 7 >/dev/null
fi
echo "DEBUG3: beginning" >${FD_DEBUG3}
ls -1 >5 2>&4 # command1 >5 2>&4
echo "Done" # command2
echo "sending mail" >&${FD_LOGEEVENTS}
# Writes "sending mail" to file descriptor #7.
```

exit 0