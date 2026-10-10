# **LISTING 29.1** Continued

```
case "$1" in

    start)
        ${PORTSENTRY} -tcp && echo "Starting PortSentry TCP mode..."
        ${PORTSENTRY} -udp && echo "Starting PortSentry UDP mode..."
        ;;

    stop)
        killall `basename ${PORTSENTRY}`
        ;;

    *)
        echo ""
        echo "Usage: `basename $0` { start | stop }"
        echo ""
        ;;

esac
```

# **TIP**

While PortSentry is running, you can see which ports it's listening on by using the sockstat command:

```
# sockstat

USER        COMMAND       PID   FD  PROTO   LOCAL ADDRESS       FOREIGN ADDRESS
root        portsent      2432  0   udp4    *:*                 *:*   
root        portsent      2432  1   udp4    *:*                 *:*   
root        portsent      2432  2   udp4    *:*                 *:*   
root        portsent      2432  3   udp4    *:*                 *:*   
root        portsent      2432  4   udp4    *:*                 *:*   
root        portsent      2432  5   udp4    *:*                 *:*   
...
```

Each time PortSentry detects an attack attempt, it lists the host and ports that triggered the detection in /usr/local/etc/portsentry.blocked.tcp for TCP attacks and /usr/local/etc/portsentry.blocked.udp for UDP attacks. PortSentry uses these lists to keep track of which hosts it has already blocked so that it doesn't try to block them again later. You can also use these files to see what hosts have been caught by your attack-detection system. These files are cleared out automatically each time PortSentry starts up. When you reboot, both IPFW and the routing table are cleared of any entries that were added during runtime, so a host that was blocked once will have access to you again if you reboot—at least until it tries to probe your ports again.