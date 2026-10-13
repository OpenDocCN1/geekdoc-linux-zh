```
}
IntHandler() {
    echo "Got SIGINT, user interrupt."
    KillSubProcs
    exit 2
}
KillSubProcs() {
    kill ${CHPROCSIDS:=$!}
    if [ $? -eq 0 ] ; then echo "Sub-processes killed." ; fi
}
SetTimer() {
    DEF_TOUT=$[1-10];
    if [ $DEF_TOUT -ne 0 ] ; then
        sleep $DEF_TOUT & kill -s 14 $$ &
        CHPROCSIDS="$CHPROCSIDS $!"
        TIMERPROC=$!
    fi
}
UnsetTimer() {
    kill $TIMERPROC
}
# main()
trap AlarmHandler 14
trap IntHandler 2
SetTimer 15
SPROG &
CHPROCSIDS="$CHPROCSIDS $!"
wait $!
unsetTimer
echo "All Done."
exit 0
```

# Hour 20

1. The three main methods are

+   - Issue the script in the following fashion:
+     $ /bin/sh option script arg1 arg2 arg3
+   - Change the first line of the script to
+     #!/bin/sh option
+   - Use the set command as follows:
+     set option