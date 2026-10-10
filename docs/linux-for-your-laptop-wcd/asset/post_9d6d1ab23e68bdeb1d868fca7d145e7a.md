
## Figure B.8

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_474_0.png)

Select your time zone and location for your system.

Use the Tab and arrow keys to select your zone and location, and then press Enter. You'll then set the notebook's time to local time or GMT. After configuring the time, select the “Make Linux Bootable Directly from Hard Disk” menu item and press Enter.

You'll be asked, as shown in Figure B.9, to create a Master Boot Record if one does not exist.

This step will create a Master Boot Record and install LILO into the MBR so you can boot directly to Linux. Note that you can also modify LILO's configuration file later to accommodate other operating systems or configurations. Select the Yes button and press Enter to continue. You'll then be asked if you want to boot directly to Linux. Answer Yes and press Enter.

Finally, select the “Reboot the System” menu item, as shown in Figure B.10, and press Enter.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_474_1.png)

### Figure B.9

Create a Master Boot Record and install LILO onto your notebook's hard drive in order to boot directly to Linux.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_475_0.png)

### Figure B.10

Reboot the system from the Debian GNU/Linux installer to go to your new Linux system on your notebook.

You’ll be asked to confirm the reboot. Select Yes and press Enter. Don’t forget to remove your Bootable Business Card before the system restarts!

## Final Steps

When the system reboots, you’ll be prompted with:

```text
login:
```

Type in the username `root` and press Enter, like this:

```text
login:  root
```

You’ll then be asked to enter a new password, like this:

```text
New password:
```

Enter a short, perhaps eight-character password (a mix of letters and numbers is best), and press Enter. You’ll be asked to confirm the password by entering it again. Don’t forget this password! You’ll then be asked if you want to create a new user for your system. You can safely skip this step for now, and later, use the `adduser` command to create a new user.

You’ll also be asked if you want to use shadow passwords. This is a good idea, because this system adds a bit more security for Linux. Type a `y` and press Enter. You’ll then be asked if you want to select additional packages for Linux. Since all the software available from the card has been installed, type `n` and press Enter.

The installer will then run the `dselect` command, offering you the chance to configure, install, or remove software packages. Scroll down to the line:

```text
*6. [Q]uit  Quit dselect.
```

Type a `q` or press `Enter` to quit the program. Congratulations! You have finished installing Debian GNU/Linux! The installer will exit, and you'll be presented with your new Linux `login:` prompt. You can then log in as `root` and use your new password. After you log in, you can then shut down the system with:

```bash
# shutdown -h now
```

If you run into problems installing from the card, try browsing to Linuxcare's errata page at:

```text
http://www.linuxcare.com/bootable_cd/errata.html
```

## Downloading and Creating Your Own Copy

If you have a `CDR` or `CDRW` drive, you can download and burn your own copy of the Bootable Business Card. Browse to:

```text
http://www.linuxcare.com
```

Follow the links to the Bootable Business Card and download a copy of the card's `.iso` image, named `lnx-gold.iso`. Next, insert a blank `CDR`, `CDRW`, or even better, blank business card-sized `CDR` in your drive, and use the `cdrecord` command to burn a copy. If you have a PCMCIA SCSI `CDRW` drive, you can use the `cdrecord` command like this:

```bash
# cdrecord -v speed=4 dev=0,1,0 -data lnx-gold.iso
```

Since the burned filesystem is only about 51MB, this process should only take two or three minutes. Keep a couple of copies on hand, make one for a friend, or distribute copies at your local Linux Users Group meeting!

## Index

### Numbers
- 3Com, Palm PDA, 270–277
- 4Front Technology, commercial sound drivers, 12

### A
- AC/DC converters, battery conservation, 374
- ACPI (Advanced Configuration and Power Interface), Linux support, 165
- Add a Printer Entry dialog box, printer creation, 309
- Adventure, 380
- agetty utility, dial-in support, 251
- aliases, 204–206
- Alps Electric Company, Cirque GlidePoint, 35
- AMD K6-2 CPU, 21
- APM (Advanced Power Management)
    - described, 164
    - apm daemon, 169
    - apmsleep utility, 169
    - battery monitoring, 175
    - hibernate (suspend-to-RAM/suspend-to-disk) feature, 164, 171–173
    - information display, 373–374
    - init scripts, 171
    - kcrlaptop utilities, 173–176
    - KDE utilities, 173–176
    - kernel issues, 165
    - Linux process directory (/proc) values, 168
    - network communication troubleshooting, 170–171
    - on_ac_power shell script, 169
    - recompiling the kernel to save memory/power, 166–168
    - save-to-disk problem solving, 171–172
    - shell scripts, 170–171
    - support programs, 169–170
    - suspend (sleep) feature, 164
    - suspend/hibernation time tracking, 172–173
    - tailf command, 169
    - xapm client, 169
    - xbattery client, 170
