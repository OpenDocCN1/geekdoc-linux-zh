
## 20.5.5 The [print$] Share Directory

In order for a Windows NT print server to support the downloading of driver files by multiple client architectures, you must create several subdirectories within the `[print$]` service (i.e., the UNIX directory named by the `path` parameter). These correspond to each of the supported client architectures. Samba follows this model as well. Just like the name of the `[print$]` share itself, the subdirectories must be exactly the names listed below (you may leave out the subdirectories of architectures you do not need to support).

Therefore, create a directory tree below the `[print$]` share for each architecture you wish to support like this:

```
[print$]--
|---W32X86    # serves drivers to Windows NT x86
|---WIN40     # serves drivers to Windows 95/98
|---W32ALPHA  # serves drivers to Windows NT Alpha_AXP
|---W32MIPS   # serves drivers to Windows NT R4000
|---W32PPC    # serves drivers to Windows NT PowerPC
```

### REQUIRED PERMISSIONS

- The account used to connect to the Samba host must have a UID of 0 (i.e., a root account).
- The account used to connect to the Samba host must be named in the `printer admin` list.

Of course, the connected account must still have write access to add files to the subdirectories beneath `[print$]`. Remember that all file shares are set to "read-only" by default.

Once you have created the required `[print$]` service and associated subdirectories, go to a Windows NT 4.0/2000/XP client workstation. Open **Network Neighborhood** or **My Network Places** and browse for the Samba host. Once you have located the server, navigate to its **Printers and Faxes** folder. You should see an initial listing of printers that matches the printer shares defined on your Samba host.

## 20.6 Installing Drivers into [print$]

Have you successfully created the [print$] share in **smb.conf**, and have you forced Samba to reread its **smb.conf** file? Good. But you are not yet ready to use the new facility. The client driver files need to be installed into this share. So far, it is still an empty share. Unfortunately, it is not enough to just copy the driver files over. They need to be correctly installed so that appropriate records for each driver will exist in the Samba internal databases so it can provide the correct drivers as they are requested from MS Windows clients. And that is a bit tricky, to say the least. We now discuss two alternative ways to install the drivers into [print$]:

- Using the Samba command-line utility **rpcclient** with its various subcommands (here, **adddriver** and **setdriver**) from any UNIX workstation.
- Running a GUI (**Printer Properties** and **Add Printer Wizard**) from any Windows NT/2000/XP client workstation.

The latter option is probably the easier one (even if the process may seem a little bit weird at first).

### 20.6.1 Add Printer Wizard Driver Installation

The printers initially listed in the Samba host’s **Printers** folder accessed from a client’s Explorer will have no real printer driver assigned to them. By default this driver name is set to a null string. This must be changed now. The local **Add Printer Wizard** (APW), run from NT/2000/XP systems, will help us in this task.

Installation of a valid printer driver is not straightforward. You must attempt to view the printer properties for the printer to which you want the driver assigned. Open Windows Explorer, open **Network Neighborhood**, browse to the Samba host, open Samba’s **Printers** folder, right-click on the printer icon, and select **Properties...** You are now trying to view printer and driver properties for a queue that has this default **NULL** driver assigned. This will result in the following error message: "Device settings cannot be displayed. The driver for the specified printer is not installed, only spooler properties will be displayed. Do you want to install the driver now?"

Do *not* click on **Yes!** Instead, click on **No** in the error dialog. Now you will be presented with the printer properties window. From here, the way to assign a driver to a printer is open. You now have the choice of:

- Select a driver from the pop-up list of installed drivers. Initially this list will be empty.
- Click on **New Driver** to install a new printer driver (which will start up the APW).

Once the APW is started, the procedure is exactly the same as the one you are familiar with in Windows (we assume here that you are familiar with the printer driver installations procedure on Windows NT). Make sure your connection is, in fact, set up as a user with *printer admin* privileges (if in doubt, use **smbstatus** to check for this). If you wish to install printer drivers for client operating systems other than Windows NT x86, you will need to use the **Sharing** tab of the printer properties dialog.

Assuming you have connected with an administrative (or root) account (as named by the `printer admin` parameter), you will also be able to modify other printer properties such as ACLs and default device settings using this dialog. For the default device settings, please consider the advice given further in Section 20.6.2.

