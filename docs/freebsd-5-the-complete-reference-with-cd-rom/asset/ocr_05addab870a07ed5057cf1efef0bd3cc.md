If you can’t find support for your sound card, you may want to check with 4Front Technologies (http://www.opensound.com). This company provides commercial sound drivers for FreeBSD and other Unix-like OSs. You can download a demo version, and if it works, pay the registration fee, which is probably less than a new sound card would cost.

# Starting Sound Support

Soon after you boot your computer, type dmesg | less to examine the kernel boot messages. If your kernel was compiled with support for your sound card, you should see one or more messages identifying the card, such as the following for a Gravis UltraSound (GUS) PnP board:

```
gusc0: <Gravis UltraSound Plug & Play PCM> at port 0x32c-0x32f, 0x320-0x327,0x220-0x22f irq 12 drq 7,5 on isa0
pcm0: <GUS CS4231> on gusc0
gusc1: <Gravis UltraSound Plug & Play OPL> at port 0x388-0x389, irq 5 drq 1 on isa0
gusc2: <Gravis UltraSound Plug & Play MIDI> at port 0x330-0x331, on isa0
```

The dmesg command displays the kernel message buffer. This buffer is limited in size, and it’s constantly fed new data. Thus, after your computer has been up for some time (a few days or even just a few hours), dmesg won’t display information that’s useful for identifying your hardware.

These messages may include more than one card driver (gusc0, gusc1, and gusc2 in the preceding example) to handle different parts of the card’s hardware. One particularly important driver is the pcm0 driver, which handles pulse code modulation (PCM) encoding and decoding. Most digital audio formats use PCM in one way or another.

If you see these messages, your kernel has identified your sound card. You may or may not need to load a sound driver kernel module. If you need to load a driver module, you can do so with the kldload command:

```
# kldload snd_gusc.ko
```

This command is described in Chapter 12. In brief, the preceding example command loads the snd_gusc.ko driver, which supports the GUS PnP and various related