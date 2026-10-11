TrueType Download Options choose *Outline*. Use PostScript Level 2 if you are having trouble with a non-PS printer and if there is a choice.

# 21.19.17 cupaddsmmb Does Not Work with Newly Installed Printer

**Symptom:** The last command of **cupaddsmmb** does not complete successfully. If the **cmd** = **smdriver printername printername** result was **NT_STATUS_UNSUCCESSFUL**, then possibly the printer was not yet recognized by Samba. Did it show up in Network Neigh- boorhood? Did it show up in **rpcclient hostname** -c **'enumprinters’**? Restart smbd (or send a **kill -HUP** to all processes listed by **smbstatus**, and try again.

# 21.19.18 Permissions on /var/spool/samba/ Get Reset After Each Re- boot

Have you ever by accident set the CUPS spool directory to the same location (*Reque- stRoot* /var/spool/samba/ in **cupsd.conf** or the other way round: /var/spool/cups/ is set as *path>* in the **printers** section)? These *must be different*. Set **RequestRoot** /var/spool/cups/ in **cupsd.conf** and *path* = /var/spool/samba in the *printers* section of **smb.conf**. Otherwise, cupsd will sanitize permissions to its spool directory with each restart and printing will not work reliably.

# 21.19.19 Print Queue Called "lp" Mishandles Print Jobs

In this case a print queue called "lp" intermittently swallows jobs and spits out completely different ones from what was sent.

It is a bad idea to name any printer "lp". This is the traditional UNIX name for the default printer. CUPS may be set up to do an automatic creation of Implicit Classes. This means, to group all printers with the same name to a pool of devices and load-balance the jobs across them in a round-robin fashion. Chances are high that someone else has a printer named "lp" too. You may receive that person's jobs and send your own to his or her device unwittingly. To have tight control over the printer names, set **BrowseShortNames No**. It will prevent any printer as **printername@cupshot**, which gives you better control over what may happen in a large networked environment.

# 21.19.20 Location of Adobe PostScript Driver Files for "cupaddsmmb"

Use **smbclient** to connect to any Windows box with a shared PostScript printer: **smbclient //windowsbox/print/$ -U guest**. You can navigate to the **W32X86/2** subdir to **mget ADOBE\*** and other files or to **WIN40/0** to do the same. Another option is to download the **\*.exe** packaged files from the Adobe Web site.

# 21.20 Overview of the CUPS Printing Processes

A complete overview of the CUPS printing processes can be found in Figure 21.19.