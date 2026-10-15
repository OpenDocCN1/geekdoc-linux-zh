> Important: A minimal Linux guest system fits onto a single 3390-3 DASD, and this is the recommended practice in the field. This practice requires that you do not use GNOME or KDE window managers in order to retain the small size of the installed system. Our example does not do this because we want to show the use of LVM and KDE.

To avoid a one-cylinder gap being reported on each user volume, use the user ID $ALLOC$. This user is set to NOLOG which means it can never be logged onto. Thus, it is not a conventional user ID, rather it is a convenient place to put dummy minidisks definitions for cylinder 0 of all PERM volumes. The user ID $ALLOC$ is in the beginning of the USER DIRECT C, near line 100. Include a definition for each of your volumes, as shown in Example 4-15.

# Example 4-15 Avoiding a 1-cylinder gap being reported

```
00104 *
00105 USER $ALLOC$ NOLOG
00106 MDISK A01 3390 000 001 LX6RES R
00107 MDISK A02 3390 000 001 LX6W01 R
00108 MDISK A03 3390 000 001 LX6W02 R
00109 MDISK A04 3390 000 001 <NW1A25> R
00110 MDISK A05 3390 000 001 <NW1A26> R
00111 MDISK A06 3390 000 001 <NW1A27> R
00112 MDISK A07 3390 000 001 <NW1A28> R
00113 MDISK A08 3390 000 001 <NW1A29> R
00114 *
```

# Updating the autolog profile

The new Linux ID you defined must have access to the VSWITCH. To do his automatically when the system IPLs, add the SET VSWITCH command with the GRANT parameter to AUTOLOG1's PROFILE EXEC. Also, an XAUTOLOG statement can be added for your Linux user ID to be automatically logged on at z/VM IPL time.

To accomplish those, log in as MAINT and make sure your AUTOLOG1's profile looks like the one shown in Example 4-16.

# Example 4-16 Granting users access to the virtual switches

```
=> link autolog1 191 1191 mr
=> acc 1191 f
=> x profile exec f // add two lines
/*********************/
/* Autolog1 Profile Exec */
/*********************/
```