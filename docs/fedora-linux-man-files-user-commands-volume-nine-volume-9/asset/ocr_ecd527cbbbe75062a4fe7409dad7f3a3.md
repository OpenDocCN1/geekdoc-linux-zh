Interactive boot nus/prompts can be enabled via **nu=on** as far as firmware/BIOS supports them. The default is non-interactive boot.

A splash picture could be passed to bios, enabling user to show it as logo, when option splash=sp_na is given and nu=on, If firmware/BIOS supports them. Currently Seabios for X86 system support it. limitation: The splash file could be a jpeg file or a bmp file in 24 bpp format(true color). The resolution should be supported by the SVGA mode, so the recommended is 320x240, 640x480, 800x640.

A tiout could be passed to bios, guest will pause for rb_tiout ms when boot failed, then reboot. If rb_tiout is ‘-1’, guest will not reboot, qe passes ‘-1’ to bios by default. Currently Seabios for X86 system support it.

Do strict boot via **strict=on** as far as firmware/BIOS supports it. This only effects when boot priority is changed by bootindex options. The default is non-strict boot.

```
# try to boot from network first, then from hard disk qe-system-i386 -boot order=nqc # boot from CD-ROM first, switch back to default order after
# reboot qe-system-i386 -boot once=d # boot with a splash picture for 5 seconds. qe-system-i386 -boot nu=on, splash=/root/boot.bmp, splash-ti=5000
```

Note: The legacy format ‘boot drives’ is still supported but its use is discouraged as it may be removed from future versions.

-m [size=]gs,slots=n,maxm=size Sets guest startup RAM size to gs gabutes. Default is 128 MiB. Optionally, a suffix of “M” or “G” can be used to signify a value in gabutes or gigabytes respectively. Optional pair slots, maxim could be used to set amount of hotpluggable morv slots and maxim amount of morv. Note that maxim st be aligned to the page size.

For example, the following command-line sets the guest startup RAM size to 1GB, creates 3 slots to hotplug additional morv and sets the maxim morv the guest can reach to 4GB: qe-system-x86_64 -m 1G, slots=3, maxim=4G

If slots and maxim are not specified, morv hotplug won’t be enabled and the guest startup RAM will never increase.

-m-path path Allocate guest RAM from a temporarily created file in path. -m-prealloc Preallocate morv when using -m-path. -k language Use keyboard layout language (for example fr for French). This option is only needed where it is not easy to get raw pc keycodes (e.g. on Macs, with so X11 servers or with a vnc display). You don’t normally need to use it on PC/Linux or PC/Windows hosts.

The available layouts are: ar de-ch es fo fr-ca hu ja mk no pt-br sv da en-gb et fr fr-ch is lt nl pl ru th de en-us fi fr-be hr it lv nl-be pt sl tr

The default is en-us.

-audio-help Will show the audio subsystem help: list of drivers, tunable paraters. -soundhw card1[,card2,...] or -soundhw all Enable audio and selected sound hardware. Use ‘help’ to print all available sound hardware.