
## Mouse Configuration

results. Virtually all serial mice will work using the Microsoft or generic serial mouse driver. For the correct mouse to work properly X Windows must be set to use the correct mouse port. If you are using a bus or ps/2 mouse port there should be no problem, and the configuration program should default to the correctly select the correct one. This is the normal configuration between Linux and MS/DOS or Windows port identifications.

- MS/DOS: Port 1 (COM1) / Linux: /dev/tty0
- MS/DOS: Port 2 (COM2) / Linux: /dev/tty1

The names used for the ports are not fully standardised, and the serial ports could be called something like /dev/cua0 and /dev/cua1. If necessary, take a little time to find the correct port setting.

There are some options such as mouse sensitivity that can be set to suit particular preferences. Other options such as the baud rate should not be altered unless there is a good reason to do so. As explained previously, in theory Linux requires a three-button mouse, but you can use a two-button mouse plus a three-button emulation mode. In practice the third button mouse seems to be of little importance these days, but if you are using a two-button mouse it might be well to activate the three-button emulation.

## Keyboard

The next screen of the configuration program asks for the keyboard (Figure 1.7). The keyboard should be working reasonably well already, and it is not normally essential to alter any settings. It is probably best to leave everything else unaltered. You can always return to the configuration later if some aspect of keyboard operation is incorrect or you wish to "fine tune" the key functions.

## Video card

For X Windows to work with your video card it must have a suitable server. A server is roughly equivalent to a driver program in Windows, but it is often a program provided by the video card manufacturer. Linux support from hardware manufacturers is still a bit "thin on the ground", and the X server will normally be one of those required servers included to be selected, or you may have already installed it. If the required installation process, or if they would normally be installed. This will only operate at 640 by 480 pixel resolution with 16 colours, but it should work with any normal video card.

Video servers are in use. You need a server that any likely looking servers can be installed so that various servers are left open, if necessary, you can work properly. If SVGAsvga servers are available at higher resolution than the VGA type, and is working. Then trying to utilise the full capabilities of your video card. It is unlikely to utilise the full capabilities of your video card.

The video configuration page (Figure 1.8) enables various parameters to be set by the user, but provide you have selected a suitable server it should not be necessary to do so. The program can use probing to find out what it needs to do so. It is only necessary to set things manually if the probing fails for some reason. Apparently the probing can sometimes cause a malfunction, and could result in the computer hanging up, but had been infrequent such problems except when an unreliable server had not been selected. If a list of compatible cards for which you have provides, and if your video card is included in the list it clearly will try to select one that you will virtually guarantees correct operation of the video card with X Windows.

## Monitor

The next screen covers monitor selection (Figure 1.9). It is unlikely that your monitor will be included in the list of models supported, although some recent Linux distributions do have a large number to choose from. If there is no specific support for your monitor, it does not really matter. By selecting the parameters manually for any monitor that you can be accommodated as a structure manually for the monitor should Windows be compatible, and will get the monitor X Windows running with a maximum resolution of 1024 x 768 if your monitor support that. Or at least a 15-inch monitor is needed for operation long periods. At least a good 15-inch monitor is needed for operation

![](img/147f057d2f063d8c60ee616870537a94_22_0.png)

Fig. 1.9 The monitor setup screen is used to set scan frequencies, etc.

At 1024 by 768 without eyestrain. It is probably better to settle for 800 by 600 pixel operation if the size of the screen is less than 15 inches or the monitor does not support high scan rates at high resolutions.

In the initial setup if you are telling the X server the capabilities of the monitor. To do this you will need to find the "Model Setup" tab at the top of the monitor configuration screen. This brings up a near screen (Figure 1.9) that makes it easy to select the desired resolution. And the reduction can be beyond the maximum resolution selected. The monitor then display as much of the larger resolution scroll when the cursor is placed in use, and my preference is to keep the screen resolution no higher than the true resolution of the monitor.

The numbers near the bottom of the screen enable the colour depth (the size in bytes of a 16-bit word for a 16-bit display) and the number of colours. In this table shows chosen in terms of the number of bits used per pixel.

## Color Depth and Resolution

![](img/147f057d2f063d8c60ee616870537a94_23_0.png)