- apm daemon, APM control, 169
- apmsleep utility, APM control, 169
- append (>>) operator, input/output redirection, 204
- Apple iBook
    - bootable CD-ROM installation, 94
    - BootX boot manager, 136–137
    - BootX Control Panel, 227
    - Drive Setup partitioning command, 114
    - Ethernet adapter, 243
    - internal modem non-support, 250
    - Linux support issues, 10
    - mouse configuration, 38, 226
    - remote Linux client support, 309
    - text-based console jump, 208
    - X11 server application, 25
    - Yellow Dog Linux installation, 127–128
- applications, autostore settings, 369–372
- Apple’s Application for Linux, autostave settings, 370–371
- arcade games
    - fly8 simulator, 384, 386
    - GNOME, 386–387
    - KDE, 386–387
    - system requirements, 384
- archives
    - creating, 194–195
    - extracting, 192–194
- archiving, described, 289
- aspm (AfterStep APM) monitor, APM information display, 374
- ash shell, 204
- AST Ascentia A61+, Linux support, 14
- * (asterisk)
    - at (attention) command, 325, 334
- ATAPI (AT Attachment Packet Interface), CD-ROM drives, 47
- atomic clocks, UTC (Coordinated Universal Time), 350-351
- au (raw audio) sound format, 392
- audio, battery conservation, 364-365
- audio CDs
    - cdp player, 388
    - GNOME cdp/cdplayer, 390
    - GNOME gcdc cd audio CD player, 388
    - gcdc player, 388
    - ksCD player, 388-390
    - MPEG format, 390-396
    - multimedia clients/servers, 391
    - tcd player, 388
    - X11 supported players, 388
    - xplaycd player, 388
- autosave, battery conservation, 369-372
- Aviator 2.4, wireless networking, 248-249
- Aztec Sound Galaxy, sound card support, 28
- backslash (\) special characters, bash shell support, 207
- backup devices, described, 290-291
- backups
    - alternative methods, 294-296
    - BRU (backup and restore utility), 292-294
    - filesystem, 288-289
    - incremental, 289-290
    - Imageo Zip Drive, 291
    - KPIlot client, 275-277
    - Palm PDA, 273-274
    - swapping hard drives, 291
    - testing, 298
- bash (Bourne-Again Shell)
    - aliases, 204, 206
    - backslash (\) special characters, 207
    - default shell, 202
    - editing commands, 205
    - environment variables, 202, 207
    - extended expressions, 204
    - globbing, 204
    - input/output redirection, 202-204
    - job control, 209
    - shell prompt, 207
    - variable types, 203
- BASIC (Beginners All-purpose Symbolic Instruction Code), 5
- battery
    - conservation methods, 65-66, 364-374
    - kemplight gauge, 175
    - life expectancy issues, 65
    - Li-ion (Lithium-ion), 65
    - NiCd (nickel cadmium), 65
    - NiMh (nickel metal-hydride), 65
    - types, 65
- battery conservation
    - AC/DC converters, 374
    - alternative power sources, 374
    - APM information display, 373-374
    - application autosave settings, 369-372
    - audio, 364-365
    - charging/storage considerations, 372-373
    - cron daemon, 365
    - DC power plug, 374
    - external devices, 366
    - external solar panel, 374
    - filesystem updating, 366-367
    - hard drives, 367-369
    - kernel, 365-366
    - maintenance techniques, 372-373
    - PCMCIA, 365
    - ports, 365
    - screen display techniques, 364
    - system logging, 365-366
- bdflush (update) daemon, filesystems, 366-367
- BIOS
    - bootable CD-ROM configuration, 92-93
    - Phoenix Technologies, 92-93
- BIOS passwords, hacker protection, 285-286
- boot disk
    - creating, 83-84, 94-95
    - Red Hat Linux creation, 115
