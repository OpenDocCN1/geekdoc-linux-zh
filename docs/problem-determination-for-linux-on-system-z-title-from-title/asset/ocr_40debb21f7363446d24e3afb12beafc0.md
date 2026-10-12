+   f.  Try to get the debug trace in the environment in which it is occuring. Set the debug level:
+       # echo 6 > /proc/s390dbf/cio_msg/level
+       # echo 6 > /proc/s390dbf/cio_trace/level

+   g.  Set LCHP OFF/ON
+       # echo "offline" > /sys/devices/css0/chp0.63/status
+       # echo "online" > /sys/devices/css0/chp0.63/status

+   h.  Get dbginfo.

If after LCHP is turned off and the status still does not change to online:

+   a.  Examine hardware again.

+   b.  Forcibly obtain the detailed information from the OSA. (Use forcelog, which are error logs obtained by the operating system engineer.) Check that the stop happens.

+   ■  Result and solution: hardware problem.
+       Exchanging the OSA card will solve the problem.

+   ■  Tips: The same phenomon is occuring in some LPARs that share an OSA port.

It seems more likely to be a hardware problem.

When it is difficult to determine whether it is hardware trouble or software trouble, reproduce the problem and get the s390dbf.

# ### 8.4.5 DASD recognition problem in boot process

The characteristics of a DASD recognition problem in the boot process are:

+   ■  State: The system does not recognize the DASD in reboot (see Example 8-14).

```
Example 8-14 /var/log/boot.msg
Couldn't find device with uid 'cPuNQ1-zYo0-3bo5-gxrc-b5VL-Nomg-prT5qf'.
Couldn't find all physical volumes for volume group vgHPPRRC01arcdest0401.
/dev/dasdca1: lseek 0 failed: invalid argument
/dev/dasdca1: lseek 0 failed: invalid argument
```

+   ■  Environment: SLES9 on System z.

+   ■  Information gathered:
+       –  /var/log/boot.msg
+       –  dbginfo.sh (includes /var/log/messages)
+       –  siga no