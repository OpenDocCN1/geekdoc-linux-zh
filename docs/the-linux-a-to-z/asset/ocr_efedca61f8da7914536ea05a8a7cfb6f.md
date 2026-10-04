any time, whether they have a root login or not. On Linux machines for home and personal use this may not be a security issue. However, you may want to disable this feature on any machine whose main keyboard and screen are open to unauthorized access. You will see how to do this in Section 7.4 when we look at how to build a custom kernel.

Due to space restrictions on the RAM disk root filesystem, many Linux distributions do not supply the shutdown program on their setup disks. Therefore, you may need to use Ctrl-Alt-Del just for the first shutdown after initial installation.

# 7.3.6 lilo

Rebooting your Linux system from floppy disk should work fine; however, it is far more convenient if you can boot it directly from the hard disk, especially if you can have the choice of which operating system to boot, where there is more than one from which you might choose.

As I have mentioned briefly before, there is a program called lilo which can be used, along with a configuration file, to set the system up so that when the machine boots you can have exactly this choice.

If lilo is being used then at the start of the boot sequence the word:

```
LILO
```

will appear on the screen followed by a short pause. If you do nothing during this pause then lilo will boot whichever operating system or kernel it has been set up to treat as its default system. If, instead, you press one of the keys: Shift, Ctrl or Alt during the pause, then you will be presented with a:

```
boot:
```

prompt, at which you type in the name of the operating system or kernel you wish to boot. If you press the Tab key at the prompt then you will get a list of the names from which you may make your choice.

In order to set up lilo to give you these options, you just need to set up a configuration file, called:

```
/etc/lilo.conf
```

with the required information about which operating systems or kernels you want to be able to boot, where they are on your hard disks and what names you want to give them, to use at the lilo boot: prompt, and then you just type in the following command to complete the installation:

```
# lilo
```

The easiest way to appreciate what goes into the /etc/lilo.conf file is to take a look at one. The following is an example which could be used with our 320 Mb disk to boot DOS by default, but allow the choice of either dos or linux at the boot: prompt: