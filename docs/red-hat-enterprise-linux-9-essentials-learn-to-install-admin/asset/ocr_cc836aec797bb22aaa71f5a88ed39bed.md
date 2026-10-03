# Sharing Files between RHEL 9 and Windows Systems with Samba

![](bbox=[0.34, 0.07, 0.71, 0.31])

Figure 19-4

Entering the username and password will result in the shared resources configured for that user appearing in the explorer window, including the previously configured */sampleshare* resource:

![](bbox=[0.43, 0.42, 0.63, 0.48])

Figure 19-5

Double-clicking on the */sampleshare* shared resource will display a listing of the files and directories contained therein.

If you are unable to see the Linux system or have problems accessing the shared folder, try mapping the Samba share to a local Windows drive as follows:

+   1. Open Windows File Explorer, right-click on the Network entry in the left-hand panel, and select *Map network drive...* from the resulting menu.
2. Select a drive letter from the Map Network Drive dialog before entering the path to the shared folder. For example:

```
\\LinuxServer\sampleshare
```

Enable the checkbox next to *Connect using different credentials*. For example, if you do not want the drive to be mapped each time you log into the Windows system, turn off the corresponding check box: