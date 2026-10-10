
An *audio codec* converts digital audio data to analog sound signals for playing through speakers and performs the reverse operation for recording through a microphone. Other common audio inputs and outputs that interface with a codec include headsets, earphones, handsets, hands-free, line-in, and line-out. A codec also offers *mixer* functionality that connects it to a combination of these audio inputs and outputs, and controls the volume gain of associated audio signals.[1]

[1] This definition of a mixer is from a software perspective. *Sound mixing* or *data mixing* refers to the capability of some codecs to mix multiple sound streams and generate a single stream. This is needed, for example, if you want to superimpose an announcement while a voice communication is in progress on an IP phone. The *alsa-lib* library, discussed in the latter part of this chapter, supports a plug-in feature called *dmix* that performs data mixing in software if your codec does not have the capability to perform this operation in hardware.

Digital audio data is obtained by sampling analog audio signals at specific bit rates using a technique called *pulse code modulation* (PCM). CD quality is, for example, sound sampled at 44.1kHz, using 16 bits to hold each sample. A codec is responsible for recording audio by sampling at supported PCM bit rates and for playing audio originally sampled at different PCM bit rates.

A sound card may support one or more codecs. Each codec may, in turn, support one or more audio substreams in mono or stereo.

The Audio Codec'97 (AC'97) and the Inter-IC Sound (I²S) bus are examples of industry standard interfaces that connect audio controllers to codecs:

- The Intel AC'97 specification, downloadable from http://download.intel.com/, specifies the semantics and locations of audio registers. Configuration registers are part of the audio controller, while the I/O register space is situated inside the codec. Requests to operate on I/O registers are forwarded by the audio controller to the codec over the AC'97 link. The register that controls line-in volume, for example, lives at offset `0x10` within the AC'97 I/O space. The PC system in Figure 13.1 uses AC'97 to communicate with an external codec.
- The I²S specification, downloadable from www.nxp.com/acrobat_download/Various/I2SBus.pdf, is a codec interface standard developed by Philips. The embedded device shown in Figure 13.2 uses I²S to send audio data to the codec. Programming the codec's I/O registers is done via the I²C bus.

![](img/07cc6f9c8c74622020874f66bfb53dc4_361_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_362_0.png)

AC'97 has limitations pertaining to the number of supported channels and bit rates. Recent South Bridge chipsets from Intel feature a new technology called High Definition (HD) Audio that offers higher-quality, surround sound, and multistreaming capabilities.

## Linux-Sound Subsystem

*Advanced Linux Sound Architecture* (ALSA) is the sound subsystem of choice in the 2.6 kernel. *Open Sound System* (OSS), the sound layer in the 2.4 kernel, is now obsolete and deprecated. To help the transition from OSS to ALSA, the latter provides OSS emulation that allows applications conforming to the OSS API to run unchanged over ALSA. Linux-Sound frameworks such as ALSA and OSS render audio applications independent of the underlying hardware, just as codec standards such as AC'97 and I²S do away with the need of writing separate audio drivers for each sound card.

Take a look at Figure 13.3 to understand the architecture of the Linux-Sound subsystem. The constituent pieces of the subsystem are as follows:

