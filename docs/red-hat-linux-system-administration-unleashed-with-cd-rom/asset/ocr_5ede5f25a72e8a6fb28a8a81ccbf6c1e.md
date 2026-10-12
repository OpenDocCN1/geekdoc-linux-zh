+   - Support by the Linux kernel for the device chosen
+   - Support for the device by the backup software you have chosen
+   - Data storage capacity of the media
+   - Data transfer rate of the backup device

Of these factors, the first one that I would consider is whether or not the device is supported natively by the Linux kernel. You may find a backup solution that is inexpensive, has sufficient data storage capacity to meet your needs, and find backup software, whether freeware, shareware, or commercial, that will work with the device, but if your version of the Linux kernel doesn't support the device, you are out of luck.

The next consideration is whether the backup software you have chosen is compatible with the device. For example, if your backup software is a custom package that you developed and it uses the dump command, using a recordable CD drive as the media is not an option.

The data storage capacity of the media is another factor that must be carefully considered. For example, in the early days of DOS, when a 20-megabyte hard drive was considered sufficient for a desktop system, it was not uncommon to use floppy disks to back up a system. In fact, this was one of the few backup media choices available. Now, however, when systems come with 8-, 10-, or 14-gigabyte drives, anyone who would consider backing up their system to floppy would probably be committed to a mental institution. It is therefore very important to take into account the data capacity of the media for the devices you are considering.

Finally, and what is arguably the most important factor in making your decision next to support by the Linux kernel, is the transfer rate for writing data to the device. You may find that there are several possible solutions that you could implement, but what good does it do to have a supported and inexpensive backup device capable of backing up your entire system if it takes a week to do so?

# The Autoloader Question

Another aspect to consider when evaluating backup devices is whether to purchase one with an autoloading mechanism. As disks get bigger and bigger (and the data never seems to stop filling them up), the ability to back up a single machine onto a single tape has become harder. The solution is to have multiple tapes for a single machine. However, backing up one machine onto multiple tapes usually means that a human being has to be present to change tapes. Backing up large amounts of data is no mean feat with only a