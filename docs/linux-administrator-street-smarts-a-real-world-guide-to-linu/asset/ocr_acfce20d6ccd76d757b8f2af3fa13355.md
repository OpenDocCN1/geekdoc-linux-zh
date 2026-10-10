# ## Creating New Partitions

Now that the disk is cleared of its existing partitions, you can create new ones and save your changes. You can begin by creating a new Linux data partition. Make it somewhat smaller than the available disk space—say, 80MB on the 100MB Zip disk:

```
```
Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-1024, default 1): 1
Last cylinder or +size or +sizeM or +sizeK (1-1024, default 1024): +80M
```
```

With the first partition created, it’s time to create the second one, for swap space. You could do this by creating a second primary partition; however, so you can see how it’s done, try first creating an extended partition and then creating a logical partition within it:

```
```
Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)
e
Partition number (1-4): 2
First cylinder (816-1024, default 816):
Using default value 816
Last cylinder or +size or +sizeM or +sizeK (816-1024, default 1024):
Using default value 1024
```
```

```
```
Command (m for help): n
Command action
  l   logical (5 or over)
  p   primary partition (1-4)
l
First cylinder (816-1024, default 816):
Using default value 816
Last cylinder or +size or +sizeM or +sizeK (816-1024, default 1024): 1024
```
```

At this point, your partitions exist but the Linux swap partition has a type code of 0x83 (hexadecimal 83, or decimal 131), which denotes a Linux filesystem partition. To avoid confusion, you should set the partition type of 0x82, which denotes a Linux swap partition:

```
```
Command (m for help): t
```
```