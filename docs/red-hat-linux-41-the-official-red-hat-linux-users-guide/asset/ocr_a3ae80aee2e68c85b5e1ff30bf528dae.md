+   3. At the Setup menu, select Manage boot selection menu...
+   4. In the Boot selections menu, choose Add a boot selection
+   5. Choose Floppy Disk 0
+   6. Enter \nlinload.exe as the osloader directory and name
+   7. Say "yes" to the operating system being on the same partition as the osloader
+   8. Enter "/" as the operating system root directory
+   9. I usually enter "Linux" as the name for this boot selection
+   10. Say "No" you do not want to initialise the debugger at boot time
+   11. You should now be back in the Boot selections menu, choose the Change a boot selection option and pick the selection you just created as the one to edit
+   12. Use down arrow \downarrow to get OSLOADFILENAME up and then type in the name of the Milo image that you wish to use, for example noname.arc Return
+   13. Press Esc to get back to the Boot Selections menu
+   14. Choose Setup Menu (or hit Esc again) and choose Supplementary menu, and save changes option
+   15. Esc will get you back to the Boot menu and you can attempt to boot Milo. If you do not want Linux as the first boot option, then you can alter the order of the boot options in the Boot selections menu.

At the end of all this, you should have a boot selection that looks something like:

```
LOADIDENTIFIER=Linux
SYSEMPARTITION=muli(0)disk(0)fdisk(0)
OSLOADER=muli(0)disk(0)fdisk(0)\nlinload.exe
OSLOADPARTITION=muli(0)disk(0)fdisk(0)
OSLOADFILENAME=\noname.arc
OSLOADOPTIONS=
```