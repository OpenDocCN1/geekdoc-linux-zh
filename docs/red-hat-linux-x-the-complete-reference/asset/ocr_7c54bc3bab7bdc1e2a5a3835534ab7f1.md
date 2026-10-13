# Sound Devices

On Red Hat, you can use the redhat-config-soundcard utility to install most sound cards on Linux. A listing of the different sound devices is provided in Table 32-3. Some sound cards may require more specialized support. For sound cards, you can tell what your current sound configuration is by listing the contents of the /dev/sndstat file. You can test your card by simply redirecting a sound file to it, as shown here:

```
cat sample.au > /dev/audio.
```

For the 2.4 kernel, most Linux sound drivers are developed as part of the Open Sound System (OSS) and freely distributed as OSS/Free. These are installed as part of Linux distributions. The OSS device drivers are intended to provide a uniform API for all Unix platforms, including Linux. They support Sound Blaster- and Windows Sound System- compatible sound cards (ISA and PCI). OSS is also available for a nominal fee and features configuration interfaces for device setup.

The Advanced Linux Sound Architecture (ALSA) replaces OSS in the 2.6 Linux kernel that aims to be a better alternative to OSS, while maintaining compatibility with it. ALSA provides a modular sound driver, an API, and a configuration manager. ALSA is a GNU project and is entirely free; its Web site at www.alsa-project.org contains extensive documentation, applications, and drivers. Currently available are the ALSA sound driver, the ALSA Kernel API, the ALSA library to support application development, and the ALSA manager to provide a configuration interface for the driver. ALSA evolved from the Linux Ultra Sound Project.

Table 32-3: Sound Devices

| Device | Description |
|---|---|
| /dev/sndstat | Sound driver status |
| /dev/audio | Audio output device |
| /dev/dsp | Sound sampling device |
| /dev/mixer | Control mixer on sound card |
| /dev/music | High-level sequencer |
| /dev/sequencer | Low-level sequencer |
| /dev/midi | Direct MIDI port |

The Linux Musical Instrument Digital Interface (MIDI) and Sound Pages, currently at www.xdt.com/ar/linux-snd, hold links to Web and FTP sites for Linux sound drivers for various sound cards. They also include links to sites for Linux MIDI and sound software.