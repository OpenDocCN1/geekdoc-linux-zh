# # The ALSA Driver Project

The ALSA project (http://www.alsa-project.org/) provides an alternative sound driver architecture for Linux. To use the ALSA drivers, you must download and compile three separate packages:

+   - `alsa-driver`  The ALSA driver files proper
+     - `alsa-lib`  Libraries used by ALSA-enabled programs and utilities
+       - `alsa-util`  Programs to use sound with the ALSA drivers

You compile each package much as you would other source code programs, by typing `./configure` and then `make install`. You should probably issue additional parameters to at least some of the configuration procedures, however, in order to add or remove support for features you do or do not need. Consult the INSTALL and README files that come with each package for details. You must also run the snddevices script that comes with the driver package in order to create appropriate ALSA sound device files in your /dev directory.

When the ALSA drivers are installed and the modules loaded, you can use your sound devices. You can compile the ALSA drivers with OSS compatibility support for digital audio functionality, and I recommend you do so. Many programs—particularly games and audio utilities that serve as adjuncts to desktop environments—assume that they'll be dealing with OSS-style audio drivers, so omitting this feature can reduce the utility of your sound system. You must explicitly load OSS compatibility modules for digital audio (snd-pcm-oss), MIDI (snd-seq-oss), and mixers (snd-mixer-oss) in order to use OSS-style audio applications. If you want to use software waveable, you can use the TiMidity program with ALSA.

# # Sound Card Resource Allocations

Although the commercial OSS driver set includes utilities to help detect and configure sound cards, the kernel's OSS drivers and ALSA drivers rely upon manual configuration of the sound card in other ways. Two files are particularly important to this configuration:

+   - `/etc/isaapnp.conf`  This file contains configuration information for ISA PnP cards. I describe its configuration in detail in the section “ISA Bus” in Chapter 2. You only need to deal with this configuration file if you have an ISA PnP board. If you have a PCI sound card or an older jumper-configured ISA card, the card is configured automatically or through jumpers, respectively. In addition, the 2.3.x and later kernels include ISA PnP configuration features independent of the isaapntools utility package, for which `/etc/isaapnp.conf` is the configuration file.