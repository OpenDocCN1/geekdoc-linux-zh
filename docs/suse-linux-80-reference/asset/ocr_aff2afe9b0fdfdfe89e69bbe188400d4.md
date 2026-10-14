+   2. Go to the folder or position on your desktop to which to save your Linux icon. Press the right mouse button and click ‘Add Link’.
+   
+   3. Highlight the link you just made, press the right mouse button and click ‘Properties’. Go to the ‘Application’ tab and click the button ‘Advanced’ below. Check the box ‘MS-DOS Mode’ in the dialog. Confirm with ‘OK’.
+   
+   4. You can use the ‘Other Icon’ browse button to search for a nice icon then give the link a suitable name. Done!
+   
+   5. Double-clicking the new icon takes you to a dialog confirming that Windows 95 is now entering MS-DOS mode. If this dialog bothers you, disable it in the link properties.

# The Windows Boot Menu

Configure a boot menu for Windows 95:

+   1. First, edit the file `c:\msdos.sys`. To do so, make the file visible by entering

```
C:> attrib -R -S -H c:\msdos.sys
```

This is a text file in which you need to enter some lines to activate the special Windows 95 boot menu. The lines below the `[Options]` label should look similar to those shown in File 10.

```
[Options]
BootGUI=0
BootDelay=0
BootMenu=0
Logo=0
```

*File 10: msdos.sys for Booting Linux*

The Logo=0 parameter is optional and prevents Windows 95 from switching to graphical mode before booting. This will speed up the booting process and make things easier later, in case at some point you want to use the DOS emulator in Linux.

The BootGUI=0 parameter causes Windows 95 to boot directly to DOS mode. After editing the file, reset the attributes. Then enter

```
C:> win
```

at the DOS prompt to start Windows, although our sample file c:\autoexec.bat will already do this, if you have chosen Win95 in the menu.