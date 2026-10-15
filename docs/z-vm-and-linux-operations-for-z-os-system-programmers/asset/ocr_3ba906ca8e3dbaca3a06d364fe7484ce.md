+   3. The operating system brings the CP owned volumes online, such as those used for paging, spool, and t-disk.
+   4. Depending on how it was started (see 5.2.2, "Warm start, force start, cold start, and clean start" on page 234), z/VM reads the information about systems attributes saved in the checkpoint and warm start data files² during last the shutdown and restores them.
+   5. System prompts for set up of time-of-day (TOD).
+   6. The user directory, with the user's definitions, is brought online.
+   7. Existing spool files are made available.
+   8. All connected I/O is brought online and made available.
+   9. User volumes defined in SYSTEM CONFIG are made available.
+   10. The OPERATOR user is logged on.
+   11. The OPERATOR virtual machine starts the logging/accounting/symptom services by logging on the erep, diskacct and opersymp users.
+   12. The OPERATOR user ID autologs AUTOLOG1.
+   13. AUTOLOG1 starts any other virtual machine that it has been instructed to start according to its PROFILE EXEC.
+   14. Services machines send messages to OPERATOR on initialization status.

Example 5-1 shows the output of a z/VM IPL process. Interactions with the console are in bold.

# Example 5-1 z/VM IPL process.

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
```

> ² This file is stored in the system RES volume