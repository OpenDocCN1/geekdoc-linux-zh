Qlogic adapter, Trantor T128, T128F, and T228 adapters, Ultrastor adapters, and the 7000 FASST adapters. Compatibles of any of these cards should also work.

+   * xt. IDE and IBM PC-XT-compatible hard disk drivers.

With some distributions, an extension is added to the kernel image name to indicate the floppy type. For example, if the kernel image is for a 1.44MB floppy, it will have the filetype “.144” as part of the name. Similarly, a filetype of “.12” indicates a 1.2MB image. You cannot interchange these images, or the disk will be useless (in other words you cannot load a .12 image onto a 1.44MB disk). Most distributions don’t bother with this convention because the files are in the appropriate directories for the disk size.

There are fewer choices for the root floppy image. Most distributions include four basic images, although a few more esoteric images also appear from time to time. The basic root floppy images are as follows:

+   * color. Offers a full-screen color-based installation script for installing Linux.

+   * tape. Designed to support Linux installation from a cartridge tape. This kernel was still not functioning properly at the time of writing.

+   * tty. A dumb terminal installation version with no color or graphics.

+   * umsdos. Used to install UMSDOS, which allows you to install Linux into an existing MS-DOS partition. The installation script creates the subdirectories it needs. UMSDOS is not as efficient or fast as a dedicated Linux partition, but you can retain your current disk partitions.

Each of the root images has the disk size as part of its name (color144 and color12, for example).

If you obtained your boot and root images from an FTP or BBR site, the files may be compressed and archived. If they are, they will end with the filetype .gz. Before you can install the images to a floppy, they must be uncompressed with the gzip utility.

**TIP**
The color root image is a lot more attractive than the tty image and can make the Linux installation a bit friendlier. However, the color image is intolerant of typing errors and doesn’t always proceed smoothly. It’s worth a try, in most cases, unless you know exactly how you want to install Linux. The color process tends to require much more user interaction, clicking on OK buttons at many stages.