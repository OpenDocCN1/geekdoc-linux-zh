the version of these drivers included in the Linux kernel will suffice. To configure these drivers, you need to activate several kernel options. These are located in the Ftape, the floppy tape device driver configuration area, which is located in the Character devices menu. Options you must set include

+   * **Ftape (QIC-80/Travan) support**  This option is necessary to activate the more specific features.
+   * **Zftape, the VFS interface**  This feature has historically been optional, but is a requirement for 2.2x and later kernels.
+   * **Floppy tape controllers**  This option should usually be left at the default value of Standard. Some floppy-interfaced drives, however, come with optional ISA cards that enable them to operate more quickly. If you use such a card, select it from the list.

The Ftape device files usually contain $rt$ in their names, such as /dev/rft$x$ and /dev/nrf$x$ for rewinding and non-rewinding devices, respectively, where $x$ is a number from 0–4. Device numbers for these devices files are major 27 and minor 0–3 for /dev/rft$x$ and minor 4–7 for /dev/nrf$x$. Ftape versions in the 3.0$x$ range supported separate compression devices that typically used device filenames of the form /dev/zqft$x$ and /dev/nqft$x$, but this feature was removed from Ftape 4.0$x$ in order to support improved error recovery features. If you use a 3.0$x$ version of Ftape along with the compression devices, the effect is much like using a tape device with built-in compression, except that your computer’s CPU does the compression. Using the 4.0$x$ version of the driver requires that you use backup software that supports compression, assuming you want to compress your data as you back it up.

# ### Parallel Port Interfaces

As with many other external devices, the parallel port has long served as an interface method for removable tape backup drives. The parallel port was never intended for this function, however, and the results aren’t as reliable as can be achieved with SCSI or ATAPI drives. If you want an external tape backup device, therefore, I favor using a SCSI drive. In the future, USB and FireWire might fill this niche, as well.

For all parallel-port tape devices, you must select $Y$ or $M$ to the Parallel port support option in the kernel’s General setup area. You must also activate additional options, depending upon the type of parallel-port drive you have.

The Ftape driver, which is generally thought of as a driver for floppy-interfaced devices, supports a fair number of parallel-interfaced tape devices. When used with these devices, the Ftape driver uses the same kernel compilation options and device filenames, so check the section of floppy-based drives for more information.