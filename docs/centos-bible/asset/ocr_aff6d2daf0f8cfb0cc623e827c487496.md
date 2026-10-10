# Configuring a Sound Card

Configuring a sound card in Linux consists primarily of having the right modules load (which usually happens automatically at boot time) and then using the sound utilities you choose (such as the PulseAudio Volume Control, a\samixer, or aumix) to adjust the settings for the sound card. Today's sound cards often have more than one old Mic-In, Line-In, Speaker-out, and Joy-stick ports. So when you go to adjust your audio levels, there are more items you need to learn about.

# Sound Card Features

Sound cards can pack an amazing number of features these days. Most PCs these days come with built-in sound support. Here are some of the features you should look for if you want to purchase a sound card separately.

+   * **Sound Recording and Playback Quality** — When you record and play back audio, quality and file size are determined, in part, by word length (the number of bits that are used to hold a numerical value) and sample rates. Typical word lengths include 8-bit (less popular), 16-bit, or 24-bit digital sizes. To convert the sound, the board samples the sound in waves from 8 kHz to 96 kHz, or 8,000 to 96,000 times per second (of course, the higher the sampling, the better the sound and the larger the output).
+   * **Full-Duplex Support** — This allows for recording and playback to occur at the same time. This is particularly useful for bidirectional Internet communication or simultaneous recording and playback.
+   * **PCI or USB Interface** — Most people purchase a PCI sound card to put in the case of their desktop system, when sound ports on the computer's motherboard are not sufficient. However, if you are using a PC (such as a Shuttle) with limited slots or a laptop, there are USB sound cards that are supported in Linux.

Several different ports on the board enable you to connect input/output devices. These ports can include some or all of the following:

+   * **Line-In (blue)** — Connects an external CD player, cassette deck, synthesizer, MiniDisc, or other device for recording or playback. If you have a television card, you might also patch that card's line out to your sound card's line in.
+   * **Microphone (red)** — Connects a microphone for audio recording or communications.
+   * **Headphone/Line-Out/Speaker Out (green)** — Connects speakers, headphones, or a stereo amplifier. (On some sound cards I've tested, this is marked as Headphone in mixer utilities.)
+   * **Joystick/MIDI (15-pin connector)** — Connects a joystick for gaming or MIDI devices. (Some sound cards no longer have these ports because they are now available from most motherboards.)
+   * **Digital Out (orange)** — A digital out connector can be used to connect a digital audio tape (DAT) device or CD recordable (CD-R) device.