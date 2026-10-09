Although this message is normal if you have not yet used `nftl_format` on the DOC device, it is a sign that an error occurred if you already used `nftl_format` on the DOC. There are many reasons why you may encounter these messages. None of them is your fault if you have followed the instructions here, as well as those in Chapter 9. Whenever you encounter such a message, review your manipulations and make sure you have faithfully followed the steps in the discussion. If it is not a manipulation error, you can choose to dig deeper and use your hacking skills to figure out the problem on your own. It is often a good idea to consult the MTD mailing list and search its archive, because others may have encountered a similar problem and already solved it. When sending a message to the MTD mailing list (or any other mailing list, for that matter), try to be as verbose as possible. It is very frustrating for mailing list subscribers to receive pleas for help that have little or no detail. Specifically, provide the versions of all the software components involved, explain the exact steps you followed, and provide the output of all the tools you used.

# ### Partitioning

With the DOC device formatted for NFTL, you can now partition the device using *fdisk*. Here is the transcript of an *fdisk* session in which I created one partition on my NFTL device:

```
# fdisk /dev/nftla
Device contains neither a valid DOS partition table, nor Sun or S...
Building a new DOS disklabel.  Changes will remain in memory only,
until you decide to write them.  After that, of course, the previous
content won't be recoverable.
```

```
Command (m for help): p


Disk /dev/nftla: 16 heads, 4 sectors, 1018 cylinders
Units = cylinders of 64 * 512 bytes


   Device    Boot  Start  End  Blocks  Id System
```

```
Command (m for help): d
Partition number (1-4): **1**
```

```
Command (m for help): n
e	extended
p	primary partition (1-4)
p
Partition number (1-4): **1**
```

```
First cylinder (1-1018, default 1): _Using default value 1_
Last cylinder or +size or +sizeM or +sizeK (1-1018, default 1018): _Using default value 1018_
```

```
Command (m for help): p
```