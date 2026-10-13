To make the user jsmith in the OU=ACCTG.O=CALDERA context a trustee of the OPENLINUX_SYS: groups\\acctg directory, and to assign read, write, and create rights, issue the following command:

```
```text
nwdsaddtrust -o /NetWare/NDS/NW-TREE/CALDERA/ACCTG/jsmith -r [RWC] -p /NetWare/_
NDS/NW-TREE/CALDERA/OPENLINUX_SYS/groups/acctg
```
```

If jsmith is already a trustee of the acctg directory, his rights will be overridden by the new assignment.

The xnwdstrustees utility gives you a graphical interface for managing trustee assignments for NetWare files and directories.

**TABLE 28.13 — COMMAND-LINE OPTIONS FOR xnwdstrustees**

| Options | Description |
|---|---|
| `-p <PATH>` | Directory or file to which trustees assignment is being added |
| `-h` | Displays command help |

To make the user jsmith in the OU=ACCTG.O=CALDERA context a trustee of the OPENLINUX_SYS: groups\\acctg directory, and to assign read, write, and create rights, issue the following command:

```
```text
xnwdstrustees -p /NetWare/NDS/NW-TREE/CALDERA/OPENLINUX_SYS/groups/acctg
```
```

The command brings up the graphical interface shown in Figure 28.5.

![](bbox=[0.204, 0.556, 0.661, 0.793])

After the window opens, you need to perform the following steps to accomplish the desired results:

+   1. Click Add Trustee in the Directory Trustees window.
+   2. Click the search icon next to the New Trustee field.
+   3. Navigate the NDS Tree to find jsmith.
+   4. Click jsmith and choose OK.