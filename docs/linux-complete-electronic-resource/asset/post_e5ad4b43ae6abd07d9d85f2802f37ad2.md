
an uppercase letter, the action applies to all files, and you won’t be prompted again.
You may also choose actions (for all files) on the command line, when invoking mtools:

-   -o    Overwrites primary names by default.
-   -O    Overwrites secondary names by default.
-   -r    Renames primary name by default.
-   -R    Renames secondary name by default.
-   -a    Autorenames primary name by default.
-   -A    Autorenames secondary name by default.
-   -s    Skip primary name by default.
-   -S    Skip secondary name by default.
-   -m    Ask user what to do with primary name.
-   -M    Ask user what to do with secondary name.

By default, the user is prompted if the primary name clashes, and the secondary name is auto-renamed.
If a name clash occurs in a Unix directory, mtools only asks whether to overwrite the file, or to skip it.

## CASE SENSITIVITY OF THE VFAT FILESYSTEM

The VFAT filesystem is able to remember the case of the filenames. However, filenames which differ only in case are not allowed to coexist in the same directory. For example if you store a file called LongFileName on a VFAT filesystem, mdir shows this file as LongFileName, and not as Longfilename. However, if you then try to add LongFilename to the same directory, it is refused, because case is ignored for clash checks.

The VFAT filesystem allows you to store the case of a filename in the attribute byte, if all letters of the filename are the same case, and if all letters of the extension are the same case too. Mtools uses this information when displaying the files, and also to generate the Unix filename when copying to a Unix directory. This may have unexpected results when applied to files written using an pre-7 version of DOS: Indeed, the old style filenames map to all uppercase. This is different from the behavior of the old version of mtools which used to generate lowercase Unix filenames.

## HIGH CAPACITY FORMATS

Mtools supports a number of formats which allow you to store more data on disk than usual. Due to different operating system abilities, these formats are not supported on all OSes. Mtools recognizes these formats transparently where supported. In order to format these disks, you need to use an operating-system-specific tool. For Linux, suitable floppy tools can be found in the fdutils package at the following locations:

ftp://linux.wauuuog.org/pub/knaff/fdutils/
ftp://tsx-11.mit.edu/pub/linux/sources/sbin/fdutils*
ftp://sunsite.unc.edu/pub/linux/system/Misc/fdutils-*

See the manpages included in that package for further details: Use superformat to format all formats except XDF, and use xdfcopy to format XDF.

### More sectors

The oldest method of fitting more data on a disk is to use more sectors and more tracks. Although the standard format uses 80 tracks and 18 sectors (on a 3 1/2 inch high-density disk), it is possible to use up to 83 tracks (on most drives) and up to 21 sectors. This method allows to store up to 1743K on a 3 1/2 HD disk. However, 21 sector disks are twice as slow as the standard 18 sector disks because the sectors are packed so close together that we need to interleave them. This problem doesn't exist for 20 sector formats.

These formats are supported by numerous DOS shareware utilities such as idformat and vgcoppy. In his infinite hubris, Bill Gates believed that he invented this, and called it "DMF disks," or "Windows formatted disks." But in reality, it had already existed years before! Mtools supports these formats on Linux, on SunOS and on the Dell Unix PC.

### Bigger sectors

By using bigger sectors it is possible to go beyond the capacity which can be obtained by the standard 512-byte sectors. This is because of the sector header. The sector header has the same size, regardless of how many data bytes are in the sector. Thus, we save some space by using fewer, but bigger sectors. For example, 1 sector of 4K only takes up header space once, whereas 8 sectors of 512 bytes have also 8 headers, for the same amount of useful data.

This method allows you to store up to 1992K on a 3 1/2 HD disk. Mtools supports these formats only on Linux.

### 2m

The 2m format was originally invented by Ciriaco Garcia de Celis. It also uses bigger sectors than usual in order to fit more data on the disk.

However, it uses the standard format (18 sectors of 512 bytes each) on the first cylinder, in order to make these disks easier to handle by DOS. Indeed this method allows a standard sized bootsector, which contains a description of how the rest of the disk should be read.

However, the drawback of this is that the first cylinder can hold less data than the others. Unfortunately, DOS can only handle disks where each track contains the same amount of data. Thus 2m hides the fact that the first track contains less data by using a *shadow FAT*. (DOS usually stores the FAT in two identical copies, for additional safety. XDF stores only one copy, and it tells DOS that it stores two. Thus the space that would be taken up by the second FAT copy is saved.) This also means that you should *never use a 2m disk to store anything else than a DOS fs*.

Mtools supports these formats only on Linux.

## XDF

XDF is a high capacity format used by OS/2. It can hold 1840K per disk. That’s lower than the best 2m formats, but its main advantage is that it is fast: 600 milliseconds per track. That’s faster than the 21 sector format, and almost as fast as the standard 18 sector format. In order to access these disks, make sure mtools has been compiled with XDF support, and set the *use_xdf* variable for the drive in the configuration file. See section “Compiling mtools and misc variables,” for details on how to do this. Fast XDF access is only available for Linux kernels more recent than 1.1.34.

Mtools supports this format only on Linux.

## WARNING

![](img/a3584dae761d2e3abed8bf40d7637389_758_0.png)

Caution / Attention distributors: If mtools is compiled on a Linux kernel more recent than 1.3.34, it won’t run on an older kernel. However, if it has been compiled on an older kernel, it still runs on a newer kernel, except that XDF access is slower. It is recommended that distribution authors only include mtools binaries compiled on kernels older than 1.3.34 until 2 comes out. When 2 is out, mtools binaries compiled on newer kernels may (and should) be distributed. Mtools binaries compiled on kernels older than 1.3.34 won’t run on any 2.x kernel or later.

## EXIT CODES

All the Mtools commands return 0 on success, 1 on utter failure, or 2 on partial failure. All the Mtools commands perform a few sanity checks before going ahead, to make sure that the disk is indeed an MS-DOS disk (as opposed to, say, an ext2 or minix disk).

These checks may reject partially corrupted disks, which might otherwise still be readable. To avoid these checks, set the MTOOLS_SKIP_CHECK environmental variable or the corresponding configuration file variable (see section “Global Variables”).

## BUGS

An unfortunate side effect of not guessing the proper device (when multiple disk capacities are supported) is an occasional error message from the device driver. These can be safely ignored.

The FAT checking code chokes on 1.72 MB disks formatted with pre-2.0.7 mttools. Set the environmental variable MTOOLS_FAT_COMPATIBILITY (or the corresponding configuration file variable, global variables) to bypass the FAT checking.

## HOW TO CONFIGURE MTOOLS FOR YOUR ENVIRONMENT

### DESCRIPTION

This sections explains the syntax of the configurations files for mttools. The configuration files are called /usr/local/etc/mtools.conf and “~/”.mttoolsrc. If the environmental variable MTOOLSRC is set, its contents are used as the filename for a third configuration file. These configuration files describe the following items:

-   Global configuration flags and variables
-   Per drive flags and variables
-   Character translation tables

### LOCATION OF THE CONFIGURATION FILES

/usr/local/etc/mtools.conf is the system-wide configuration file, and “~/”.mttoolsrc is the user’s private configuration file.

On some systems, the system-wide configuration file is called /etc/defaults/mtools.conf instead.

### GENERAL CONFIGURATION FILE SYNTAX

The configuration file is made up of sections. Each section starts with a keyword identifying the section followed by a colon. Then follow variable assignments and flags. Variable assignments take the following form: name=value

Flags are lone keywords without an equal sign and value following them. A section either ends at the end of the file or where the next section begins.
