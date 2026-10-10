**-volset-size #**
Sets the volume set size to #. The volume set size is the number of CDs that are in a CD volume set. A volume set is a collection of one or more volumes, on which a set of files is recorded. Volume Sets are not intended to be used to create a set numbered CDs that are part of e.g. a Operation System installation set of CDs. Volume Sets are rather used to record a big directory tree that would not fit on a single volume. Each volume of a Volume Set contains a description of all the directories and files that are recorded on the volumes where the sequence numbers are less than, or equal to, the assigned Volume Set Size of the current volume.
**genisoimage** currently does not support a **-volset-size** that is larger than 1.
The option **-volset-size** must be specified before **-volset-seqno** on each command line.

**-volset-seqno #**
Sets the volume set sequence number to #. The volume set sequence number is the index number of the current CD in a CD set. The option **-volset-size** must be specified before **-volset-seqno** on each command line.

**-v**
**	-verbose**
Verbose execution. If given twice on the command line, extra debug information will be printed.

**-x glob**
Identical to **-m glob**.

**-XA**
Generate XA directory attributes.

**-xa**
Generate rationalized XA directory attributes.

**-z**
**-transparent-compression**
Generate special *RRIP* records for transparently compressed files. This is only of use and interest for hosts that support transparent decompression, such as Linux 2.4.14 or later. You must specify **-R** or **-r** to enable Rock Ridge, and generate compressed files using the *mkzftree* utility before running **genisoimage**. Note that transparent compression is a nonstandard Rock Ridge extension. The resulting disks are only transparently readable if used on Linux. On other operating systems you will need to call *mkzftree* by hand to decompress the files.