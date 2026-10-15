# FIGURE 12.4

Netatalk-exported filesystems give few clues to their origins.

+   - Macintoshes have traditionally used their own means of supporting long filenames on FAT floppies. These methods are incompatible with VFAT, and therefore with Linux’s handling of long filenames. Attempting to share such floppies with Macintoshes therefore loses the Macintosh-created long filenames. Fortunately, recent versions of MacOS use VFAT as DOS does, so this problem should only exist when exchanging FAT floppies with relatively elderly Macintosh systems.
+   - Linux’s HFS support is considered experimental, and may not be 100% reliable. I therefore recommend that you not mount large Macintosh removable media with irreplaceable data for read/write access. You’re unlikely to run into problems writing a few files to blank media, though, or to small disks.

# CAUTION

As of this writing, Linux kernels past 2.2.8 don’t work well in conjunction with the export of HFS media via Netatalk. The problem manifests in a hung Macintosh. If you’re using a more recent kernel and have this problem, try either the very latest kernel available (which may or may not have fixed the problem) or the 2.2.8 kernel.

![](bbox=[0.15, 0.15, 0.77, 0.6])