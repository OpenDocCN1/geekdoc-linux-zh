The system operator machine is defined in the z/VM configuration file, SYSTEM CONFIG, as shown in Example 8-4.

# Example 8-4 System Userids configuration

```
/*****************************************************************/
/* System Userids */
/*****************************************************************/

System_Userids ,
Operator OPERATOR ,
Account DISKACNT ,
Dump OPERATNS ,
Erep EREP
```

This console log can be saved to a spool file, so you can analyze it later. In case of a system abend, CP also automatically saves the console log to a spool file.

# Status of console logging

To determine whether the console activity is logged into a file, issue the command QUERY VIRTUAL CONSOLE (abbreviated as q v con), as shown in Example 8-5. The first line of the output says STOP, meaning console logging is not enabled.

# Example 8-5 Status of console logging

```
q v console
00: CONS 0009 ON LDEV L0003 TERM STOP HOST TCPIP FROM
9.57.138.243
00: 0009 CL T NO CONT NOHOLD COPY 001 READY FORM STANDARD
00: 0009 TO LNXGUI PRT DIST LNXGUI FLASCH 000 DEST OFF
00: 0009 FLASH CHAR MDFY 0 FCB LPP OFF
00: 0009 3215 NOEOF 0008 NOKEP NOMS G NOMAME
00: 0009 SUBCHANNEL = 0008

Ready; T=0.01/0.01 15:28:01
```

# Enabling console logging

To enable console logging in a virtual machine, such as LNXGUI, use the command CP SPOOL CONSOLE START (abbreviated as cp sp con start), as shown in Example 8-6. Check the status again with query console. The first line of the output should say START, meaning console logging is started.