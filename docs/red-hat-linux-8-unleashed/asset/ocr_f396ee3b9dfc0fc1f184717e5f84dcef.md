Do the same for the ALSA software libraries, and then build and install the ALSA utility software. You can then use the insmod command to load supporting kernel modules to initialize and configure sound:

```
# modprobe snd-via82xx
# modprobe snd-pcm-oss
# modprobe snd-mixer-oss
# modprobe snd-seq-oss
```

This will initialize your soundcard (which ALSA numbers 0). To sound you, you should then use ALSA's alsamixer command to unmute your soundcard's channels and save the settings using the alsactl command:

```
# alsactl store 0
```

The state of your soundcard will be saved in the file /etc/sound.state. These settings, as channel volumes, can be retrieved later by using the restore option instead of store.

> NOTE
You'll find complete documentation about the Linux kernel's sound support in various text files under the /usr/src/linux-2.4/Documentation/sound directory if you install the source code to Linux.

Configuration problems can arise, especially if your soundcard's manufacturer won't or release specifications to help open source developers create working drivers. If your sound card is not recognized, or is recognized but won't work, and using ALSA fails, you can turn to commercial drivers from 4Front Technologies. These relatively inexpensive drivers support more than 350 sound systems and are installed, configured, and controlled using shell scripts. Browse to http://www.opensound.com for more information.

# Using Loadable Kernel Modules to Start Sound Service

Although support for sound cards can be compiled directly in the Linux kernel, loadable kernel modules are most used to start sound service. These modules are enabled by entries in /etc/modules.conf—similar to this example, which enables a SoundBlaster-compatible chipset:

```
alias sound-slot-0 sb
options sound dmabuf=1
alias synth op13
options opl3 io=0x388
options sb io=0x220 irq=5 dma=0 mpu_io=0x530
```