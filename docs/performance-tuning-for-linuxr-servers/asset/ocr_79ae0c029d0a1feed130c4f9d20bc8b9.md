performance boost, simply disable access time updates with the mount option noatime.

# Tuning ReiserFS

reiserfstune tunes the ReiserFS file system. reiserfstune changes the journal size and maximum transaction size. The journal's location can also be changed:

```
-j | --journal-device *FILE*
```

*FILE* specifies the name of the block device where the file system places the journal.

```
-o | journal-offset *N*
```

*N* specifies the offset where the journal starts when it is on a separate block device. The default is 0.

```
--no-journal-available
```

This allows the file system to continue when the current journal's block device is no longer available by having a disk that has gone bad.

```
--journal-new-device *FILE*
```

*FILE* is the name of the block device that will contain the new journal for the file system.

```
-s | journal-size *N*
```

*N* specifies the journal in blocks. When the journal is on a separate block device, the default size is the number of blocks on that device. When the journal is not on a separate block device, the default is 8193 and the maximum is 32749. The minimum is 513 blocks for both cases.

```
-t | --transaction-max-size *N*
```

*N* is the journal's maximum transaction size. The default and maximum is 1024 blocks.