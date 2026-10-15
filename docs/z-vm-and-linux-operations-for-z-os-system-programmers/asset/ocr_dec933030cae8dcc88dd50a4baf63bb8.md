a. Press the Tab key to traverse to the IPL Parameters section, as shown in Figure 4-15, and enter the value cons=sysg. This specifies the use of Integrated 3270 console.

![](bbox=[0.27, 0.2, 0.85, 0.5])

Figure 4-15 IPL parameters.

b. Press the F10 key to continue the IPL of your z/VM system. This can be approximately 2-3 minutes.

7. At the Start (Warm|Force|COLD|CLEAN) prompt, enter the following command:
==> cold drain noautolog

8. At the Change TOD clock prompt enter:
==> no
The last message is:
HCPCRC8082I EREP records are accumulating for userID EREP

9. Disconnect from the OPERATOR user ID by using the DISCONNECT command (or its abbreviated form: DISC):
==> disc

10. Press Enter to open a new logon window.

# Completing the z/VM installation

To complete the z/VM installation:

1. On the z/VM login window, log on as MAINT. The password is MAINT. You might receive messages HCPLMN108E or DMSACP113S about disks not linked or attached. This is not a problem. Press Enter when you see the VM Read prompt in the lower right corner.