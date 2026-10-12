```
# There should be no spaces at the start of a line
# or around the '=' sign
CARDTYPE=SB16
```

# Note

If you find that you cannot get Red Hat Linux to work with your sound card, take heart! First, try to find someone who has the same sound card and has met with success. Linux laptop users should definitely browse to the Linux Laptop pages at http://www.cs.utexas.edu/users/akharrel/linux-laptop/. You can also turn to the free Advanced Linux Sound Architecture sound drivers available from the ALSA project at http://www.alsa-project.org. If the ALSA drivers do not work, you can then browse to 4Front Technologies' Open Sound System at http://www.opensound.com and download a demo set of commercial drivers. The OSS drivers are relatively inexpensive, and the system currently supports more than 350 different sound cards, so you should be in luck. Users with new, cutting-edge hardware are most at risk for lack of sound support.

The corresponding entry in /etc/modules.conf looks like this:

```
alias sound-slot-0 sb
options sound dmasb=1
alias midi opl3
options opl3 io=0x0x388
options sb io=0x220 irq=5 dma=0 dma16=5 mpu_io=0x0x330
```

These examples are for a SoundBlaster 16-compatible card, and the kernel module options create the settings for proper initialization of the card when Linux boots. After configuring your sound card and ensuring that it works with Linux, you should then launch an audio mixer to choose proper settings for different audio devices offered by your sound system. This may include volume, bass, treble, synthesizer, MIDI, line in, line out, microphone, and audio CD settings. Red Hat Linux comes with a number of audio mixers:

+   * aumix—A console audio mixer
+   * gmix—A GNOME X11 mixer
+   * kmix—A KDE mixer client
+   * xmixer—An X11 mixer client

All mixers provide the same functions, but you'll most likely use the one available in your desktop's panel. If you do not use X11, the aumix command can be used from the console. Interestingly, if you've properly configured the gpm or mouse daemon so that you can use your mouse for copying and pasting under the console, you can use your mouse to control the aumix slider controls (otherwise you'll need to use the cursor keys).