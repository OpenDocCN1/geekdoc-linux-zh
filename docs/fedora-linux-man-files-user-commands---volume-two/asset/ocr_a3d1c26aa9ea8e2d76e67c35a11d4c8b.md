# HFS MACINTOSH FILE FORMATS

Macintosh files have two parts called the Data and Resource fork. Either may be empty. Unix (and many other OSS) can only cope with files having one part (or fork). To add to this, Macintosh files have a number of attributes associated with them – probably the most important are the TYPE and CREATOR. Again, Unix has no concept of these types of attributes.

E.g., a Macintosh file may be a JPEG image where the image is stored in the Data fork and a desktop thumbnail stored in the Resource fork. It is usually the information in the data fork that is useful across platforms.

Therefore to store a Macintosh file on a Unix filesystem, a way has to be found to cope with the two forks and the extra attributes (which are referred to as the Finder info). Unfortunately, it seems that every software package that stores Macintosh files on Unix has chosen a completely different approach.

The Apple/Unix formats that genisoimage (partially) supports are:

+   *   CAP AUFS format
+       Data fork stored in a file. Resource fork in subdirectory .resource with same filename as data fork. Finder info in subdirectory .finderinfo with same filename.

+   *   AppleDouble/Netatalk
+       Data fork stored in a file. Resource fork stored in a file with same name prefixed with ‘%’. Finder info also stored in same ‘%’ file. Netatalk uses the same format, but the resource fork/Finder info stored in subdirectory .AppleDouble with same filename as data fork.

+   *   AppleSingle
+       Data structures similar to above, except both forks and Finder info are stored in one file.

+   *   Helios EtherShare
+       Data fork stored in a file. Resource fork and Finder info together in subdirectory .rsrc with same filename as data fork.

+   *   IPT UShare
+       Like the EtherShare format, but the Finder info is stored slightly differently.

+   *   MacBinary
+       Both forks and Finder info stored in one file.

+   *   Apple PC Exchange
+       Used by Macintoshes to store Apple files on DOS (FAT) disks. Data fork stored in a file. Resource fork in subdirectory resource.frk (or RESOURCE.FRK). Finder info as one record in file finder.dat (or FINDER.DAT). Separate finder.dat for each data fork directory.

Note: genisoimage needs to know the native FAT cluster size of the disk that the PC Exchange files are on (or have been copied from). This size is given by -cluster-size. The cluster or allocation size can be found by using the DOS utility chkdsk. May not work with PC Exchange v2.2 or higher files (available with MacOS 8.1).