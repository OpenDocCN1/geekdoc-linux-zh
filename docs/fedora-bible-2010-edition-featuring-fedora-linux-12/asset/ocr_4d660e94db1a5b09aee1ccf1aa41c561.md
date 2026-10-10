+   * **Line-In (blue)** — Connects an external CD player, cassette deck, synthesizer, MiniDisc, or other device for recording or playback. If you have a television card, you might also patch that card’s line out to your sound card’s line in.
+   * **Microphone (red)** — Connects a microphone for audio recording or communications.
+   * **Headphone/Line-Out/Speaker Out (green)** — Connects speakers, headphones, or a stereo amplifier. (On sound cards I’ve tested, this is marked as Headphone in mixer utilities.)
+   * **Joystick/MIDI (15-pin connector)** — Connects a joystick for gaming or MIDI devices. (Some sound cards no longer have these ports because they are now available from most motherboards.)
+   * **Digital out (orange)** — A digital out connector can be used to connect a digital audio tape (DAT) device or CD recordable (CD-R) device.
+   * **Rear out (black)** — Can be used to deliver audio output to powered speakers or an external amplifier.
+   * **Internal CD Audio** — This internal port connects the sound card to your computer’s internal CD-ROM drive (typically, this port isn’t exposed when the board is installed, which makes it more difficult to directly connect these devices).

For some sound applications, you need to identify the device files used to communicate with the sound card and other sound hardware. While your system may not have all these available, the devices that the audio programs use to access audio hardware in Fedora include:

+   * **/dev/audio, /dev/audio1** — Devices that are compatible with Sun workstation audio implementations (audio files with the `.au` extension). This requires the snd-pcm-oss kernel module.
+   * **/dev/cdrom** — Device representing your first CD-ROM drive. (Additional CD-ROM drives are located at `/dev/cdrom1, /dev/cdrom2`, and so on.)
+   * **/dev/dsp, /dev/dsp1, /dev/adsp** — Digital sampling devices, which many audio applications identify to access your sound card. This requires the snd-pcm-oss kernel module.
+   * **/dev/mixer, /dev/mixer1** — Sound-mixing devices.
+   * **/dev/sequencer** — Device that provides a low-level interface to MIDI, FM, and GUS.
+   * **/dev/midi0, /dev/midi** — Device that provides raw access to midi ports.
+   * **/dev/snd/*** — ALSA native sound device interfaces.

> **TIP:** Nodes in the `/dev` directory, such as `/dev/audio`, aren’t just regular files. They represent access points to the physical devices (hard disks, COM ports, and so on) that are connected to your system, or to pseudo-devices (such as Terminal windows). For example, to find out the device of your current Terminal window, type **tty**. Then send some data to that device. For example, if your device name is `/dev/pts/0`, type: