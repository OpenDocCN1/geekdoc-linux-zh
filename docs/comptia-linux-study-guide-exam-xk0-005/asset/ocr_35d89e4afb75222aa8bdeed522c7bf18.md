```
0376-0376 : 0000:00:01.1
0376-0376 : ata_pix
03c0-03df : vga+
03f6-03f6 : 0000:00:01.1
03f6-03f6 : ata_pix
0cf8-0cff : PCI conf1
0d00-ffff : PCI Bus 0000:00
```

There are lots of different I/O ports in use on the Linux system at any time, so your output will most likely differ from this example. With PnP, I/O port conflicts aren't very common, but it is possible that two devices are assigned the same I/O port. In that case, you can manually override the settings automatically assigned by using the `setpci` command.

# ## Direct Memory Access

Using I/O ports to send data to the CPU can be somewhat slow. To speed things up, many devices use direct memory access (DMA) channels. DMA channels do what the name implies; they send data from a hardware device directly to memory on the system, without having to wait for the CPU. The CPU can then read those memory locations to access the data when it's ready.

As with I/O ports, each hardware device that uses DMA must be assigned a unique channel number. To view the DMA channels currently in use on the system, just display the `/proc/dma` file:

```
$ cat /proc/dma
4: cascade
$
```

This output indicates that only DMA channel 4 is in use on the Linux system.

# ## The /sys Directory

Yet another tool available for working with devices is the /sys directory. The /sys directory is another virtual directory, similar to the /proc directory. It provides additional information about hardware devices that any user on the system can access.

A number of information files are available within the /sys directory. They are broken down into subdirectories based on the device and function in the system. You can take a look at the subdirectories and files available within the /sys directory on your system by using the ls command-line command, as shown in Listing 23.4.

# Listing 23.4: The contents of the /sys directory

```
$ ls -al /sys
total 4
```