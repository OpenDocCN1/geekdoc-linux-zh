joliet.

**-hide-joliet-trans-tbl**
Hide the TRANS.TBL files from the Joliet tree. These files usually don't make sense in the Joliet world as they list the real name and the ISO9660 name which may both be different from the Joliet name.

**-hide-rr-moved**
Rename the directory RR\_MOVED to .rr\_moved in the Rock Ridge tree. It seems to be impossible to completely hide the RR\_MOVED directory from the Rock Ridge tree. This option only makes the visible tree less confusing for people who don't know what this directory is for. If you need to have no RR\_MOVED directory at all, you should use -D. Note that if -D has been specified, the resulting filesystem is not ISO9660 level-1 compliant and will not be readable on MS-DOS. See also the NOTES section.

**-input-charset** *charset*
Input charset that defines the characters used in local filenames. To get a list of valid charset names, call genisoimage -input-charset help. To get a 1:1 mapping, you may use default as charset name. The default initial values are cp437 on DOS-based systems and iso8859-1 on all other systems. See the CHARACTER SETS section below for more details.

**-output-charset** *charset*
Output charset that defines the characters that will be used in Rock Ridge filenames. Defaults to the input charset. See CHARACTER SETS section below for more details.

**-iso-level** *level*
Set the ISO9660 conformance level. Valid numbers are 1 to 4.
With level 1, files may only consist of one section and filenames are restricted to 8.3 characters.
With level 2, files may only consist of one section.
With level 3, no restrictions (other than ISO-9660:1988) do apply.
With all ISO9660 levels from 1 to 3, all filenames are restricted to uppercase letters, numbers and underscores (\_.) Filenames are limited to 31 characters, directory nesting is limited to 8 levels, and pathnames are limited to 255 characters.
Level 4 officially does not exist but genisoimage maps it to ISO-9660:1999, which is ISO9660 version 2.
With level 4, an enhanced volume descriptor with version number and file structure version number set to 2 is emitted. Directory nesting is not limited to 8 levels, there is no need for a file to contain a dot and the dot has no special meaning, filenames do not have version numbers, and filenames can be up to 207 characters long, or 197 characters if Rock Ridge is used.
When creating Version 2 images, genisoimage emits an enhanced volume descriptor, similar but not identical to a primary volume descriptor. Be careful not to use broken software to make ISO9660 images bootable by assuming a second PVD copy and patching this putative PVD copy into an El Torito VD.