Fig. 1.10 The screen used to select the required screen modes

the correlation between bits per pixel (bpp) and the actual number of colours available.

| Bits per pixel | Colours |
| :--- | :--- |
| 8 | 256 |
| 16 | 65536 |
| 24 | 16779850 |
| 32 | Approx. 4.3 billion |

The maximum number of colours available for a given (true) screen resolution depends on the amount of RAM fitted to the video card. Unless your computer is rather slow it makes sense to choose a fairly high colour depth, but for most purposes there is no point in going beyond 24-bit operation.

## Other

![](img/147f057d2f063d8c60ee616870537a94_23_1.png)

Fig. 1.11 The "Other" screen configures minor functions

The final tab at the top of the main configuration page brings up a screen (Figure 1.11) that enables miscellaneous factors to be controlled. These are concerned with switching screen resolutions on the fly, and with default X Windows. Some of the options are irrelevant unless the computer is part of a network. By default the system will be set to use Control-Alt-Backspace as an easy way back to normal Linux operation if you are greeted with a blank or scrambled screen on entering X Windows.

When everything has been set up your X86Config operate then "Done" tab to exit the X86Config program. The program will then "adjust" everything to suit your video card and monitor settings after which it will try to run the X server. If all is well you can exit the configuration program completely. You must rerun the X86Config program if there is a major problem, and the screen is far from correct. Minor problems with a display, such as too little width or height, can usually be corrected using the monitor's controls. If this fails to give satisfactory results you can use the Xrdump program to make fine adjustments to the scan rates and other aspects of the video timing. I suppose that using Xrdump is very slightly risky, so it is best to only use it if you really need to.

## Testing, testing

Eventually you should end up with everything installed and Linux under way. Before you can use Linux it is necessary to log in, and this requires a user name and the corresponding password. If you set up a user account during the installation process enter the appropriate name and press Return. Then when prompted for the password, enter the appropriate string of characters and press Return. You should then be in to Linux and ready to start using the new operating system. If you did not set up a user account during installation it is still possible to go into Linux. You must log in as the system supervisor. For the user name enter “root” and then press Return. Then type in the password and press Return again. Linux will then be up and running, awaiting your first commands.

At this point it is a good idea to close down Linux, switch off the computer, “cold start” it again to do so, go through the installation process again, making sure that the appropriate disc partition is bootable, etc. It is not a good idea to shut down Linux by simply switching off the computer. As with Windows 95 and 98, this leaves various temporary files on the hard disc drive, and things left somewhat “up in the air”. The correct way to close down Linux is to use the shutdown command, and to only switch off the computer once the string of on-screen messages finish. The first message should say something like “system halted”.

The shutdown command has various switches and controls that can be used to govern the exact way in which it functions. Bear in mind here that Linux is designed for use with a network that will probably be switched off would normally be issued together with a shutdown time and a message. All this is of no consequence if Linux is used on a workstation, warning of the shutdown time would then be sent to each terminal. When you simply want to close down the system immediately at the end of each session. For an immediate shutdown use this command:

```
shutdown -h now
```

Linux is usually case sensitive, and the command examples given in this book will only work if they are copied precisely, but there are some exceptions. The text will be in lower case letters, but if in some cases everything had been written in lowercase then the system successfully the next step is to check that X windows is functioning correctly. By default Linux does not usually run X windows automatically at start-up. But some systems do now it so. to start X Windows use this command:

```
startx
```

After a few seconds of frantic hard disc activity a graphical user interface should appear on the screen, and the screen's exact appearance will depend on the distribution and version of Linux in use. Figure 1.12 and 1.13 respectively show the screens obtained from Red Hat Linux 5.2 and Caldera Open Linux 1.3. It is worthwhile experimenting with the general way in which systems and the mouse. However, if an alternative desktop environment such as KDE is included in the installation, I would suggest extending X Windows before trying such a thing in the normal start-up. If KDE or an alternative such as Gnome is available during installation. I would strongly recommend including it in the installation. Most Linux

![](img/147f057d2f063d8c60ee616870537a94_24_0.png)

Fig. 1.12 The opening X Windows screen in Red Hat Linux 5.2
