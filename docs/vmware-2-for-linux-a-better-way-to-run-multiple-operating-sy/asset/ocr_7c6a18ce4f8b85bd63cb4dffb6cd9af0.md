# Installing and Configuring Windows 3.1

There is very little difference between a Windows 3.1 and Windows for Workgroups (3.11) installation, so I make no special mention of the differences except the obvious extra network configuration step in Windows for Workgroups:

+   1. Start with a fresh reboot of the DOS virtual machine you just prepared for Windows 3.1.

+   2. If you are installing Windows from floppies, remove any CD-ROMs from the drive. Windows scans all attached drives for Windows-compatible programs and creates program groups and icons for programs on your CD, which in most cases is a bad idea.

+   3. Start the Windows 3.1 installation by typing setup at the appropriate drive prompt. The Microsoft "blue screen" installer appears, as seen in Figure 14.19.

![](bbox=[0.08, 0.51, 0.56, 0.78])

Figure 14.19 Windows 3.1 installation starts with a text screen.

+   4. Press Enter to start the installation. When prompted, you can safely select an Express Setup unless you specifically know you want to avoid installing certain Windows components.

+   5. Windows 3.1 scans the virtual machine for hardware (not especially well) and then copies files to the virtual disk (see Figure 14.20).

+   6. Soon after, the Windows graphical environment will load, and your mouse pointer should work. If you are installing Windows for Workgroups, Windows tries (and fails) to identify your network card. When asked to enter your name, organization, and serial number as shown in Figure 14.21, follow the prompts and click Continue.