- The sound core, which is a code base consisting of routines and structures available to other components of the Linux-Sound layer. Like the core layers belonging to other driver subsystems, the sound core provides a level of indirection that renders each component in the sound subsystem independent of the others. The core also plays an important role in exporting the ALSA API to higher applications. The following `/dev/snd/control*` device nodes shown in Figure 13.3 are created and managed by the ALSA core: `/dev/snd/control0` is a control node (that applications use for controlling volume gain and such), `/dev/snd/pcmC0D0p` is a playback device (*p* at the end of the device name stands for playback), and `/dev/snd/pcmC0D0c` is a recording device (*c* at the end of the device name stands for capture). In these device names, the integer following $C$ is the card number, and that after $D$ is the device number. An ALSA driver for a card that has a voice codec for telephony and a stereo codec for music might export `/dev/snd/pcmC0D0p` to read audio streams destined for the former and `/dev/snd/pcmC0D0c` to channel music bound for the latter.
- Audio controller drivers specific to controller hardware. To drive the audio controller present in the Intel ICH South Bridge chipsets, for example, use the `snd_intel8x0` driver.
- Audio codec interfaces that assist communication between controllers and codecs. For AC'97 codecs, use the `snd_ac97_codec` and `ac97_bus` modules.
- An OSS emulation layer that acts as a conduit between OSS-aware applications and the ALSA-enabled kernel. This layer exports `/dev` nodes that mirror what the OSS layer offered in the 2.4 kernels. These nodes, such as `/dev/dsp`, `/dev/adsp`, and `/dev/mixer`, allow OSS applications to run unchanged over ALSA. The OSS `/dev/dsp` node maps to the ALSA node `/dev/snd/pcmC0D0*`, `/dev/adsp` corresponds to `/dev/snd/pcmC0D1*`, and `/dev/mixer` associates with `/dev/snd/control0`.
- Procs and sysfs interface implementations for accessing information via `/proc/asound/` and `/sys/class/sound/`.
- The user-space ALSA library, *alsa-lib*, which provides the `libasound.so` object. This library eases the job of the ALSA application programmer by offering several canned routines to access ALSA drivers.
- The *alsa-utils* package that includes utilities such as *alsamixer*, *amixer*, *alsactl*, and *aplay*. Use alsamixer or amixer to change volume levels of audio signals such as line-in, line-out, or microphone, and alsactl to control settings for ALSA drivers. To play audio over ALSA, use aplay.

### Figure 13.3. Linux-Sound (ALSA) subsystem.

[View full size image]

![](img/07cc6f9c8c74622020874f66bfb53dc4_364_0.png)

To obtain a better understanding of the architecture of the Linux-Sound layer, let's look at the ALSA driver modules running on a laptop in tandem with Figure 13.3 ( `⇒` is used to attach comments):

```
bash> lsmod|grep snd

snd_intel8x0    33148  0                  ⇒ Audio Controller Driver
snd_ac97_codec   92000  1 snd_intel8x0     ⇒ Audio Codec Interface
ac97_bus         3104   1 snd_ac97_codec   ⇒ Audio Codec Bus
snd_pcm_oss      40512  0                  ⇒ OSS Emulation
snd_mixer_oss    16640  1 snd_pcm_oss      ⇒ OSS Volume Control
snd_pcm          73316  3 snd_intel8x0, snd_ac97_codec, snd_pcm_oss,
                           snd_mixer_oss, snd_pcm, snd_timer      ⇒ Core layer
snd_timer        22148  1 snd_pcm          ⇒ Core layer
snd              50820  6 snd_intel8x0, snd_ac97_codec, snd_pcm_oss,
                           snd_mixer_oss, snd_pcm, snd_timer      ⇒ Core layer
soundcore        8960   1 snd              ⇒ Core layer
snd_page_alloc   10344  2 snd_intel8x0, snd_pcm ⇒ Core layer
```

## Device Example: MP3 Player

Figure 13.4 shows audio operation on an example Linux Bluetooth MP3 player built around an embedded SoC. You can program the Linux cell phone (that we used in Chapter 6, "Serial Drivers," and Chapter 12, "Video Drivers") to download songs from the Internet at night when phone rates are presumably cheaper and upload it to the MP3 player's *Compact Flash* (CF) disk via Bluetooth so that you can listen to the songs next day during office commute.

### Figure 13.4. Audio on a Linux MP3 player.

![](img/07cc6f9c8c74622020874f66bfb53dc4_366_0.png)

Our task is to develop the audio software for this device. An application on the player reads songs from the CF disk and decodes it into system memory. A kernel ALSA driver gathers the music data from system memory and dispatches it to transmit buffers that are part of the SoC's audio controller. This PCM data is forwarded to the codec, which plays the music through the device's speaker. As in the case of the navigation system discussed in the preceding chapter, we will assume that Linux supports this SoC, and that all architecture-dependent services such as DMA are supported by the kernel.

The audio software for the MP3 player thus consists of two parts:

1. A user program that decodes MP3 files reads from the CF disk and converts it into raw PCM. To write a native ALSA decoder application, you can leverage the helper routines offered by the *alsa-lib* library. The section "ALSA Programming" looks at how ALSA applications interact with ALSA drivers.
   - You also have the option of customizing public domain MP3 players such as *madplay* (http://sourceforge.net/projects/mad/) to suit this device.
2. A low-level kernel ALSA audio driver. The following section is devoted to writing this driver.
