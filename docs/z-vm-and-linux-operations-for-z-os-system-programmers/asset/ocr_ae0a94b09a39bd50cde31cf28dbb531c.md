Important: By defining the PROFILE EXEC as we did, you could not AUTOLOG this machine and have the z/OS system IPL automatically. The file does not contain any statements to actually IPL the z/OS image.

Instead of placing the statements and commands necessary to perform an IPL of the z/OS image in the profile, we created an exec to actually perform this. In short, this exec performs the following tasks:

+   1. Switches the mode of the console to 3270
+   2. Issues command SET RUN ON
+   3. IPLs the z/OS image

The contents of the IPLSC59 EXEC is shown in Figure 4-38.

```
IPLSC59 EXEC      A1  V 130  Trunc=130 Size=14 Line=0 Col=1 Alt=2
00000 * * * Top of File * * *
00001 /* Exec to IPL the SC59 guest system */
00002 trace 'o'
00003 'vmfclear'
00004 cmd = 'TERM CONMODE 3270' || '15'X
00005 cmd = cmd || 'SET RUN ON' || '15'X
00006 say '**************************************************'
00007 say '*'
00008 say '*    This is a z/OS 1.9 system,'
00009 say '*    WAIT, the system is coming up... SC59'
00010 say '*'
00011 say '**************************************************'
00012 cmd = cmd || 'IPL D42A LOADPARM C73059M1 CLEAR'
00013 push cmd
00014 exit
00015 * * * End of File * * *
```

Figure 4-38 Contents of IPL

Significant items in the IPLSC59 exec are described in the following list:

+   TERM CONMODE 3270    This switches the mode (or terminal type) to 3270.
+   '15'x    This is the end-of-line indicator that occurs after each command. The commands themselves are stacked and are issued after the exec has ended (not controlled by any logic in the exec itself).