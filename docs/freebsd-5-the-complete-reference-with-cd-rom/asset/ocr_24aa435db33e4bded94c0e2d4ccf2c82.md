![](bbox=[0.15, 0.12, 0.85, 0.52])

**Figure 2-1.** The Windows Device Manager window can help you learn about your computer prior to installing FreeBSD.

chipset. Even if the information appears cryptic, it may match an option you'll find when you install FreeBSD or configure it after installation.

> **Caution** Some chips, such as many recent video card and motherboard chipsets, generate so much heat that they're covered with heat sinks, which obscure chipset identification markings. Do not attempt to remove such heat sinks because you may damage the chip, and even if you don't, you'll have a hard time re-attaching the heat sink so that it does its job.

If you can't find mention of a device in HARDWARE.TXT, that doesn't necessarily mean that it won't work. The device might be known by multiple names, and you simply haven't found the one by which it's listed in the file. Try doing a Usenet search using `http://groups.google.com` or a web search using your favorite search engine using FreeBSD and the name you've discovered. You could also try simply installing FreeBSD; the OS automatically detects many devices, so you may learn if it works quickly enough.