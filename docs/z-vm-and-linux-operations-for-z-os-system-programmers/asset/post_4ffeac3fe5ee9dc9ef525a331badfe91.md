
==> log
A new logon panel opens.

+   2. Log on to AUTOLOG1. Again the password is the same as the user ID.

+   3. At the VM READ prompt enter ACCESS (NOPROF to prevent PROFILE EXEC from running:

```
LOGON AUTOLOG1
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: NO RDR, NO PRT, NO PUN
LOGON AT 13:30:12 EST THURSDAY 11/29/07
DMSIND2015W Unable to access the Y-disk. Filemode Y (19E) not accessed
z/VM V5.3.0 2007-11-24 12:48
acc (noprof
```

+   4. Copy the PROFILE XEDIT from the MAINT 191 disk so XEDIT sessions will have a common interface among user IDs.

+   a. Use the VMLINK command to both link to the read-only disk and to access it at the highest available file mode. The default read password is read:

```
==> vmlink maint 191
ENTER READ PASSWORD:
read
DMSVML20601 MAINT 191 linked as 0120 file mode Z
```

+   b. Copy the PROFILE XEDIT to your A disk:

```
==> copy profile xedit z = = a
```

+   5. Make a backup copy of the PROFILE EXEC and run the editor to edit it:

```
==> copy profile exec a = execorig =
==> x profile exec
```

The text in Example 4-2 appears.

## Example 4-2 The text before you modify it

```
/**************************/
/* Autolog1 Profile Exec */
/**************************/

Address Command
'CP XAUTOLOG VMSERVS'
'CP XAUTOLOG VMSERVU'
'CP XAUTOLOG VMSERVR'
```

+   6. Modify it as follows and see the results in Example 4-3 on page 163.

+   a. The z/VM Shared File System (SFS), is not required to run Linux so you can safely delete the three AUTOLOG lines for the user IDs VMSERVS, VMSERVR and VMSERVU.
+   b. You can also safely delete the Address Command line.
+   c. Add a line to start the TCPIP user ID with the XAUTOLOG command, and retain any statements that start the VSWITCH controllers.
+   d. Add a line to LOGOFF of AUTOLOG1 when the EXEC is complete. There is no need to keep that virtual machine running because its sole purpose is to run the PROFILE EXEC.

## Example 4-3 The text after you modify it

```
/***********************/
/* Autolog1 Profile Exec */
/***********************/

/* start up TCPIP */
/* logoff when done */

'cp autolog tcpip' /* start up TCPIP */
'cp logoff' /* logoff when done */
```

7. Save your changes with the FILE subcommand and use LOGOFF to log off AUTOLOG1:

=====> file

=====> log

When your z/VM system IPLs, the TCP/IP stack will come up automatically (if you do not specify the notautolog parameter at IPL time).

## Setting up an FTP server

In this section, you learn how to set up an FTP server for your z/VM because, in the section "Getting the files required for Linux boot" on page 188, you have to send files from your workstation to your Linux guest virtual machine. The files must keep their 80-character record length property.

By default, z/VM has an FTP server included in its installation. To bring it online, log on as TCPMAINT and edit the PROFILE TCPIP file on its 198 disk, which is accessed as the D disk:

=====> x profile tcpip d

## Example 4-4 The file before editing it

```
; 
; 
OBEY
OPERATOR TCPMAINT MAINT MPROUTE ROUTED DHCPD REXECD SNMPD SNMPQE
ENDBEY
```

```
; -----------------------------------------------------------------
PORT
; 20 TCP FTPSERVE NOAUTOLOG ; FTP Server
; 21 TCP FTPSERVE          ; FTP Server
; 23 TCP INTCLIEN          ; TELNET Server
; 25 TCP SMTP              ; SMTP Server
...
```

Add an AUTOLOG statement near the top of the file; FTPSERVE should be the only entry. In the PORT statement, remove the semicolons to uncomment the lines containing FTPSERVE (ports 20 and 21). These changes cause the FTP server to start when TCP/IP is started. Then, save your changes with the FILE subcommand. See Example 4-5.

## Example 4-5 The file after editing it

```
; -----------------------------------------------------------------
OBEY
OPERATOR TCPMAINT MAINT MPROUTE ROUTED DHCPD REXECD SNMPD SNMPQE
ENDOBEY
; -----------------------------------------------------------------
AUTOLOG
    FTPSERVE 0
ENDAUTOLOG

PORT
  20 TCP FTPSERVE NOAUTOLOG ; FTP Server
  21 TCP FTPSERVE          ; FTP Server
  23 TCP INTCLIEN          ; TELNET Server
; 25 TCP SMTP              ; SMTP Server
...
====> file
```

These changes will take effect after you IPL you system again.

## IPL the system again (re-IPL)

You might want to shut down and re-IPL z/VM without having to access the HMC. Often, the HMC is logged off and thus the Integrated 3270 console (SYSG) is not available. Because of these factors, it is useful to use the System Console (SYSC), which has a title of Operating System Messages on the HMC, to be able to shut down z/VM and re-IPL it without having to use the console. This console is always accessible whether you are logged on to the HMC or not. z/VM messages during both the shutdown and re-IPL processes are written to the system console, but often you can ignore them; you simply want your system back in a few minutes over the network.
