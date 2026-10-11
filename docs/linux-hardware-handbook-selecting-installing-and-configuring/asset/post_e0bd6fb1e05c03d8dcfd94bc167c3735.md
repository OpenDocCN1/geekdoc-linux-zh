
![](img/860d0c38bd76c9ded976e9d1e179ef25_307_0.png)

**FIGURE 10.1**
*A waveform is translated into movements of membranes in a speaker, which creates pressure changes in the air that we hear as sound.*

## Bits on the Bus

Before proceeding further, it’s important to distinguish between the *sample* bit size and the *bus’s* bit size. The ISA bus comes in 8- and 16-bit variants, and the PCI bus comes in 32- and 64-bit variants (although 64-bit PCI buses are extremely rare). These bus bit sizes are completely irrelevant to the size of the samples used by the sound card. For instance, suppose you’ve got a 32-bit PCI sound card. You can play 8- or 16-bit sounds on this device; the card simply transfers four or two samples with each operation, or possibly transfers one with some wasted space in the transfer. In theory, an 8-bit ISA sound card could handle 16-bit sounds by using two transfers for each sample. In practice, however, ISA sound cards that use 16-bit sound samples also use 16-bit ISA bus interfaces.

The size of the bus (8–64 bits) is important to data transfer speed, although it’s not the only factor in determining that speed. As described earlier, however, the 16-bit ISA bus’s 8MB/s speed is quite adequate for most sound functions. Indeed, even the slower 8-bit ISA bus is more than adequate, especially for the slower 8-bit sound samples generally used on such cards.

## Bits in the Sample

When used in reference to a sound card, the card’s “bittness” generally refers to the number of bits in the sound sample. At any given moment in time—represented by a position on the X-axis of Figure 10.1—a sound waveform can be described by a single value—represented by a position along the Y-axis of Figure 10.1. (Figure 10.1 includes two waveforms, for left and right channels. Each has its own value at any given time.) This value is almost always either 8 or 16 bits in size. An 8-bit sample size allows for 2⁸, or 256, distinct values. A 16-bit sample size allows for 2¹⁶, or 65,536, distinct values. An 8-bit value is a bit deficient, but a 16-bit value is large enough that most humans would hear little or no difference if the sample size were increased to 24 or 32 bits. Some audiophiles claim to be able to hear the difference between 16-bit and 24-bit sound, though. As I mentioned earlier, CDs use 16-bit audio.

In the mid-1990s, sound cards were easily broken into two categories: 8-bit and 16-bit. The 8-bit cards were unable to record or play back 16-bit sounds. Sound card names frequently included the number *8 or 16* to distinguish the quality of the product. Some later products put higher values into the product name, such as 32. This practice led some people to believe that these sound cards could record 32-bit samples, but, in fact, the value 32 referred to some other characteristic, such as 32 MIDI voices. Aside from very high-end audiophile products, few sound cards today use better than 16-bit sound.

All 16-bit sound cards are capable of playing and recording 8-bit sounds. In fact, some Linux drivers only support 8-bit sound, even on 16-bit cards. For example, as of kernels 2.2.14 and 2.3.47, the Linux kernel drivers for the VIA MVP4 chipset only support 8-bit sound, although the chipset is capable of 16-bit operation, and can achieve this performance with the commercial OSS drivers or the ALSA project drivers. As a general rule, enforced 8-bit operation under Linux arises because the sound drivers run the sound card in a mode that emulates the old 8-bit SoundBlaster Pro. It's a good idea to check the drivers for any sound card you're considering to be sure that the drivers run the card in its native 16-bit mode rather than in an 8-bit compatibility mode.

### Sample Frequency

At least as important as the sample size is the sample frequency. This characteristic refers to the number of samples taken per second. Audio CDs are recorded at 44,100Hz—that is, 44,100 samples per second. Most sound cards sold today can record at up to that rate, if not higher. Some can go to 48,000Hz, which is the sample rate used by digital audio tape (DAT) recorders.

