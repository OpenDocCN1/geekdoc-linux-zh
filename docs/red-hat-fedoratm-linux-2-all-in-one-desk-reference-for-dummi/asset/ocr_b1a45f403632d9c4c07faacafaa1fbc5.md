# ## 450  Backing Up and Restoring Files

![](bbox=[0.16, 0.12, 0.23, 0.19])

Use the `du -s` command to determine the amount of storage you need for archiving a directory. For example, here's how you can get the total size of the `/etc` directory in kilobytes:

```
```
du -s /etc
35724 /etc
```
```

The resulting output shows that the `/etc` directory requires at least 35,724K of storage space to back up.

# ### Backing up on tapes

Although backing up on tapes is as simple as using the right device name in the `tar` command, you do have to know some nuances of the tape device to use it well. When you use `tar` to back up to the device named `/dev/st0` (the first SCSI tape drive), the tape device automatically rewinds the tape after the `tar` program finishes copying the archive to the tape. The `/dev/st0` device is called a rewinding tape device because it rewinds tapes by default.

If your tape can hold several gigabytes of data, you may want to write several `tar` archives — one after another — to the same tape (otherwise much of the tape may be left empty). If you plan to do so, your tape device can't rewind the tape after the `tar` program finishes. To help you with scenarios like this one, several Linux tape devices are nonrewinding. The nonrewinding SCSI tape device is called `/dev/nst0`. Use this device name if you want to write one archive after another on a tape.

![](bbox=[0.16, 0.59, 0.23, 0.66])

After each archive, the nonrewinding tape device writes an *end-of-file* (EOF) marker to separate one archive from the next. Use the `mt` command to control the tape — you can move from one marker to the next or rewind the tape. For example, after you finish writing several archives to a tape using the `/dev/nst0` device name, you can force the tape to rewind with the following command:

```
```
mt -f /dev/nst0 rewind
```
```

After rewinding the tape, you can use the following command to extract files from the first archive to the current disk directory:

```
```
tar xvf /dev/nst0
```
```

After that, you must move past the EOF marker to the next archive. To do so, use the following `mt` command:

```
```
mt -f /dev/nst0 fsf 1
```
```

This positions the tape at the beginning of the next archive. Now use the `tar xvf` command again to read this archive.