
```bash
alias char-major-14 off
alias sound off
alias midi off
```

## Chapter 12: Calculators, Music Makers, and Games People Play

and place a comment symbol (#) in front of each, like this:

```bash
#alias char-major-14 off
#alias sound off
#alias midi off
```

Now sound support is no longer disabled for your system. 
Next you have to scroll down and find the section of the file that is preconfigured for your sound card and remove the comment symbol from the lines that begin with any of the following words: alias, post-install, or mpu. Here is an example of a section of the file that is preconfigured for a Soundblaster or clone sound card:

```bash
********************************
# module: sb.0 Soundblaster 16, SB Pro + Clones
#                               Also needed for AWE32/64
#
# Documentation available in
# /usr/src/linux/Documentation/sound/Soundblaster
# and in /usr/src/linux/drivers/sound/sb.c .
# Possible configuration:
# alias char-major-14 sb
# post-install sb /sbin/modprobe "-k" "adlib_card"
# options sb io=0x220 irq=7 dma1=6
# mpu_io=0x330
# options adlib_card io=0x388
********************************
```

What you see in this example is the full name of the module (sb.o), a list of cards that use this module (Soundblaster 16, SB Pro + Clones, also needed for AWE32/64), and a description of where additional documentation can be found. Turning toward the bottom of this section, you see few cryptic-looking lines. These are the lines that contain the information concerning which resources your sound module should use. In this example, we are using the sb module to support a Soundblaster card, we need to uncomment out these lines, like this:

```bash
#
#alias char-major-14 sb
#post-install sb /sbin/modprobe "-k" "adlib_card"
#options sb io=0x220 irq=7 dma1=6
#mpu_io=0x330
#options adlib_card io=0x388
#
```

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use. You can view the currently used interrupts using the command:

![](img/96a9ce6a13d8d15ed05f867f41574278_237_0.png)

```bash
bash-2.03# cat /proc/interrupts
```

which will produce an output similar to this:

| Interrupt | Value | Description |
| :--- | :--- | :--- |
| 0: | 49893 | XT-PIC timer |
| 1: | 206 | XT-PIC keyboard |
| 2: | 0 | XT-PIC cascade |
| 8: | 3 | XT-PIC rtc |
| 12: | | XT-PIC PS/2 Mouse |
| 13: | 1 | XT-PIC fou |
| 14: | 57363 | XT-PIC ide0 |

and you can view the currently used iports by using the command:

```bash
bash-2.03# cat /proc/ioports
```

which will produce an output similar to this:

```
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : DMA page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-017f : ide0
02f8-02ff : serial(auto)
03c0-03df : vga+
03f6-036f : ide0
03f8-03ff : serial(auto)
e800-e807 : ide0
e808-e80f : ide11
```

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

After you have made the necessary modifications to your /etc/conf.modules file, save it. Now you should test the configuration for whether you can load the module manually. You only need to manually load the modules now you are testing to verify that they work. After you have verified this, you do not have to think about them again, as they will be automatically loaded when they are needed by the kernel.

- 1. First, because you have modified the modules configuration file, you need to update the modules dependency file, by issuing the following command:

```bash
bash-2.03# depmod -a
```

You will probably receive a message that there are some unresolved dependencies, and you do not need to be alarmed about them.

- 2. When this file has been updated (the command prompt will appear again), try to load the module for your sound card. In this example, with the Soundblast, the module is sb (note that to load the module, we do not use the full name) and the command looks like this:

```bash
bash-2.03# modprobe sb
```

If the module loaded successfully, you will not see any error messages. You can verify that the module is loaded by showing a list of currently modules:

```bash
bash-2.03# lsmod
```

which will give you an output similar to this:

| Module | Size | Used by |
| :--- | :--- | :--- |
| bttv | 6808 | 0 (autoclean) |
| i2c | 206 | 0 (autoclean) |
| videodev | 3144 | 0 (autoclean) |
| adlib_card | 5552 | 0 (autoclean) |
| sound | 3125 | 0 (autoclean) |
| sb | 2008 | 0 (autoclean) |
| uart401 | 5576 | 0 (autoclean) |
| serial | 4194 | 0 (autoclean) |
| memstat | 1544 | 0 (autoclean) |
| lsmod | 1412 | 0 (autoclean) |
| snd_pcm | 8736 | 0 (autoclean) |
| snd_sb | 4000 | 0 (autoclean) |
| snd_card | 12000 | 0 (autoclean) |

Furthermore, if there are no errors, you can test the sound by issuing the following command:

```bash
bash-2.03# cat /proc/interrupts
```

which will produce an output similar to this:

```
Kernel modules: 2.0.33-x86-2
Loaded on: Mon Jan 1 00:00:00 UTC 2001
CPU: 0
SMP: 0 processor(s) available
processor(s): 0
Interrupts:
00000000 00000000 00000000 00000000  00000000 00000000 00000000 00000000
00000000 00000000 00000000 00000000  00000000 00000000 00000000 00000000
00000000 00000000 00000000 00000000  00000000 00000000 00000000 00000000
00000000 00000000 00000000 00000000  00000000 00000000 00000000 00000000
...
```

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

After you have made the necessary modifications to your /etc/conf.modules file, save it. Now you should test the configuration for whether you can load the module manually. You only need to manually load the modules now you are testing to verify that they work. After you have verified this, you do not have to think about them again, as they will be automatically loaded when they are needed by the kernel.

If there are no errors, you can test the sound by issuing the following command:

```bash
bash-2.03# cat /proc/interrupts
```

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

The configuration settings in the /etc/conf.modules were chosen because they work for most sound cards. There is a possibility that they will not work for your sound card. This could be caused by either a resource conflict (interrupt or ioport) with another device on your computer, or in some cases a jumper setting on your card. In either case, you should check to see which interrupts and iports are currently in use.

After you have made the necessary modifications to your /etc/conf.modules file, save it. Now you should test the configuration for whether you can load the module manually. You only need to manually load the modules now you are testing to verify that they work. After you have verified this, you do not have to think about them again, as they will be automatically loaded when they are needed by the kernel.

- 1. First, because you have modified the modules configuration file, you need to update the modules dependency file, by issuing the following command:

```bash
bash-2.03# depmod -a
```

You will probably receive a message that there are some unresolved dependencies, and you do not need to be alarmed about them. (Wait, the text says "you do not need to be alarmed about them.")

- 2. When this file has been updated (the command prompt will appear again), try to load the module for your sound card. In this example, with the Soundblast, the module is sb (note that to load the module, we do not use the full name) and the command looks like this:

```bash
bash-2.03# modprobe sb
```

If the module loaded successfully, you will not see any error messages. You can verify that the module is loaded by showing a list of currently modules:

```bash
bash-2.03# lsmod
```

which will give you an output similar to this:

| Module | Size | Used by |
| :--- | :--- | :--- |
| bttv | 6808 | 0 (autoclean) |
| i2c | 206 | 0 (autoclean) |
| videodev | 3144 | 0 (autoclean) |
| adlib_card | 5552 | 0 (autoclean) |
| sound | 3125 | 0 (autoclean) |
| sb | 2008 | 0 (autoclean) |
| uart401 | 5576 | 0 (autoclean) |
| serial | 4194 | 0 (autoclean) |
| memstat | 1544 | 0 (autoclean) |
| lsmod | 1412 | 0 (autoclean) |
| snd_pcm | 8736 | 0 (autoclean) |
| snd_sb | 4000 | 0 (autoclean) |
| snd_card | 12000 | 0 (autoclean) |

Furthermore, if there are no errors, you can test the sound by issuing the following command:

```bash
bash-2.03# cat /proc/interrupts
```

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

If there does not appear to be a conflict with another device, you need to either change the jumper settings on your sound card or change the value(s) in /etc/conf.modules so that they correspond with the jumper settings on your card.

## Chapter 12: Calculators, Music Makers, and Games People Play

Information about the artist

| Cycle time display | Play/Pause Forward |
| :--- | :--- |
| Eject Volume control | Stop Loop |

![](img/96a9ce6a13d8d15ed05f867f41574278_240_0.png)

![](img/96a9ce6a13d8d15ed05f867f41574278_240_1.png)

Quit KSCD

| CDDB Dialog | Previous Track |
| :--- | :--- |
| Backward | Configure KSCD |

Shuffle/Unshuffle Playlist

If you've used a CD player, most of these symbols will be familiar. In addition, most elements are labeled in the figure. All you have to do is hold the mouse over one of the buttons, and a description of the button will automatically appear. Here are details on a few of them:

- * To start with a song other than the first one, click the down arrow and select the song that you want to play.
- * The volume control bar in the middle of the screen is normally used to guess— control the volume of sound. You may also have to start mixer to control the volume. (I cover mixer in the next section).
- * To have the songs on the CD player in a random order, click the button with the question mark in it.
- * To skip a song, click the button with the double-headed arrow with a vertical bar pointing to the right.

# mixer: Sounds for the rest of us

As mentioned in the last section, the controls on the CD Player may not affect the volume of the music coming from your sound card. This process is usually controlled by the mixer program. Depending on how the hardware of your computer is, the mixer program may use different inputs for the CD music, so you may have to experiment a little by moving the sets of slider bars until you get the volume of sound you want.

Figure 12-6 shows the mixer window with all its buttons and slider bars. These controls may or may not match the capabilities of your sound card;
