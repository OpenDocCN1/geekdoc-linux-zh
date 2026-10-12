# Loading and unloading modules

You can manage the loadable device driver modules by using a set of com-mands. You have to log in as root to use some of these commands. In Table 5-1, I summarize a few of the commonly used module commands.

Table 5-1 Commands to Manage Kernel Modules

This Command Does the Following
insmod Inserts a module into the kernel
rmmod Removes a module from the kernel
depmod Determines interdependencies between modules
ksyms Displays a list of symbols along with the name of the module that defined the symbol
lsmod Lists all currently loaded modules
modinfo Displays information about a kernel module
modprobe Inserts or removes a module or a set of modules intelligently (for example, if module A requires B, then modprobe automatically loads B when asked to load A)

If you have to use any of these commands, log in as root or type su - in a terminal window to become root.

To see what modules are currently loaded, type

lsmod

You see a list of modules. For example, here is a list on one of my laptops running Fedora Core:

```
Module             Size  Used by
hid                50580  0
ntfs               78924  1
ide_cd             32644  0
snd_mixer_oss      14336  1
snd_intel8x0       30120  1
snd_ac97_codec     53768  1
snd_pcm            84744  1
snd_timer          25604  1
gameport           4352   1
snd_page_alloc     9092   2
snd_mpu401_uart    7680   1
snd_rawmidi        21792  1
snd_seq_device     6792   1
snd                44516  8
snd_mixer_oss,snd_intel8x0,snd_ac97_codec,snd_pcm,snd_time r,snd_mpu401_uart,snd_rawmidi,snd_seq_device
```