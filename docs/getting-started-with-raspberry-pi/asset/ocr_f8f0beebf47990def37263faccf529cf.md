# ## Debugging

You may turn on options under *Device Drivers* **\u2192***Sound* **\u2192*****Advanced Linux Sound Architecture* in the kernel configuration menu to include ALSA debug code (`CONFIG_SND_DEBUG`), verbose `printk()` messages (`CONFIG_SND_VERBOSE_PRINTK`), and verbose procs content (`CONFIG_SND_VERBOSE_PROCFs`).

Procs information pertaining to ALSA drivers resides in `/proc/asound/`. Look inside `/sys/class/sound/` for the device model information associated with each sound-class device.

If you think you have found a bug in an ALSA driver, post it to the alsa-devel mailing list (<http://mailman.alsa-project.org/mailman/listinfo/alsa-devel>). The linux-audio-dev mailing list (<http://music.columbia.edu/mailman/listinfo/linux-audio-dev/), also called the *Linux Audio Developers* (LAD) list, discusses questions related to the Linux-sound architecture and audio applications.