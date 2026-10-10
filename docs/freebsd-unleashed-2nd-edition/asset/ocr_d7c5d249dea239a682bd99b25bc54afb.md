Note that in this case, **sbc0** is actually the name for a group of devices related to the sound card. The sound card uses several devices, depending on what features you want to access, including **dsp**, which is where output such as WAV and MP3 files go, and **mixer**, which controls the levels of various audio devices.

You may also see some of the following lines on your startup message:

unknown: <PNP0033> can't assign resources
unknown: <PNP0F13> can't assign resources
unknown: <PNP0501> can't assign resources
unknown: <PNP0700> can't assign resources
unknown: <PNP0401> can't assign resources
unknown: <PNP0501> can't assign resources

These lines indicate that the kernel has found some “Plug and Play” (often abbreviated to PnP) devices in the system, but it doesn’t know anything about them, and it can’t assign resources for them. These messages are harmless. If you don’t like seeing them, then note that, as the FreeBSD FAQ says, “the FreeBSD project will happily accept driver contributions via send-pr.” (This is for you C gurus who are good at writing device drivers.)

The next message shows that the kernel has found the hard drives, and it provides various information about the drives, including device name, size, manufacturer and model, geometry, and what controller the drive is located on:

ad0: 19473MB <Maxtor 92049U6> [39566/16/63] at ata0-master UDMA33
ad1: 14664MB <IBM-DJNA-351520> [29795/16/63] at ata0-slave UDMA33

It also tells what access mode the drive is using. In this case, both of the drives are using Ultra DMA 33. (This will be covered in more detail in Chapter 18, “Understanding Hard Disks and Filesystems.”)

The final message shows that the kernel has mounted the root filesystem:

Mounting root from ufs:/dev/ad0s1a

After the root filesystem is mounted, the kernel passes control to a process called **init**. The messages in light gray are triggered by events that occur during the **init** stage. You can differentiate kernel messages from non-kernel messages by color. Kernel messages appear in white; non-kernel messages appear in light gray.

# ### init

The **init** program is the first actual process that runs under the operating system, and as such its process ID is 1. **init** is responsible for starting up all the rest of the processes that constitute a completely functional operating system; to do that, though, it must first determine whether the disks are in suitable shape.