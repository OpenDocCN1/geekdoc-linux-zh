
You can interchangeably add and remove PCMCIA cards as you wish. They will be recognized from a database of supported cards and configured using their appropriate startup scripts. This task is handled by the cardmgr daemon, which scans for insertion and removal events on the PCMCIA device, detecting an added device and automatically loading the appropriate kernel module. The cardmgr tool will generate a /var/lib/pcmcia/stab file, which will list the socket number, device class, driver, and a device number for devices that use the same driver. An stab entry can use the device class to determine which startup configuration script to use for that device.

You can obtain information about a PCMCIA device with the cardctl command, as well as manually eject and insert a device. The status, config, and ident options will display the device’s socket status and configuration, and the identification of the device. The insert and eject option will let you add and remove a device. The cardinfo command also provides device information.

It is not advisable to hot swap IDE or SCSI devices. For these you should first manually shutdown the device using the cardctl command.

```
cardctl eject
```

All PCMCIA configurations support the use of schemes, which let you specify different sets of settings for your devices. For example, for an Ethernet device you could have one set of settings to use at the office and one to use at home. For the office settings you could create an office scheme and for the home settings, a home scheme. When starting up the device you can specify which scheme to use. You can find out the current scheme in use with the cardctl command and the scheme option with no argument. To change to a certain scheme you supply the scheme argument, which will change the scheme for that device.

```
cardctl scheme home
```

## Installing Sound, Network, and Other Cards

To install a new card, your kernel must first be configured to support it. Support for most cards is provided in the form of modules that can be dynamically loaded into the kernel. Installing support for a card is usually a simple matter of loading a module that includes the drivers for it. For example, drivers for the Sound Blaster sound card are in the module sb.o. Loading this module makes your sound card accessible to Linux. Most distributions automatically detect the cards installed on your system and load the needed modules. If you change sound cards, the new card is automatically detected by Kudzu, invoking redhat-config-soundcard to configure it. For network cards, Kudzu invokes redhat-config-network to perform the configuration. You could also load modules you need manually, removing an older conflicting one. The section "Modules" later in this chapter describes this process.

Ethernet card on your system. An alias used to reference the module used for that particular card, for example, a 3Com Etherlink XL card, aliases the 3c59x network module, whose alias would be eth0 if it is the first Ethernet card. The modules themselves are kept in the kernel’s module directory, /lib/modules, as described in the last section.

## Sound Devices

On Red Hat, you can use the redhat-config-soundcard utility to install most sound cards on Linux. A listing of the different sound devices is provided in Table 32-3. Some sound cards may require more specialized support. For sound cards, you can tell what your current sound configuration is by listing the contents of the /dev/sndstat file. You can test your card by simply redirecting a sound file to it, as shown here:

```
cat sample.au > /dev/audio.
```

For the 2.4 kernel, most Linux sound drivers are developed as part of the Open Sound System (OSS) and freely distributed as OSS/Free. These are installed as part of Linux distributions. The OSS device drivers are intended to provide a uniform API for all Unix platforms, including Linux. They support Sound Blaster- and Windows Sound System-compatible sound cards (ISA and PCI). OSS is also available for a nominal fee and features configuration interfaces for device setup.

The Advanced Linux Sound Architecture (ALSA) replaces OSS in the 2.6 Linux kernel that aims to be a better alternative to OSS, while maintaining compatibility with it. ALSA provides a modular sound driver, an API, and a configuration manager. ALSA is a GNU project and is entirely free; its Web site at www.alsa-project.org contains extensive documentation, applications, and drivers. Currently available are the ALSA sound driver, the ALSA Kernel API, the ALSA library to support application development, and the ALSA manager to provide a configuration interface for the driver. ALSA evolved from the Linux Ultra Sound Project.

The Linux Musical Instrument Digital Interface (MIDI) and Sound Pages, currently at www.xdt.com/ar/linux-snd, hold links to Web and FTP sites for Linux sound drivers for various sound cards. They also include links to sites for Linux MIDI and sound software.

### TABLE 32-3
Sound Devices

| Device | Description |
|---|---|
| /dev/sndstat | Sound driver status |
| /dev/audio | Audio output device |
| /dev/dsp | Sound sampling device |
| /dev/mixer | Control mixer on sound card |
| /dev/music | High-level sequencer |
| /dev/sequencer | Low-level sequencer |
| /dev/midi | Direct MIDI port |
