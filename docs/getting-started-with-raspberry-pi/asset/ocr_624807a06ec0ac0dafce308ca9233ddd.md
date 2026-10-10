# # Patch Submission

To generate a kernel patch out of your changes, use the `diff` command:

Code View:
`bash> diff -Nur /path/to/original/kernel /path/to/your/kernel > changes.patch`

Note that the original kernel precedes the changed version in the `diff`-ing order. As per 2.6 kernel patch submission conventions, you also need to add a line at the end of the patch that says this:

`Signed-off-by: Name <Email>`

With this, you certify that you wrote the code yourself and that you have the right to contribute it.

You are now all set to post your patch to the relevant mailing list, such as LKML.

Look at *Documentation/SubmittingPatches* for a guide on creating patches for submission and at *Documentation/applying-patches.txt* for a tutorial on applying patches.

Now that your patched `/usr/src/linux-X.Y.Z/` tree is ready for use, let’s take a moment to observe how the source layout is organized. Go to the root of the source tree and list its contents. The directories branching out from the root of the code tree are as follows:

+   1.  **arch.** This directory contains architecture-specific files. You will see separate subdirectories under `arch/` for processors such as ARM, Motorola 68K, s390, MIPS, Alpha, SPARC, and IA64.

+   2.  **block.** This primarily contains the implementation of I/O scheduling algorithms for block storage devices.

+   3.  **crypto.** This directory implements cipher operations and the cryptographic API, used, for example, by some WiFi device drivers for implementing encryption algorithms.

+   4.  **Documentation.** This directory has brief descriptions of various kernel subsystems. This can be your first stop to dig for answers to kernel-related queries.

+   5.  **drivers.** Device drivers for numerous device classes and peripheral controllers reside in this directory. The device classes include character, serial, *Inter-Integrated Circuit* (I2C), *Personal Computer Memory Card International Association* (PCMCI A), *Peripheral Component Interconnect* (PCI), *Universal Serial Bus* (USB), video, audio, block, *Integrated Drive Electronics* (IDE), *Small Computer System Interface* (SCSI), CD-ROM, network adapters, *Asynchronous Transfer Mode* (ATM), Bluetooth, and *Memory Technology Devices* (MTD). Each of these classes live in a separate subdirectory under `drivers/`. You will, for instance, find PCMCI A driver sources inside the `drivers/pcmcia/` directory and MTD drivers inside the `drivers/mtd/` directory. The subdirectories present under `drivers/` constitute the primary subjects for this book.