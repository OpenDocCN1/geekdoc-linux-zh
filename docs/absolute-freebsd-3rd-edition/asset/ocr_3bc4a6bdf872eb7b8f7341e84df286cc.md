This disk partition is conveniently available as `/dev/gptid/075e7b89-30ed-11e7-a386-002590dbd594` (1). Much like disk serial numbers, GUIDs are integral to the partition. You can move the disk to another host and still get the same GPT ID. By using the GPT ID label in configurations like `/etc/fstab`, you guarantee that FreeBSD uses this particular partition, rather than partition 1, on whatever device happens to get assigned ada0 at system boot.

Using a GPT ID label makes sense when you have many automatically configured disks, such as large storage arrays. On smaller systems, though, the 128-bit GUID is annoyingly long. If you decide not to use these labels, remove them from your system by setting the tunable `kern.geom.label.gptid.enable` to 0 in `/boot/loader.conf`.

For most hosts, I recommend assigning GPT labels.

# ## GPT Labels

GPT partitions let you manually assign a label name within the partition table. I highly recommend doing so whenever possible. Here's a partition that I assigned a name:

```
Geom name: ada2p1
Providers:
(1) 1. Name: gpt/swap2
  -snip-
```

I've assigned the label `swap2` (1) to partition 1 on disk ada2. This label is physically stored on the disk partition. I can use this label in my configurations just like any other device name. Using manually assigned labels is much more manageable for small systems, as this `/etc/fstab` shows:

```
/dev/gpt/swap2 none swap sw 0 0
```

An assigned label is much more human-friendly than a long serial number or GUID. If you have the choice, I encourage you to label GPT partitions. We'll assign labels when we partition disks.

# ## GEOM Labels