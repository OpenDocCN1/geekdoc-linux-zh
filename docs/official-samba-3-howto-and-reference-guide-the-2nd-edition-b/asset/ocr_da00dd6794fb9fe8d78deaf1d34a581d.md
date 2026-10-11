# 21.10.4 Recognizing Different Driver Files

The CUPS drivers do not support the older Windows 95/98/Me, but only the Windows NT/2000/XP client.

Windows NT, 2000, and XP are supported by:

+   - cups.hlp
+   - cupsdrv.dll
+   - cupsui.dll

Adobe drivers are available for the older Windows 95/98/Me as well as for Windows NT/2000/XP clients. The set of files is different from the different platforms.

Windows 95, 98, and ME are supported by:

+   - ADFONT5.MFM
+   - ADOBEPS4.DRV
+   - ADOBEPS4.HLP
+   - DEFFPRTR2.PPD
+   - ICONLIB.DLL
+   - PSMON.DLL

Windows NT, 2000, and XP are supported by:

+   - ADOBEPS5.DLL
+   - ADOBEPSU.DLL
+   - ADOBEPSU.HLP

![](bbox=[0.0, 0.78, 0.06, 0.8])

If both the Adobe driver files and the CUPS driver files for the support of Windows NT/200x/XP are presently installed on the server, the Adobe files will be ignored and the CUPS files will be used. If you prefer — for whatever reason — to use Adobe-only drivers, move away the three CUPS driver files. The Windows 9x/Me clients use the Adobe drivers in any case.