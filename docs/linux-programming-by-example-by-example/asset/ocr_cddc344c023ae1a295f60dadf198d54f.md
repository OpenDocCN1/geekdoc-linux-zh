# Sounding Off

Sound cards are not monolithic hardware devices. Instead, they are made up of several components. Although there is considerable variety among manufacturers, and even among a single manufacturer's cards, most cards have a MIDI interface, a digital voice device, a mixer device, and a synthesizer. Linux's support for these devices is enabled through entries under the /dev filesystem:

```
`/dev/mixer` , `/dev/dsp` , `/dev/audio` , `/dev/sequencer` , and `/dev/midi` .
```

# Sound Hardware

The MIDI (*Musical Instrument Digital Interface*) interface is a port that connects external devices, particularly synthesizers, but also lighting equipment and other stage props, to a computer. The mixer is a control device that controls input and output volume levels and switches among the available input devices, such as microphones and CDs. Digital voice devices are used to record and play back digitized voice data. They are generally referred to by the *codecs* , or algorithms, used to record and encode the sample.

Synthesizer devices are used to play music and generate a wide variety of sounds and sound effects. In general, synthesizers fall into two categories. One group is based on the Yamaha OPL2 and OPL3 chips, which are common on most sound cards. The second group are wave table synthesizers—they produce sound from recorded instrument samples stored in chips on the card. Of the two types, wave table synthesizers produce far richer, more realistic sounds.

# Sound Devices

Linux's /dev filesystem contains device files that correspond roughly one-to-one with the sound hardware available. All the devices end with a number *N* , usually 0, 1, or 2, to which the device name is symbolically linked. For example, on my system, `/dev/mixer` is a symbolic link to `/dev/mixer0`. The rest of this chapter refers to the symbolic links unless it is necessary to refer to specific device files.

`/dev/mixer` is the interface to the mixer hardware, whereas `/dev/dsp` and `/dev/audio` are the primary interfaces to the digital voice devices. The only difference between the two is that `/dev/audio` uses µLaw (µ is the Greek letter *mu* , pronounced "mew") encoding by default, which represents 12or 16-bit samples in 8 bits, whereas `/dev/dsp` uses 8-bit unsigned linear encoding. `/dev/sequencer` is the device used for electronic music and the sounds emitted by games. It is the interface to the synthesizer chips on the sound card and also can be used to access external MIDI devices and the wave table, `/dev/midi` , finally, is used for low-level MIDI output.