
## -root dir

Moves all files and directories into dir in the image. This is essentially the same as using -graft-points and adding dir in front of every pathspec, but is easier to use. dir may actually be several levels deep. It is created with the same permissions as other graft points.

## -old-root dir

This option is necessary when writing a multisession image and the previous (or even older) session was written with -root dir. Using a directory name not found in the previous session causes genisoimage to abort with an error. Without this option, genisoimage would not be able to find unmodified files and would be forced to write their data into the image once more. -root and -old-root are meant to be used together to do incremental backups. The initial session would e.g. use: genisoimage -root backup_1 dirs. The next incremental backup with genisoimage -root backup_2 -old-root backup_1 dirs would take another snapshot of these directories. The first snapshot would be found in backup_1, the second one in backup_2, but only modified or new files need to be written into the second session. Without these options, new files would be added and old ones would be preserved. But old ones would be overwritten if the file was modified. Recovering the files by copying the whole directory back from CD would also restore files that were deleted intentionally. Accessing several older versions of a file requires support by the operating system to choose which sessions are to be mounted.

## -s sector type
## -sectype sector type

Set output sector type to e.g. data/xa1/raw.

## -sort sort_file

Sort file locations on the media. Sorting is controlled by a file that contains pairs of filenames and sorting offset weighting. If the weighting is higher, the file will be located closer to the beginning of the media, if the weighting is lower, the file will be located closer to the end of the media. There must be only one space or tabs character between the filename and the weight and the weight must be the last characters on a line. The filename is taken to include all the characters up to, but not including the last space or tab character on a line. This is to allow for space characters to be in, or at the end of a filename. This option does not sort the order of the filenames that appear in the ISO9660 directory. It sorts the order in which the file data is written to the CD image, which is useful in order to optimize the data layout on a CD. See README.sort for more details.

## -sparc-boot img_sun4,img_sun4c,img_sun4m,img_sun4d,img_sun4e

See -B above.

## -sparc-label label

Set the Sun disk label name for the Sun disk label that is created with -sparc-boot.

## -split-output

Split the output image into several files of approximately 1 GB each. This helps to create DVD-sized ISO9660 images on operating systems without large file support. wodim will concatenate more than one file into a single track if writing to a DVD. To make -split-output work, -o filename must be specified. The resulting output images will be named: *filename_00, filename_01, filename_02...*.

## -stream-media-size #

Select streaming operation and set the media size to # sectors. This allows you to pipe the output of the (1) program into **genisoimage** and to create an ISO9660 filesystem without the need of an intermediate tar archive file. If this option has been specified, **genisoimage** reads from *stdin* and creates a file with the name STREAM.IMG. The maximum size of the file (with padding) is 200 sectors less than the specified media size. If - **no-pad** has been specified, the file size is 50 sectors less than the specified media size. If the file is smaller, **genisoimage** will write padding. This may take awhile.

The option *-stream-media-size* creates simple ISO9660 filesystems only and may not used together with multisession or hybrid filesystem options.

## -stream-file-name *name*

Reserved for future use.

## -sunx86-boot *UFS_img*... *AUX1_img*

Specifies a comma-separated list of filesystem images that are needed to make a bootable CD for Solaris x86 systems.

Note that partition 1 is used for the ISO9660 image and that partition 2 is the whole disk, so partition 1 and 2 may not be used by external partition data. The first image file is mapped to partition 0. There may be empty fields in the comma-separated list, and list entries for partition 1 and 2 must be empty. The maximum number of supported partitions is 8 (although the Solaris x86 partition table could support up to 16 partitions), so it is impossible to specify more than 6 partition images. This option is required to make a bootable CD for Solaris x86 systems.

If *-sunx86-boot* has been specified, the first sector of the resulting image will contain a PC fdisk label with a Solaris type 0x82 fdisk partition that starts at offset 512 and spans the whole CD. In addition, for the Solaris type 0x82 fdisk partition, there is a SVr4 disk label at offset 1024 in the first sector of the CD. This disk label specifies slice 0 for the first (usually UFS type) filesystem image that is used to boot the PC and slice 1 for the ISO9660 image. Slice 2 spans the whole CD slice 3 ... slice 7 may be used for additional filesystem images that have been specified with this option.

A Solaris x86 boot CD uses a 1024 byte sized primary boot that uses the **El-Torito** **no-emulation** boot mode and a secondary generic boot that is in CD sectors 1...15. For this reason, both *-b bootimage -no-emul-boot* and *-G genboot* must be specified.

## -sunx86-label *label*

Set the SVr4 disk label name for the SVr4 disk label that is created with *-sunx86-boot*.

## -sysid *ID*

Specifies the system ID. There is space for 32 characters. Equivalent to *SYS1* in the *.genisoimagerc* file.

## -T
## -translation-table

Generate a file TRANS.TBL in each directory on the CD-ROM, which can be used on non-Rock Ridge-capable systems to help establish the correct filenames. There is also information present in the file that indicates the major and minor numbers for block and character devices, and each symlink has the name of the link file given.

## -table-name table_name

Alternative translation table filename (see above). Implies -T. If you are creating a multi-session image you must use the same name as in the previous session.

## -ucs-level level

Set Unicode conformance level in the Joliet SVD. The default level is 3. It may be set to 1..3 using this option.

## -udf

Include UDF filesystem support in the generated filesystem image. UDF support is currently in alpha status and for this reason, it is not possible to create UDF-only images. UDF data structures are currently coupled to the Joliet structures, so there are many pitfalls with the current implementation. There is no UID/GID support, there is no POSIX permission support, and there is no support for symlinks. Note that UDF wastes the space from sector ~20 to sector 256 at the beginning of the disc in addition to the space needed for real UDF data structures.

## -uid uid

Overrides the uid read from the source files to the value of uid. Specifying this option automatically enables Rock Ridge extensions.

## -use-fileversion

The option **-use-fileversion** allows **genisoimage** to use file version numbers from the filesystem. If the option is not specified, **genisoimage** creates a version number of 1 for all files. File versions are strings in the range `;1` to `;32767`. This option is the default on VMS.

## -U
## -untranslated-filenames

Allows "untranslated" filenames, completely violating the ISO9660 standards described above. Enables the following flags: **-d -l -N -allow-leading-dots -relaxed-filenames -allow-lowercase -allow-multidot -no-iso-translate**. Allows more than one `:` character in the filename, as well as mixed-case filenames. This is useful on HP-UX, where the built-in `cdfs` filesystem does not recognize any extensions. Use with extreme caution.

## -no-iso-translate

Do not translate the characters `#` and `~` which are invalid for ISO9660 filenames. Although invalid, these characters are often used by Microsoft systems. This violates the ISO9660 standard, but it happens to work on many systems. Use with caution.

## -V volid

Specifies the volume ID (volume name or label) to be written into the master block. There is space for 32 characters. Equivalent to **VOLI** in the `.genisoimagerc` file. The volume ID is used as the mount point by the Solaris volume manager and as a label assigned to a disc on various other platforms such as Windows and Apple Mac OS.

## -volset ID

Specifies the volume set ID. There is space for 128 characters. Equivalent to **VOLS** in the `.genisoimagerc` file.
