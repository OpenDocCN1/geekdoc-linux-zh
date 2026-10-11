As a general rule, I favor drives with hardware compression. Using hardware compression removes some computing burden from the host computer and can often speed up backups. When necessary, you can disable compression using jumpers or the Linux ntu command, described in the section “Using mt to Control a Tape Drive.” One of the prime advantages of hardware compression, though, relates to Linux backup software. Some Linux backup programs, such as tar with its gzip compression, use compression algorithms that render all the data after an error unreadable. This flaw makes using software compression a risky prospect. If you decide to buy a drive that relies upon software compression, you should definitely look into more sophisticated backup programs than tar, or use it without compression, in order to avoid these problems.

# ## Estimating Your Space Requirements

Whether or not you use compression, it’s important to know how large a tape drive you need to get. As a general rule, it’s best to buy a tape drive with enough capacity to hold all your data on a single tape (or a single set of tapes, in the case of a changer). If you’re backing up a single desktop computer, finding your capacity requirements is relatively straightforward: you can use the Linux df command to find how much space your files consume. For instance

```
$ df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda6 | 2679650 | 1449936 | 1118867 | 56% | / |
| /dev/sda8 | 676435 | 202258 | 439238 | 32% | /usr/local |
| /dev/sda5 | 5135482 | 2879989 | 2255493 | 56% | /home |
| /dev/sda3 | 31077 | 11530 | 18906 | 38% | /boot |


The *Used* column indicates the space consumed by files (in bytes) on each partition. In the preceding example, the system’s files consume 4.3GB. What’s more, the total capacity of the computer’s disk is 8.1GB, so files could conceivably expand to fill that much space.

In theory, a 2GB uncompressed capacity drive might be able to back up the entire hard disk. I recommend, however, buying a drive with enough capacity to handle your entire hard disk’s filled capacity, preferably without compression. The reason is simple—expansion. As you install more software and generate new data files, your needs for backup capacity will expand. A tape drive that’s barely adequate today will become inadequate tomorrow. Upgrading to a higher-capacity tape format can be expensive, because either the drives or the tapes will cost a fair amount of money. If you buy a drive with capacity to spare, you won’t need to upgrade it or resort to multi-tape backups for some time to come. In practice, though, to back up the preceding hard drive, I would recommend a drive with an 8–10GB uncompressed capacity. That drive will be adequate for the present and probably for at least another year or two.

If your system dual boots between Linux and one or more other OSs, you can modify this rule to one of purchasing a drive that’s adequate to back up any one OS. For instance, if 5GB were