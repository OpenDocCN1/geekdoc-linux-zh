```
putting file HDNISO1_de.NTF as \W32X86\HDNISO1_de.NTF
```

Whew - that was a lot of typing! Most drivers are a lot smaller-many have only three generic PostScript driver files plus one PPD. While we did retrieve the files from the 2 subdirectory of the w32x86 directory from the Windows box, we do not put them (for now) in this same subdirectory of the Samba box. This relocation will automatically be done by the addriver command, which we will run shortly (and do not forget to also put the files for the Windows 9x/Me architecture into the \WIN4O\ subdirectory should you need them).

# 20.6.2.4 smbclient to Confirm Driver Installation

For now we verify that our files are there. This can be done with **smbclient**, too (but, of course, you can log in via SSH also and do this through a standard UNIX shell access):

```
root# smbclient //SAMBA-CUPS/print/$ -U 'root/xxxxx' \\
-c 'cd W32X86; pwd; dir; cd 2; pwd; dir'
added interface ip=10.160.51.60 bcast=10.160.51.255 nmask=255.255.252.0
Got a positive name query response from 10.160.51.162 ( 10.160.51.162 )
Domain=[CUPS-PRINT] OS=[UNIX] Server=[Samba 2.2.8a]

Current directory is \\ SAMBA-CUPS \ print$ \ W32X86\ :
D 0 Sun May 4 03:56:35 2003
. D 0 Thu Apr 10 23:47:40 2003
.. D 0 Sun May 4 03:56:18 2003
2 D 0 Sun May 4 03:56:18 2003
HDNISO1Aux.dll A 15356 Sun May 4 03:58:59 2003
Hdcm91c1KMW.in.DLL A 46966 Sun May 4 03:58:59 2003
HDNISO1_de.DLL A 434400 Sun May 4 03:58:59 2003
HDNISO1_de.NTF A 790404 Sun May 4 03:58:35 2003
Hddm91c1_de.DLL A 876544 Sun May 4 03:58:59 2003
Hddm91c1_de.INI A 101 Sun May 4 03:58:59 2003
Hddm91c1_de.dat A 5044 Sun May 4 03:58:59 2003
Hddm91c1_de.def A 428 Sun May 4 03:58:59 2003
Hddm91c1_de.hlp A 37699 Sun May 4 03:58:59 2003
Hddm91c1_de.lpr A 323584 Sun May 4 03:58:59 2003
Hddm91c1_de.ppd A 26373 Sun May 4 03:58:59 2003
Hddm91c1_de.vnd A 45056 Sun May 4 03:58:59 2003
HDNIS01U_de.DLL A 165888 Sun May 4 03:58:59 2003
HDNIS01U_de.HLP A 19770 Sun May 4 03:58:59 2003
Hddm91c1_de_reg.HLP A 228417 Sun May 4 03:58:59 2003
40976 blocks of size 262144. 709 blocks available

Current directory is \\ SAMBA-CUPS \ print$ \ W32X86 \ 2\ :
D 0 Sun May 4 03:56:18 2003
. D 0 Sun May 4 03:56:35 2003
.. A 434400 Sat May 3 23:18:45 2003
ADOBEPS5.DLL A 434400 Sat May 3 23:18:45 2003
```