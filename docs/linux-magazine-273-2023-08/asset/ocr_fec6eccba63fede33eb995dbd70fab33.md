# Hardware

The step from a simple USB microphone to a mixer is affordable nowadays. I used the Mackie ProFX10v3 [2] mixer for this article, priced at around EUR250 (Figure 1). The device is the result of more than three decades of experience in building analog mixers. In addition to all the qualities you can expect from it, there is also a built-in USB interface that goes about its tasks without treading on anybody's toes.

Thanks to the JACK audio server built into most Linux systems, generic USB devices of this type now work well, but the generic ALSA driver does not provide controls for the device's software mixer for some devices. The ProFXv3 also shows up as a mixer section in QasMixer; in other words, everything this piece of hardware can offer on a computer is fully available (Figure 2). For the specs, see the “ProFX Mixer Details” box.

The first thing you notice about the ProFX10v3 mixer is its very solid build. All of the controls, switches, and connectors are easy to reach and leave the user with a reliable impression. Nothing wobbled, and I didn't encounter any annoying noise during operation. Everything is clearly legible and sensibly labeled. Thanks to illuminated mute switches, the ProFX10v3 mixer is also useful for live gigs in poor lighting conditions.

The 10 in the name ProFX10v3 stands for the analog inputs whose stereo output is routed to the two PCM inputs of the USB interface. The mixer's master

![](bbox=[0.07, 0.31, 0.65, 0.53])

**Figure 1:** Mackie's ProFX10v3 mixer only has dials instead of channel faders, but it can sit next to a normal laptop on your desk.

# ProFX Mixer Details

The mixer offers a great deal on a small footprint. To use the inserts in the first four channels, you need a stereo jack plug to route one channel out with the other receiving the processed signal (Figure 3). The FX in the mixer's name stands for digital effects computed by the GigFX engine in the mixer. These effects can be inserted into each channel. For the complete version 3 series manual, visit the Mackie product page [3].

![](bbox=[0.07, 0.57, 0.92, 0.9])

**Figure 2:** Immediately after connecting, the ProFX shows up with two inputs and four outputs for jackd (with the Carla audio plugin host here), which you can control with QasMixer.