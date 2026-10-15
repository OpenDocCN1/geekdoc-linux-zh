
3. The operating system brings the CP owned volumes online, such as those used for paging, spool, and t-disk.
4. Depending on how it was started (see 5.2.2, "Warm start, force start, cold start, and clean start" on page 234), z/VM reads the information about systems attributes saved in the checkpoint and warm start data files² during last shutdown and restores them.
5. System prompts for set up of time-of-day (TOD).
6. The user directory, with the user's definitions, is brought online.
7. Existing spool files are made available.
8. All connected I/O is brought online and made available.
9. User volumes defined in SYSTEM CONFIG are made available.
10. The OPERATOR user is logged on.
11. The OPERATOR virtual machine starts the logging/accounting/symptom services by logging on the erep, diskacct and opersymp users.
12. The OPERATOR user ID autologs AUTOLOG1.
13. AUTOLOG1 starts any other virtual machine that it has been instructed to start according to its PROFILE EXEC.
14. Services machines send messages to OPERATOR on initialization status.

## Example 5-1 z/VM IPL process.

```
14:58:30 z/VM V5 R3.0 SERVICE LEVEL 0703 (64-BIT)
14:58:31 SYSTEM NUCLEUS CREATED ON 2008-05-23 AT 10:40:19, LOADED FROM LX6RES
14:58:31
14:58:31 **********************************************************************
14:58:31 * LICENSED MATERIALS - PROPERTY OF IBM*                           *
14:58:31 *                                                                   *
14:58:31 * 5741-A06 (C) COPYRIGHT IBM CORP. 1983, 2007. ALL RIGHTS          *
14:58:31 * RESERVED. US GOVERNMENT USERS RESTRICTED RIGHTS - USE,           *
14:58:31 * DUPLICATION OR DISCLOSURE RESTRICTED BY GSA ADP SCHEDULE         *
14:58:31 * CONTRACT WITH IBM CORP.                                           *
14:58:31 *                                                                   *
14:58:31 * * TRADEMARK OF INTERNATIONAL BUSINESS MACHINES.                  *
14:58:31 **********************************************************************
14:58:31
14:58:31 HCPZCO6718I Using parm disk 1 on volume LX6RES (device 1B34).
14:58:31 HCPZCO6718I Parm disk resides on cylinders 39 through 158.
14:58:31 Start ((Warm|Force|COLD|CLEAN) (Drain) (Disable) (NODirect)
14:58:31      (NOAUTOLOG) or (SHUTDOWN)
14:58:59 WARM
14:58:59 NOW 14:58:59 EDT THURSDAY 2008-06-05
14:58:59 Change TOD clock (Yes|No)
14:59:03 NO
14:59:03 The directory on volume LX6RES at address 1B34 has been brought online.
14:59:05 HCPWRS2513I
14:59:05 HCPWRS2513I Spool files available      376
14:59:07 HCPWRS2512I Spooling initialization is complete.
14:59:07 DASD 1B35 dump unit CP IPL pages 17646
14:59:07 HCPAU2U700I System gateway VMGUEST identified.
14:59:07 z/VM Version 5 Release 3.0, Service Level 0703 (64-bit),
14:59:07 built on IBM Virtualization Technology
14:59:07 There is no logmsg data
14:59:07 FILES: 0031 RDR, 0009 PRT, NO PUN
14:59:07 LOGON AT 14:59:07 EDT THURSDAY 06/05/08
14:59:07 GRAF 0020 LOGON AS OPERATOR USERS = 1
14:59:07 HCPIOP962I 2048M system storage
14:59:07 FILES: 0000314 RDR, 0000030 PRT, 0000001 PUN
14:59:07 HCPCRC0802I Accounting records are accumulating for userid DISKACNT.
14:59:07 XAUTOLOG EREP
14:59:07 Command accepted
14:59:07 XAUTOLOG DISKACNT
14:59:07 Command accepted
14:59:07 XAUTOLOG AUTOLOG1
14:59:07 Command accepted
14:59:07 XAUTOLOG OPERSYMP
14:59:07 Command accepted
14:59:07 AUTO LOGON ***     EREP      USERS = 2   BY OPERATOR
14:59:07 AUTO LOGON ***     DISKACNT  USERS = 3   BY OPERATOR
14:59:07 AUTO LOGON ***     AUTOLOG1  USERS = 4   BY OPERATOR
14:59:07 AUTO LOGON ***     OPERSYMP  USERS = 5   BY OPERATOR
14:59:07 HCPCLS6056I XAUTOLOG information for EREP: The IPL command is verified by the IPL command processor.
14:59:07 HCPCLS6056I XAUTOLOG information for DISKACNT: The IPL command is verified by the IPL command processor.
14:59:07 HCPCLS6056I XAUTOLOG information for AUTOLOG1: The IPL command is verified by the IPL command processor.
14:59:07 HCPCLS6056I XAUTOLOG information for OPERSYMP: The IPL command is verified by the IPL command processor.
14:59:07 AUTO LOGON ***     VMSERVS   USERS = 6   BY AUTOLOG1
14:59:07 AUTO LOGON ***     VMSERVU    USERS = 7   BY AUTOLOG1
14:59:07 AUTO LOGON ***     VMSERVR   USERS = 8   BY AUTOLOG1
14:59:07 USER DSC   LOGOFF AS AUTOLOG1 USERS = 7
14:59:07 AUTO LOGON ***     DTCVSW1   USERS = 8   BY AUTOLOG1

² This file is stored in the system RES volume
