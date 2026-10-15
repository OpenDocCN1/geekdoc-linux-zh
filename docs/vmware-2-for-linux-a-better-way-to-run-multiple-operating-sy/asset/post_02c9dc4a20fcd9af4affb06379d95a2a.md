
![](img/b2b6702758c230ce537468351fc8af15_314_0.png)

Figure 14.25 Enable the network protocols you plan to use in Windows 3.1.

18. After setup scans your hard drive for Windows-compatible programs, you are prompted to restart the virtual machine. Click Restart Computer.

19. When the virtual machine is finished rebooting, type win at the DOS prompt to launch Windows.

20. If you are running Windows for Workgroups, you are prompted for your username and password for Microsoft Networking.

21. The Windows 3.1 GUI should appear, as it does in Figure 14.26.

![](img/b2b6702758c230ce537468351fc8af15_314_1.png)

Figure 14.26 The Windows 3.1 GUI, ready to go.

22. You are free to run built-in Windows 3.1 applications or install new software. Remember that you are limited to a 640×480, 16-color Windows desktop because VMware Tools is not available for Windows 3.1.

> If you are using DR DOS, you should be aware that installing Windows alters the DOS command path. Normally, the DR DOS setup.exe program is available from any prompt, but after you install Windows, typing setup invokes the Windows setup program instead. You can either edit the autoexec.bat file to change the order of the path or simply run setup.exe from the C:\DRDOS directory when you want to change DOS settings.

## Installing Sound Support in Windows 3.1

If you want native Windows programs to have access to the virtual sound device, you need to install a Windows 3.1-compatible driver. You should have already downloaded the sbbasic.exe package from Creative Labs technical support and decompressed it to a new directory:

- 1. Exit Windows 3.1.
- 2. Change to the directory with the contents of the sbbasic.exe archive. (I recommend c:\sb16.)
- 3. Run install.exe. When the installation main menu appears, press Enter to continue.
- 4. The installation program asks you to verify your system directories, as shown in Figure 14.27. Unless you have extensively customized your virtual machine, the defaults should be correct.
- 5. The installation program might mistakenly think 16-bit DMA is on channel 5. If this happens, change the setting to 7. Your screen should match Figure 14.28.
- 6. Select Proceed when the settings are complete.
- 7. The installer prompts you to accept changes to your system configuration files. Accept the changes by pressing Enter.
- 8. You can safely replace any Windows configuration files when asked. Chances are, it will be a MIDI file, which is irrelevant because the VMware sound emulation does not support MIDI.
- 9. When the installation is complete, press F10 to restart the virtual machine.

![](img/b2b6702758c230ce537468351fc8af15_316_0.png)

Figure 14.27 The SoundBlaster driver installation is largely automated.

![](img/b2b6702758c230ce537468351fc8af15_316_1.png)

Figure 14.28

- 10. When you reboot, you see a message claiming that the SoundBlaster settings are invalid. Ignore it; the diagnostics program has trouble reading the virtual device, but SoundBlaster is working.
- 11. You might want to remove the entry in the autoexec.bat file that refers to address 330 and T6 by simply erasing them. These settings affect the MIDI device, which is not available in VMware.
- 12. When you restart Windows, you should hear a short jingle. Sound is available in Windows 3.1.

## Conclusion

It may seem humble, or a backwards OS best left in the past, but if you are at all a computer enthusiast, I suspect you'll be quite pleased to see DOS up and running once more.

No, I don't think that you should spend all your time on it, or that it is by any means the best use of your investment in VMware, but a DOS virtual machine has a surprising amount of power and flexibility. It also gives you a good excuse to de-mothball all that old software you have lying around.

## Chapter 15: Playing Games with VMware

The bad news: compatibility hurdles

The good news: games that work

Configuration tips for games
