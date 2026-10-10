OPERATIONS (CONT.)

| Use This Operation | To Do This |
|---|---|
| defblksize *n* | Set the block size to *n* bytes. This operation is for SCSI drives only. |
| defcompression *compression* | Set the default compression specified by *compression*. This operation is for SCSI drives only. |
| defdensity *n* | Set the density specified by *n*. This operation is for SCSI drives only. |
| defdrvbugger *n* | Set the drive buffer code specified by *n*. This operation is for SCSI drives only. |
| densities | Display some common density codes. |
| drvbuffer *n* | Set the tape drive buffer to the value specified by *n*. |
| eod, seed | Go to end of valid data. |
| erase | Erase the tape. |
| fsfm *n* | Go forward *n* files and position the tape on the last block of the previous file. |
| fsf *n* | Go forward *n* files and position the tape on the first block of the next file. |
| fsr *n* | Go forward *n* records. |
| fss *n* | Go forward *n* setmarks. This operation is for SCSI tapes only. |
| load | Load the tape. This operation is for SCSI drives only. |
| lock | Lock the tape drive door. This operation is for SCSI drives only. |
| mkpartition [ *size* ] | When used without an argument, formats the tape with one partition. When you specify a size in megabytes, formats the tape with two partitions and makes the second partition the specified size. |
| offline, rewofl | Rewind the tape and unload. |
| partseek *n* | Set the position to the *nth* block in the specified partition. |