
> Hint: Use the Alt+Tab key sequence to conveniently move between the HMC window and 3270 console.

![](img/b0a4b9056f819dccd4781a5105c92d45_161_0.png)

Figure 4-7 Integrated 3270 Console icon

- 4. Place the "z/VM Product Package Version 5 Release 3.0" DVD in the HMC DVD drive.

- 5. Get into Single Object Operations mode, as follows:

> Note: On the z10, you do not have to go to Support Element (SE) mode to load from DVD.

- a. Double-click the Groups icon in the Views area.
- b. Double-click Defined CPCs in the Groups Work Area.
- c. Select your CPC.
- d. If necessary use the buttons with circular arrows on the bottom right corner to navigate to the CPC Recovery menu.
- e. Double-click the Single Object Operations icon. Click yes to confirm. Now a new window, Primary Support Element Workplace, should appear (on older HMC levels it will be a "window within a window"). A window about a certificate can appear. If so, click OK.
- f. Double-click Groups near the top of this window.
- g. Double-click Images in the Groups Work Area.

> Important: If you are unable to get into Single Object Operations mode, you might not have sufficient permission. Ask your system administrator.

- 6. Select the LPAR that z/VM will be installed into.

7. Go around the racetrack in this window to the CPC Recovery menu, shown in Figure 4-8.

![](img/b0a4b9056f819dccd4781a5105c92d45_162_0.png)

Figure 4-8 CPC Recovery menu

8. Double-click the Load from CD-ROM, DVD, or Server icon. The “Load from CD-ROM or Server” panel opens (Figure 4-9 on page 148).

## Load from CD-ROM or Server - SCZP201:A04

Use this task to load operating system software or utility programs from a CD-ROM / DVD or a server that can be accessed using FTP.
Select the source of the software:

- Hardware Management Console CD-ROM / DVD
- FTP Source

Host computer:
User ID:
Password:
Account (optional):
File location (optional): /cpdvd

OK Cancel Help

Figure 4-9 Load from CD-ROM or Server panel

- 9. Select the Hardware Management Console CD-ROM/DVD button, if it is not already selected.
- 10. Type /cpdvd in the File location field. This is the directory on the DVD with the z/VM 5.3 installation code.
- 11. Click OK.
- 12. Load the ramdisk. A list of software is displayed in the "Load from CD-ROM or Server" panel. To load the ramdisk:

- a. Select, if it is not already selected, the software 530vm.ins as shown in Figure 4-10 on page 149, and then click OK.

![](img/b0a4b9056f819dccd4781a5105c92d45_164_0.png)

Figure 4-10 Selecting z/VM 5.3 ramdisk system

- b. In the "Confirm the action" window, click Yes. You should see the "Load from CD-ROM, DVD or Server Progress" window. The green light on the DVD drive should light up.

- c. When you see the message Completed successfully, click OK to close. This usually takes about four to six minutes.

> Attention: Although the z/VM ramdisk (IBMVMMRAM) loads in about four to six minutes, slow load times have been observed (15-18 minutes). When the green light on the DVD drive is solid, the load time is acceptable. When it is intermittently dark more than it is green, long load times can result.

You should now have an in-memory z/VM 5.3 system running. The tasks performed in this section are similar to loading a Linux kernel onto memory for installation. You can compare this section with section 4.4.2, "Booting the Linux kernel for installation" on page 199 and later verify that both systems load an image to main memory before the installation commences. One difference is that Linux starts the installation program automatically, whereas in z/VM you must invoke a command as stated in the next section.

## Copying a z/VM system image to DASD

To copy z/VM to DASD:

- 1. Get out of Single Object Operations mode by logging off the primary SE window by closing that window.

- 2. Use the Alt+Tab sequence to move to the Integrated 3270 console window. The ramdisk IPLs and the system come up with the MAINT user ID logged on. You should see z/VM boot as shown in Figure 4-11 on page 150.
