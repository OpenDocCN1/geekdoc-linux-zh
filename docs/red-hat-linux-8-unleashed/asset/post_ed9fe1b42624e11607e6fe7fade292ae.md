
# Using Wine to Run Windows Programs in Red Hat Linux

The following are default values that will work on almost every Intel-compatible system ever made. Unless you have a unique circumstance, they need not be changed.

```
[serialports]
Com1 = /dev/ttyS0
Com2 = /dev/ttyS1
Com3 = /dev/ttyS2
Com4 = /dev/modem
```

```
[parallelports]
Lpt1 = /dev/lp0
```

```
[spooler]
;LPT1: = |lpr
;LPT2: = |gs -sDEVICE=bj200 -sOutputFile=/tmp/fred -q -
;LPT3: = /dev/lp3
```

```
[ports]
;read = 0x779,0x379,0x280-0x2a0
;write = 0x779,0x379,0x280-0x2a0
```

```
[spy]
Exclude = WM_SIZE;WM_TIMER;
```

```
[registry]
These are all booleans. Y/y/T/1 are true, N/n/F/0 are false.
;Defaults are read all, write to Home
;Global registries (stored in /etc)
;LoadGlobalRegistryFiles = "Y"
;Home registries (stored in -user/.wine/)
;LoadHomeRegistryFiles = "Y"
;Load Windows registries from the Windows directory
;LoadWindowsRegistryFiles = "Y"
;TRY to write all changes to home registries
;WriteToHomeRegistryFiles = "Y"
;Registry periodic save timeout in seconds
;PeriodicSave = "600"
;Save only modified keys
;SaveOnlyUpdatedKeys = "Y"
```

```
[Tweak.Layout]
;; supported styles = 'Win31(default), 'Win95', 'Win98'
;WineLook = "Win98"
```

# CHAPTER 27 Using Emulators and Other Cross-Platform Tools in Red Hat Linux

```
[Console]
;Drivers = "tty"
;XtermProg = "nxterm"
;InitialRows = "25"
;InitialColumns = "80"
;TerminalType = "nxterm"
```

```
[Clipboard]
ClearAllSelections = "0"
PersistentsSelection = "1"
```

```
# </wineconf>
```

> TIP
Wine, by default, emulates a Windows 98 system. If you want it to emulate a Windows 3.1, 95, or NT system, if a particular Windows application requires a specific system, add a section like at the end of the configuration file:
[Version]
"Windows" = "winNT"

Remember to always make a backup of the default configuration file before making any changes.

# Launching Win32 Applications

Launching a Windows application in Wine would be easy except for two things that give people trouble: paths and spaces in names.

If the Wine script found in /etc/init.d is executed at boot by default, Win32 binaries are associated with Wine in the kernel. Unless binaries are located in C:\Windows, you need to be in their directory to run them from the command line (or add them to your PATH if you run them frequently). Otherwise, you must provide the full path to the binary. The TAB completion of the BASH shell makes this easier and handles spaces in pathnames well.

After you have installed and configured Wine, use it to run Windows applications like this:

```
$ wine "C:\Program Files\Internet Explorer\EXPLORE.EXE"
```

Be careful to use quotes, spaces, and capitalization in the full pathname exactly as shown here. You can also create a MIME-type association for .exe files in KDE and GNOME and associate those files with the Wine binary. Then just click on them from Konrad or Nautilus.

# Using Wine to Run Windows Programs in Red Hat Linux

> NOTE
It is unlikely that Windows viruses you open in a Linux client will "infect" your system if you have Wine installed. The self-executing viruses are usually some form of macro written in Visual Basic—they won't run in Wine. If a .exe file containing malicious code were run in Windows, the worst it could do is affect your system. Remove and reinstall Wine if you suspect a problem; your configuration files will not get "infected" because they are just text files. It never hurts to be careful with attachments at a matter of course.

# Gaming with Wine

