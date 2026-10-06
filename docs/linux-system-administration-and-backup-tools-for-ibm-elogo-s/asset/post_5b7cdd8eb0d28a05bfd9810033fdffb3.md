
# Configuration Options

Select the item that you would like to configure from the list below:
* Configure Keyboard
* Configure Mouse
* Configure Video Card
* Configure Monitor
* Configure Video Mouse
* Configure Sound
* Test X Configuration
* Change Login Method
* Write Configuration

| Configure | Continue w/o Menu | Done | Cancel |
|---|---|---|---|

Figure 122. Configuration Options window

It is advisable to start out by selecting Show Configuration to see how the system is configured.

# Current Configuration

| Console Keyboard | us |
|---|---|
| XKB Model/Layout | pc101 (us) |
| Mouse | Generic PS/2 Mouse on /dev/psaux |
| Probed Card | N/A (N/A) |
| Configured Card | Generic VGA compatible (XFB6_VGA16) |
| Video RAM | 512 kb |
| Monitor ID | unconfigured unconfigured |
| Monitor Freqs | HSync 0.0 kHz VSync 0.0 |

![](img/4e6a76e57a4105be55d8a1cc0750b023_135_0.png)

Figure 123. Current configuration window

Above you see our incomplete configuration left from the install. To properly configure X, follow the following steps:

- 1. First we must confirm that the correct X server has been installed.
  Highlight Configure Video Card (Figure 123) and press Enter. You will see a window similar to Figure 124.

![](img/4e6a76e57a4105be55d8a1cc0750b023_136_0.png)

Figure 124. Probe Video Card window

- 2. Select **Yes** in Figure 124.

![](img/4e6a76e57a4105be55d8a1cc0750b023_136_1.png)

Figure 125. Select Video Card window

- 3. In Figure 125, note that the card has not been detected but we know that the Netfinity 5000 we are using has a S3 TrioV2/GX video card installed. Therefore, we select it and press **OK**. You will see a window similar to Figure 126.

![](img/4e6a76e57a4105be55d8a1cc0750b023_137_0.png)

Figure 126. Error window

- Here the correct X server was not installed, and turbboxcfg complains about this fact. The error above indicates that the X server XF86_S3 has not been installed, so we now install it by mounting the TurboLinux 6 CD and installing the file. The commands to do this are:

```
mount /mnt/cdrom
cd /mnt/cdrom/TurboLinux/RPM
rpm -Uhv XFree86-S3-3.3.6-6.1386.rpm
```

After the XFree86-S3 package is installed, you will see a window similar to Figure 127.

![](img/4e6a76e57a4105be55d8a1cc0750b023_137_1.png)

Figure 127. Video Memory window

- Turboxcfg finds the server and proceeds to ask for the amount of video RAM on the card.

- 6. Next you should select Configure Keyboard. The questions in this section ask which keymap code to use, how many keys are on your keyboard, and the country code to use.

- 7. Configure Mouse asks for you to specify the type of mouse and number of buttons.

- 8. Configure Monitor requires you to choose the manufacturer and model of your monitor.

- 9. Configure Video Modes allows you to set the maximum video resolution and color depth.

- 10. Configure Font Path allows you to use either 75dpi or 100dpi points.

- 11. Test X Configuration allows you to see if your configuration works properly.

- 12. If the X configuration works, you can choose Change Login Method to change to graphics, or choose to leave in text mode.

- 13. After everything has completed successfully, you can select Write Configuration, which saves the information to the file /etc/X11/XF86Config.

## 5.1.2 Installing the VESA frame buffer server

If you have problems configuring the X server, or want to create an image or process that runs on any video card, you should install the VESA frame buffer driver. The frame buffer is given to limited functionality to any VESA compliant video card. The following is a set of instructions needed to configure the frame buffer.

- 1. With the system started in command mode, log in as "root".

- 2. Mount the TurboLinux Companion CD and install the frame buffer package with the following commands:

```
mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom/TurboContrib/RPMS
rpm -ivh XFree86-FBDev-3.3.6-i386.rpm
```