> **TIP**
>
> If you want to manipulate sound files that originated on, or will be transferred to, DAT, be sure your sound card can handle 48,000Hz sample frequency. This advice doesn't apply if you're using a DAT drive only for backup purposes. It only applies if you intend to use DAT as an audio platform.

Sample frequency affects how high a tone can be recorded. As a general rule, you need a sample rate of at least twice the frequency of the tone you want to record. For instance, consider Figure 10.2, which shows a pure tone of 20,000Hz. This means that a peak or valley occurs 20,000 times a second, or once every 0.00005s. Now, consider a digital sample frequency of 0.00005s (20,000Hz). The result might be Samples 1 and 3 shown in Figure 10.2. Because these samples occur at two peaks of the same height, the result would be interpreted by a sound card as a flat line—the sound card wouldn't know that a valley existed between the two samples. To reproduce the 20,000Hz tone with any accuracy, it's necessary to double the sample frequency to 40,000Hz, which adds Sample 2 to the mix. Now the sound card can reproduce a reasonable facsimile of the waveform, with both peaks and valleys intact.

![](img/860d0c38bd76c9ded976e9d1e179ef25_309_0.png)

**FIGURE 10.2**

To reproduce a sound, a digital reproduction method must sample the signal frequently enough to detect both the peaks and valleys of the original signal.

Note that I said you need to sample a sound using a sample rate of at least twice the sample frequency, in order to reproduce the sound. Consider what would happen if Figure 10.2's samples occurred at points slightly offset from the peaks and valleys, as shown in Figure 10.3. The result is a greatly attenuated sound—the volume will be reduced. In a worst-case scenario, the volume will be so low that the sound will be inaudible.

Matters are complicated still further by real-life sounds, which usually don't consist of the pure tones depicted in Figures 10.2 and 10.3. Real-life sounds consist of several different frequencies overlaid upon one another, which creates complex waveforms, such as those shown in Figure 10.1. Fortunately, it's the highest-frequency tones that are most important in determining the requirements for digital audio sample rates. For instance, if a 20Hz tone were overlaid on the waveform shown in Figures 10.2 and 10.3, these figures would barely need to be modified, because 1000 of the 20,000Hz waves would fit within a single 20Hz wave. On the scale used in Figures 10.2 and 10.3 (just three 20,000Hz waves), the shifts associated with the 20Hz tone would be minor.

![](img/860d0c38bd76c9ded976e9d1e179ef25_310_0.png)

**FIGURE 10.3**

*If a digital sample at twice a pure tone’s frequency is offset from the sound’s peaks and valleys, its apparent volume will be reduced in the reproduction.*

As a result of these considerations, you can see that the maximum 44,100Hz sample rate produces a maximum best-case accurate reproduction for most sound cards of about 22,050Hz, with the potential for some attenuation of volume at more than 11,025Hz. It’s no coincidence that the range for adult human hearing is approximately 20–20,000Hz. (Children can often hear somewhat higher than this, and some animals, such as dogs and dolphins, can hear much higher tones.)

Many of the sounds we hear in everyday life contain little in the way of high-frequency components, however. For recording a person speaking normally, a much lower sample rate might suffice. You should have no trouble understanding speech recorded at 8000Hz, for instance. If you want to accurately reproduce most music, though, a 44,100Hz recording rate is an absolute must.

All sound cards support setting a variety of recording and playback sample rates, and most sound software offers you a choice of several standard rates—generally power-of-2 fractions of 44,100Hz or multiples of 8,000Hz. You can therefore adjust your recording sample rate to fit the type of audio you’re recording.

## Channels

Most sound cards support both mono and stereo recording and playback. Just as in other audio equipment, mono operation records just one audio signal, whereas stereo operation records two—one for each of the two speakers you probably have connected to your computer.