Many older DOS and Windows games run well on the standard version of Wine, but the Project has not emphasized support for Microsoft's Direct3D. A commercial company, TransGaming, has done work on supporting Direct3D in Wine. TransGaming has incorporated the installer to make installing Windows applications easier, and they have licensed and included copy-protection code to produce a Windows variant called WineX.

> CAUTION
The default kernel installed with Red Hat 8 includes patches added by Red Hat that degrade the performance of the games. TransGaming suggests that you install a "vanilla" kernel if you play these games. Installing a "vanilla" kernel from source code is covered in Chapter 24, "Kernel and Module Management." TransGaming expects these problems to be solved in futures of Wine.

Wine installs and runs many popular Windows games, including Max Payne, Warcraft III, Diablo 2, and others in Red Hat. A full list of supported games can be found at http://www.transgaming.com/searchgame.php. Wine is not free, and is far from perfect. Development continues and is supported by a variant of Street Performer where users contribute in support of development, like giving money to the street performer. Concurrent Versioning System is a method of organizing and managing source code under TransGaming license. That source code does not contain licensed copy-protection, although many games will install in order to run.

![](img/446debe023486a07fde575245cfa3ff_227.png)

**27.3** Although a native Linux port of Castle Wolfenstein exists, the win version loads and runs perfectly using Wine.

TransGaming has changed the license under which it develops its version of Wine. The company did so to prevent commercial competitors from using its enhancements until TransGaming has achieved its sales and subscription goals. The move is controversial and using its code is a personal choice. Please read the EULA (End User Agreement) carefully.

# Crossover and Wine 1.0

Crossover, a software development company specializing in Wine development, has used Wine for several Open Source and commercial projects and has made many contribution to Wine development. Their initial project is an attempt to produce a 1.0 release of Wine. This particular Wine variant is older than the one currently provided by Red Hat, but contains code not included in the standard version of Wine provided by Red Hat. While still not finished, this Wine version sports a useful, no-cost, proprietary configuration tool. It is possible to download Crossover' version of Wine, install it to get the GUI configuration tool (see Figure 27.4), and then update to the Red Hat by reinstalling the Red Hat after you have installed the Crossover' version.

CAUTION
Crossover' configuration tool, although free of cost, is proprietary. Some might have an objection to its use on their computers. Read the licensing terms before installing.

Active development of Crossover Wine has been neglected for the two other Wine variants that in both cases, Crossover uses Wine as a base to which it adds proprietary code, a better GUI interface, and good documentation to offer enhanced functionality and usability to the Linux user. All enhancements to the Wine codebase are returned to the community; proprietary code is not.

![](img/446debe023486a07fde575245cfa3ff_928.png)

**27.4** The GUI configuration tool from Crossover Wine is well worth the effort to install, but needs updating to address Sound configuration.

Crossover’s first commercial product is the Crossover Plugin, which allows Web browser plug-ins for Microsoft Explorer to be in the current Linux versions of the Netscape, Opera, Mozilla, Galeon, Skipstone, and Konrad Web browsers. Crossover supports the major plug-ins, including Shockwave, Quicktime, and Windows Media Player, as well as browser-based viewers for Word, Excel, and PowerPoint. The program provides a GUI installer and automatic download links to the major plug-ins themselves. The documentation is very good, and the Web site contains a good FAQ. The installation and configuration display is shown in Figure 27.5.

Crossover Office, another commercial product from Crossover, provides support for installing and running Microsoft Office (97 through 2000, see Figure 27.6), Microsoft Internet Explorer 5.5, Lotus Notes, Microsoft Visio, Microsoft Outlook, and Intuit Quicker. It also provides a GUI installer for the applications and will download and install the freely available Microsoft fonts. Crossover Office can also be configured to be used as a standard Wine to run other Win32 binaries (it’s the only Wine you have installed) or it can coexist with other versions of Wine installed on your system—the Wine supplied with Red Hat and WineX.
