+   4. All running processes are terminated.
+   5. z/VM disables of the I/O devices.
+   6. The running system is terminated.

Example 5-20 shows the output of a z/VM shutdown process.

# Example 5-20 z/VM shutdown process.

```
00: 14:54:42 HCPWRP963I SHUTDOWN STEP USDAC - JOURNAL USER TERMINATION
00: 14:54:43 HCPWRP963I SHUTDOWN STEP MFRSD - TERMINATE HARDWARE LOADER
00: 14:54:43 HCPWRP963I SHUTDOWN STEP APISD - TERMINATE OTHER PROCESSORS
00: 14:54:44 HCPWRP963I SHUTDOWN STEP ENASD - DISABLE TERMINAL DEVICES
00: 14:54:45 HCPWRP963I SHUTDOWN STEP ISHDN - SHUT DOWN I/O SUBSYSTEM
00: 14:54:45 HCPWRP963I SHUTDOWN STEP TTRAL - TERMINATE CONCURRENT COPY SESSIONS
00: 14:54:46 HCPWRP963I SHUTDOWN STEP SVACV - ACTIVATE TERMINATION SAVE AREAS
00: 14:54:46 HCPWRP963I SHUTDOWN STEP CHMOF - DISABLE CHANNEL MEASUREMENT
00: 14:54:47 HCPWRP963I SHUTDOWN STEP ISHDA - DISABLE ALL DEVICES
00: 14:54:47 HCPWRP963I SHUTDOWN STEP CKPSH - TAKE A CHECKPOINT
00: 14:54:48 HCPWRP963I SHUTDOWN STEP OPRCD - SAVE OPERATOR CONSOLE LIST
00: 14:54:48 HCPWRP963I SHUTDOWN STEP MCWMD - DETERMINE MACHINE CHECK STATUS
00: 14:54:49 HCPWRP963I SHUTDOWN STEP SOVRS - RESET IBM DASD CU CHARACTERISTICS
00: HCPWRP962I VM SHUTDOWN COMPLETED IN 10 SEC
00: 14:54:49 HCPWRP963I SHUTDOWN STEP SVADV - DEACTIVATE TERMINATION SAVE AREAS
00: 14:54:50 HCPWRP961W SYSTEM SHUTDOWN COMPLETE
00: HCPGIR450W CP entered; disabled wait PSW 00020000 00000000 00000000 00000FFF
```

# 5.2.5 z/VM services

z/VM provides several services in the form of virtual machines. A virtual machine is similar to a z/OS Started Task, TSO User, or batch job. Unlike some operating systems, CP does not have the concept of a process. Instead, all CP knows is how to run virtual machines. This means that any extra service function not built directly into CP must be implemented as a service virtual machine.

A service virtual machine is the same as any other virtual machine, except it runs certain software (typically on top of CMS) that provides a service to some or all of the other users on the system.