- 3. Save the current symbolic link and create a new symbolic link by running the following:

```
mv /etc/X11/X /etc/X11/X.old
ln -s /usr/X11/bin/XF86_FBDev /etc/X11/X
```

- 4. Open /etc/lilo.conf to add a new entry for the frame buffer.

```
vi /etc/lilo.conf
```

The file looked something like:

```
boot=/dev/sda
map=/boot
prompt=
timeout=50
default=/boot/vmlin
image=/boot/vmlin
label=/dev/sda
initrd=/boot/initrd
read-only
```

- 5. Make a copy of the existing entry. Change the label on linux-fb or something else to you. In the new entry, the line vga=xxx (where "xxx" is in Table 6) after the image line and change the label so that it is unique.

# Table 6. Screen resolution

| Screen Resolution | Screen Resolution | Screen Resolution | Screen Resolution | Bits/Pixel |
|---|---|---|---|---|
| 640x480 | 800x600 | 1024x768 | 1280x1024 | |
| 800x600 | 1024x768 | 1280x1024 | | 256 |
| 1024x768 | 1280x1024 | | | 32K |
| 1280x1024 | | | | 64K |
| | | | | 16M |

The following is an entry in /etc/lilo.conf with the frame buffer installed at /boot/:

```
image=/boot/vmlin
label=linux-fb
root=/dev/sda
vga=800
initrd=/boot/initrd
read-only
```

- 6. Do not change the default image until you have verified that the new image works. Update the boot record and LILO boot loader by running the command:

```
lilo
```

- 7. Edit /etc/X11/XF86Config to create a new section entry for the frame buffer. Copy the following example of a screen entry and make the necessary changes. The corresponding depth value defined by zzz is from the table above. xxxx and yyyy depend on strings in XF86Config. Replace xxxx with the string following the Device section. Replace yyyy with the string following the Monitor section:

```
Section Screen
Driver=fdev
Device xxxx
Monitor yyyy
Subsection Display
Depth=zzz
Modes default
EndSubsection
EndSection
```

- 8. Reboot the system and remove all the media.
- 9. You may receive a warning after you restart the server; this warning is normal. Selection is expected.
- 10. At the LILO boot prompt, press the Tab key for kernel options. You should have two options: linux and linux-fb. Select linux-fb.
- 11. After the system has started in command mode, you can start the X server by issuing command:

```bash
startx
```

- 12. If this works, you may want to edit /etc/lilo.conf again and make linux-fb the default. However, that is not necessary.

## 5.2 Turbonetcfg

Turbonetcfg is TurboLinux's multi-purpose network configuration tool. With it you can configure everything from the IP address of your NIC to the Apache Web server. To invoke this tool, type turbonetcfg. Although it is a text-mode utility, we recommend that you run it from inside X, since some of the windows require a larger console than is normally available without X.

![](img/4e6a76e57a4105be55d8a1cc0750b023_141_0.png)

Figure 128 is the main window of turbonetcfg. Here are brief explanations of all the options on this window.

- **Display Configuration.** Displays the current configuration of host and domain name, as well as the NICs in the machine and default router.
- **Basic Settings.** Allows you to set the host and domain name, and add search domains, secondary nameservers, and the default gateway and gateway device.
- **Hosts Table.** Used if you do not have a nameserver, or would like to specify the IP address of frequently used machines. It should also have 127.0.0.1 as localhost. It is a good idea to add your IP and host name to this table, as it allows GNOME to start much quicker.
- **Network Interfaces.** The network interfaces dialogue allows you to manage all the NICs in the server, including the ability to add, remove, or change interfaces without rebooting.
- **Network Diagnostics.** This is a very interesting feature of turbonetcfg. Selecting this option will cause TurboLinux to run a series of network tests. Note that if the nameserver cannot be contacted during the "Testing Name Lookup (getbyhostname)" query, the query stays on the window for several minutes if it has. However, it will eventually time out and show you a window with the results similar to Figure 129.
