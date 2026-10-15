
![](img/b0a4b9056f819dccd4781a5105c92d45_169_0.png)

*Figure 4-14 Load panel*

3. **Follow these steps:**
   a. For the load type, select the **Clear** button.
   b. Set the load address to be the new system residence (530RES) volume, which is `<1A20>` in this example.
   c. Set the load parameter to **SYSG**. This specifies to use the Integrated 3270 console.
   d. Click **OK** to load.
4. When the Load Task Confirmation window opens, click **Yes**.
5. After approximately 1-3 minutes, when the word **Success** appears in the Load Program window, click **OK**.
6. Use the **Alt+Tab** sequence to move back to the Integrated 3270 console window. The **STAND ALONE PROGRAM LOADER** panel opens.

a. Press the Tab key to traverse to the IPL Parameters section, as shown in Figure 4-15, and enter the value cons=sysg. This specifies the use of Integrated 3270 console.

![](img/b0a4b9056f819dccd4781a5105c92d45_170_0.png)

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

## Completing the z/VM installation

To complete the z/VM installation:

1. On the z/VM login window, log on as MAINT. The password is MAINT. You might receive messages HCPLMN108E or DMSACP113S about disks not linked or attached. This is not a problem. Press Enter when you see the VM Read prompt in the lower right corner.

Important: When logging on to a z/VM user ID that runs CMS, press Enter at the VM READ prompt. This results in a prompt of the form:
Ready; T=0.01/0.01 11:14:20

2. Issue the ipl cms command and then press Enter, as indicated. The Ready; prompt appears.

```
==> ipl cms
==> (Press the Enter key)
Ready;
```

3. Run the INSTVM DVD command:

```
==> instvm dvd
...
HCPP LD8329I POSTLOAD EXEC ENDED SUCCESSFULLY
...
HCPIVM8392I INSTVM ENDED SUCCESSFULLY
```

The EXEC continues the installation process. This step takes about 4-8 minutes. The last message is:
HCPIVM8392I INSTVM ENDED SUCCESSFULLY

4. Load the recommended service. For z/VM 5.3, the service name is 5301RSU1. Run the following commands:

```
==> ipl cms
==> Press Enter
Ready;
==> acc 500 c
DMSACC7241 500 replaces C (2CC)
==> listfile * * c
5301RSU1 SERVLINK C1
==> service all 5301rsu1
```

This step takes about 3-6 minutes. The last message is:
VMFSRV2760I SERVICE processing completed successfully

5. IPL CMS and run the PUT2PROD command. This puts the service into production:

```
==> ipl cms
==> Press Enter
Ready;
==> put2prod
```

This step takes about 2-4 minutes. The last message is:
VMFP2P2760I PUT2PROD processing completed successfully

A return code of 0 is ideal. You might receive a return code of 4 and the message:

```
VMFP2P27601 PUT2PROD process completed with warnings
```

In general on z/VM, a return code of 4 is acceptable. That means that only warnings were issued. A return code of 8 or greater generally means that errors were encountered.

6. Enter the following command to shutdown and IPL your system again:

```text
==> shutdown repl
SYSTEM SHUTDOWN STARTED
```

Although you lose your 3270 session, the system returns in about 2-4 minutes. After it does, the last message is:

```text
Press enter or clear key to continue
```

7. Press Enter. The z/VM logon window opens.

Congratulations! You now have a vanilla z/VM system installed.

## Configuring the PROFILE XEDIT file

When invoked, the XEDIT command looks for the file PROFILE XEDIT configuration file. Many z/VM user IDs do not have such a personal or shared system file, so all XEDIT default values are in effect. The MAINT 191 (A) disk has a PROFILE XEDIT file, so when you are editing files on MAINT, the values in this profile are usually in effect.

To have a good experience while using XEDIT, make the profile for the MAINT user be similar to the one in Example 2-25 on page 92. To do this, log on to MAINT and edit the file with XEDIT itself:

```
==> xedit profile xedit a
```

Save your changes with the XEDIT subcommand SAVE.
