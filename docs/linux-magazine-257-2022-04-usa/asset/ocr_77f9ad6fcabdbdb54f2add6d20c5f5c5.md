The DAC+ ADC in the middle then generates the audio signals, which it passes on to the speakers through the AAMP60 amplifier on top. The pair currently costs 595 (£110/EUR85). The performance of the AAMP60 is the same as that of the Amp2. Unlike the Amp2, however, the DAmp60 needs the DAC+ ADC or another compatible HifiBerry sound card.

# ## Other Accessories

The Aamp60, Amp2, and Beocreate each have a connector for an external power supply. Four-ohm speakers need a power supply rated at 12V-18V; for 8-ohm speakers, the developers advise you to go for 18V.

According to the data sheet, the Amp2 can handle a maximum of 24V and the AAMP60 20V. If you want to be on the safe side, purchase the respective board along with the matching power supply in the HifiBerry store. The Amp2 and Beocreate supply the Raspberry Pi with power; the AAMP60 additionally supplies the DAC+ ADC. Consequently, the Raspberry Pi does not need its own power supply.

To play audio material over Bluetooth, you also need a USB dongle. The exceptions here are the Raspberry Pi 3B+ and 4.

![](bbox=[0.09, 0.09, 0.64, 0.34])

Figure 1: The Amp2 contains a small DAC+ sound module on-board, so all signal processing takes place on the board, without the need for any other hardware.

device, and you can control it in a browser. Under the hood is a customized Linux system with preconfigured services at work. Details can be found in the "Tricky Manual Steps" box.

# ## Hardware Zoo

Modul 9 offers several audio amplifiers for different purposes. The MiniAmp [2] for $22 (£20/EUR15) is designed for the small Pi Zero and only has two 3W outputs, which, although enough for small PC speakers, is not good enough for a sound system in your living room.

Fortunately, an all-purpose weapon named Amp2 (Figure 1) [3] comes in at $55 (£54/EUR46). The amplifier has two outputs rated at 30W, which might not sound like much at first, but the small circuit board neighborlessly managed to delight even my neighbors on the next floor with hard rock.

Both the MiniAmp and the Amp2 only support two speakers at a time. If you want to connect more, you can get the Beocreate 4 Channel Amplifier for $190 (£175/EUR160) [4]. As the name suggests, it offers a total of four channels, with two connections even delivering 60W. Additionally, the Beocreate has a digital signal processor with which you can apply various effects to the audio signal in HifiBerryOS, if required. Unfortunately, the company does not offer a solution for surround sound.

All of these boards come without an audio input, but to continue using an old CD player, you need an analog sound card with input in the HifiBerry universe. For this project, I went for the DAC+ analog-to-digital (ADC) converter [5], combined directly with the AAMP60 amplifier [6]. However, unlike the Amp2, it does not have its own sound card, so you will have to piggy-back the two HifiBerry boards on the Raspberry Pi (Figure 2).

![](bbox=[0.65, 0.55, 0.95, 0.9])

Figure 2: The AAMP60 requires a compatible HifiBerry sound card. Here, a DAC+ ADC is plugged directly onto the GPIO ports at the bottom, with the AAMP60 sitting on top.