### 20.6.2 Installing Print Drivers Using rpcclient

The second way to install printer drivers into `print$` and set them up in a valid way is to do it from the UNIX command line. This involves four distinct steps:

1. Gather information about required driver files and collect the files.
2. Deposit the driver files into the `print$` share's correct subdirectories (possibly by using `smbclient`).
3. Run the `rpcclient` command-line utility once with the `adddriver` subcommand.
4. Run `rpcclient` a second time with the `setdriver` subcommand.

We provide detailed hints for each of these steps in the paragraphs that follow.

#### 20.6.2.1 Identifying Driver Files

To find out about the driver files, you have two options. You can check the contents of the driver CD-ROM that came with your printer. Study the `*.inf` files located on the CD-ROM. This may not be possible, since the `*.inf` file might be missing. Unfortunately, vendors have now started to use their own installation programs. These installation packages are often in some Windows platform archive format. Additionally, the files may be re-named during the installation process. This makes it extremely difficult to identify the driver files required.

Then you have the second option. Install the driver locally on a Windows client and investigate which filenames and paths it uses after they are installed. (You need to repeat this procedure for every client platform you want to support. We show it here for the W32X86 platform only, a name used by Microsoft for all Windows NT/2000/XP clients.)

A good method to recognize the driver files is to print the test page from the driver's Properties dialog (General tab). Then look at the list of driver files named on the printout. You'll need to recognize what Windows (and Samba) are calling the Driver File, Data File, Config File, Help File, and (optionally) Dependent Driver Files (this may vary slightly for Windows NT). You need to note all filenames for the next steps.

Another method to quickly test the driver filenames and related paths is provided by the rpcclient utility. Run it with `enumerdrivers` or with the `getdriver` subcommand, each at the 3 info level. In the following example, `TURBO_XP` is the name of the Windows PC (in this case it was a Windows XP Professional laptop). I installed the driver locally to `TURBO_XP` from a Samba server called `KDE-BITSCHO`. We could run an interactive `rpcclient` session; then we would get an `rpcclient />` prompt and would type the subcommands at this prompt. This is left as a good exercise for you. For now we use `rpcclient` with the `-c` parameter to execute a single subcommand line and exit again. This is the method you use if you want to create scripts to automate the procedure for a large number of printers and drivers. Note the different quotation marks used to overcome the different spaces between words:

```
root# rpcclient -U'Danka/xxxxx' -c \
'getdriver "Heidelberg Digmaster 9110 (PS)" 3' TURBO_XP
cmd = getdriver "Heidelberg Digmaster 9110 (PS)" 3
```

```
[Windows NT x86]
Printer Driver Info 3:
Version: [2]
Driver Name: [Heidelberg Digmaster 9110 (PS)]
Architecture: [Windows NT x86]
Driver Path: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\HDNISO1_de.DLL]
Datafile: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.ppd]
Configfile: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\HDNISO1_de.DLL]
Helpfile: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\HDNISO10_de.HLP]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.DLL]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.INI]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.dat]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.cat]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.def]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.hre]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.vnd]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\Hdmd91c1_de.hlp]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\HDNISO1aux.dll]
Dependentfiles: [C:\WINNT\System32\spool\DRIVERS\W32X86\2\HDNISO1_de.NTF]
Monitorname: []
Defaultdatatype: []
```

You may notice that this driver has quite a large number of **Dependent files** (there are worse cases, however). Also, strangely, the **Driver File** is tagged here *Driver Path*. We do not yet have support for the so-called WIN40 architecture installed. This name is used by Microsoft for the Windows 9x/Me platforms. If we want to support those, we need to install the Windows 9x/Me driver files in addition to those for W32X86 (i.e., the Windows NT 2000/XP clients) onto a Windows PC. This PC can also host the Windows 9x/Me drivers, even if it runs on Windows NT, 2000, or XP.

Since the /print$ share is usually accessible through the **Network Neighborhood**, you can also use the UNC notation from Windows Explorer to poke at it. The Windows 9x/Me driver files will end up in subdirectory 0 of the WIN40 directory. The full path to access them is \\WINDOWSHOST\print$\WIN40\0\.
