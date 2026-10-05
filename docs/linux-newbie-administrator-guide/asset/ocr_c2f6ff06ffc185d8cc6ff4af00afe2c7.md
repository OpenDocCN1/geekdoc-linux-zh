# 4.2.10 Can I set 32-bit hard drive I/O?

I know nothing about harddrives, but saw a review of RedHat 6.0 by Edward Choh (http://hardwarezone.community.com.sg/main.htm), in which he gave some interesting tips, including setting up the 32-bit input/output (I/O) and direct memory access (DMA). I tried, and it worked fine for me. Be warned that it can possibly harm the content of your harddrive so do not do it if you are a real PC newbie, don't feel geeky today, or have a weak heart–I can't guarantee it will work for you.

The turning on of the 32-bit I/O and DMA has to be done by, and I did it in a single-user mode (to minimize the damage to the file system if something went wrong and I had to reboot). I definitely would not do it in a system currently running many programs or X-windows, and would have a current backup of any precious data.

To boot your computer in a single-user mode, I type this at the lilo prompt (during bootup):

```
linux single
```

Say I would enable the 32-bit I/O on my first IDE harddrive, which is "hda". First, I time the harddrive current performance, and note the score:

```
hdparm -t /dev/hda
```

Now, I display my current I/O and DMA settings:

```
hdparm -c /dev/hda
```

[my system showed 0, meaning that the 32-bit I/O is turned off and the default 16-bit access is used]

```
hdparm -d /dev/hda
```

[my system showed 0 again, meaning that the harddrive DMA access is turned off].

Now, I turn on the 32 bit I/O and DMA:

```
hdparm -c 1 /dev/hda
hdparm -d 1 /dev/hda
```

Now, I can time the performance of the harddrive again to compare the score with the original one:

```
hdparm -t /dev/hda
```

If everything worked ok, and the performance has improved, I can "commit" the new settings, so they can survive a soft reset:

```
hdparm -k 1 /dev/hda
```