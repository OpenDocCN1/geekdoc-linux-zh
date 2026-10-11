# 20.6.2.3 Installing Driver Files into [print$]

We are now going to locate the driver files into the [print$] share. Remember, the UNIX path to this share has been defined previously in your smb.conf file. You also have created subdirectories for the different Windows client types you want to support. If, for example, your [print$] share maps to the UNIX path /etc/samba/drivers/, your driver files should now go here:

+   - For all Windows NT, 2000, and XP clients. /etc/samba/drivers/W32X86/, but not (yet) into the 2 subdirectory.
+   - For all Windows 95, 98, and Me clients, /etc/samba/drivers/WIN40/, but not (yet) into the 0 subdirectory.

We again use smbclient to transfer the driver files across the network. We specify the same files and paths as were leaked to us by running getdriver against the original Windows install. However, now we are going to store the files into a Samba/UNIX print server's [print$] share.

```
```
root# smbclient //SAMBA-CUPS/print$ -U'root/xxxx' -c \
'cd W32X86; put HDNISI01_de.DLL; \
put Hddm91c1_de.ppd; put HDNISI01_de.dll;   \
put HDNISIOU_de.HLP; put Hddm91c1_de.dll;    \
put Hddm91c1_de.INI; put Hddm91c1KMIN.DLL;   \
put Hddm91c1_de.dat; put Hddm91c1_de.dat;     \
put Hddm91c1_de.def; put Hddm91c1_de.hre;     \
put Hddm91c1_de.vnd; put Hddm91c1_de.hlp;     \
put Hddm91c1_de_reg.HLP; put HDNISOIAux.dll;  \
put HDNISI01_de.NTf'
```
```

```
```
added interface ip=10.160.51.60 bcast=10.160.51.255 netmask=255.255.252.0
Got a positive name query response from 10.160.51.162( 10.160.51.162)
Domain=[CUPS-PRINT] 0S=[UNIX] Server=[Samba 2.2.7a]
putting file HDNISI01_de.DLL as  W32X86HDNISI01_de.dll
putting file Hddm91c1_de.ppd as  W32X86/Hddm91c1_de.ppd
putting file HDNISIOU_de.dll as  W32X86/HDNISIOU_de.dll
putting file HDNISIOU_de.HLP as  W32X86/HDNISIOU_de.HLP
putting file Hddm91c1_de.dll as  W32X86/Hddm91c1_de.dll
putting file Hddm91c1_de.ini as  W32X86/Hddm91c1_de.ini
putting file Hddm91c1KMIn.dll as W32X86/Hddm91c1KMIn.dll
putting file Hddm91c1_de.dat as  W32X86/Hddm91c1_de.dat
putting file Hddm91c1_de.dat as  W32X86/Hddm91c1_de.dat
putting file Hddm91c1_de.def as  W32X86/Hddm91c1_de.def
putting file Hddm91c1_de.hre as W32X86/Hddm91c1_de.hre
putting file Hddm91c1_de.vnd as W32X86/Hddm91c1_de.vnd
putting file Hddm91c1_de.hlp as W32X86/Hddm91c1_de.hlp
putting file Hddm91c1_de_reg.HLP as W32X86/Hddm91c1_de_reg.HLP
putting file HDNISOIAux.dll as W32X86/HDNISOIAux.dll
```
```