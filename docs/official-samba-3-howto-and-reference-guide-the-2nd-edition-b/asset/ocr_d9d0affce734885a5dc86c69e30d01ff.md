+   • The CUPS PostScript driver will be the heart of the fully fledged CUPS IPP client for Windows NT/2000/XP to be released soon (probably alongside the first beta release for CUPS 1.2).

# ### 21.10.9 Run cupsaddsmb (Quiet Mode)

The **cupsaddsmb** command copies the needed files into your *\$print$* share. Additionally, the PPD associated with this printer is copied from */etc/cups/ppd/* to */print$*. There the files wait for convenient Windows client installations via Point’n’Point. Before we can run the command successfully, you need to be sure that we can authenticate toward Samba. If you have a small network, you are probably using user-level security (security = user).

Here is an example of a successfully run **cupsaddsmb** command:

```
root# cupsaddsmb -U root infotec_IS2027
Password for root required to access localhost via Samba: ['secret']
```

To share *all* printers and drivers, use the -a parameter instead of a printer name. Since **cupsaddsmb** “exports” the printer drivers to Samba, it should be obvious that it only works for queues with a CUPS driver associated.

# ### 21.10.10 Run cupsaddsmb with Verbose Output

Probably you want to see what’s going on. Use the -v parameter to get a more verbose output. The output below was edited for better readability: all `\` at the end of a line indicate that I inserted an artificial line break plus some indentation here.

```
root# cupsaddsmb -U root -v infotec_2105
Password for root required to access localhost via GANDALF:
Running command: smbclient //localhost/print$ -N -U'root/secret' \
 -c 'mkdir W32X86; \\
 put /var/spool/cups/tmp/3e9bf2f4333b5 W32X86/infotec_2105.ppd; \\
 put /usr/share/cups/drivers/cupsdrv.dl1 W32X86/cupsdrv.dl1; \\
 put /usr/share/cups/drivers/cupsui.dll W32X86/cupsui.dll; \\
 put /usr/share/cups/drivers/cups.hlp W32X86/cups.hlp'
added interface ip=10.160.51.60 bcst=10.160.51.255 mask=255.255.252.0
Domain=[CUPS-PRINT] OS=[UNIX] Server=[Samba 2.2.7a]
NT_STATUS_OBJECT_NAME_COLLISION making remote directory W32X86
putting file /var/spool/cups/tmp/3e9bf2f4333b5 as W32X86/infotec_2105.ppd
putting file /usr/share/cups/drivers/cupsdrv.dl1 as W32X86/cupsdrv.dl1
putting file /usr/share/cups/drivers/cupsui.dll as W32X86/cupsui.dll
putting file /usr/share/cups/drivers/cups.hlp as W32X86/cups.hlp

Running command: rpcclient localhost -N -U'root/secret' \
 -c 'adddriver "WINDOWS NT x86"'
```