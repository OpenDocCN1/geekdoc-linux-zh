# Chapter 20 ♦ Playing Music and Video 511

+   * **Full-duplex support** — Full-duplex means recording and playback occur at the same time. This is particularly useful for bidirectional Internet communication, such as Voice-Over-IP (VOIP) telephony or simultaneous recording and playback.

+   * **Input/output ports** — Several ports on the board enable you to connect other input/output devices. These ports include:

+   * **Line-In** — Connects an external CD player, cassette deck, synthesizer, MiniDisc, or other device for recording or playback. If you have a television card, you may also patch that card's line-out to your sound card's line-in.

+   * **Microphone** — Connects a microphone for audio recording and communications.

+   * **Line-Out (Speaker Out)** — Connects overpowered speakers, headphones, or a stereo amplifier.

+   * **Joystick/MIDI** — Connects a joystick for a gaming or MIDI device.

+   * **Internal CD Audio** — Connects the sound to your computer's internal CD-ROM board (which isn't externally visible when the board is installed).

Sound drivers in Linux come from many sources. However, as previously mentioned, Advanced Linux Sound Architecture (ALSA) is the sound system that is integrated into the 2.6 kernel. You may find older OSS (Open Sound System) drivers are useful if ALSA does not support your sound card. Commercial support for OSS drivers is available for a small cost from 4Front Technologies (www.opensound.com), which is the company that maintains OSS.

> Caution Before you install a separate sound driver, check if your current distribution has a recent driver. Using the driver with the kernel is always a safe bet if you are not experiencing a specific driver-related issue.

At times, a sound application will help you identify the device from which to access your system. With the introduction of the Udev feature in the 2.6 kernel, some of the device names are different from those used with the 2.4 kernel. The following are audio device nodes that may be of interest to you as you use sound in Linux:

+   * **/dev/audio/dev/audio** — Compatible with Sun workstation audio implementations (audio files with the .au extension). These devices are not recommended for new sound applications. Under Udev, these devices are symbolic links to /dev/sound/audio and /dev/sound/audio1, respectively.

+   * **/dev/cdrom** — Represents your first CD-ROM drive. /dev/cdrom is usually a symbolic link to the device node, such as /dev/hdc, that corresponds to your CD-ROM drive. Additional CD-ROM drives are located at /dev/cdrom1, /dev/cdrom2, and so on.

![](bbox=[0.166, 0.595, 0.193, 0.636])