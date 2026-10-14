# amanda.conf

The best way to create amanda.conf is to copy an example and modify it to suit your needs. When you configure Amanda, you'll get an example amanda.conf in the source code's example subdirectory. Make a copy of this file, edit the copy, skip the first section, and go down to the part that reads as follows:

```
runtapes 1      # number of tapes to be used in a single run of amdump
tpchanger "chg-manual"  # the tape-changer glue script
tapedev "/dev/null"    # the no-rewind tape device to be used
rawtapedev "/dev/null"  # the raw device to be used (ftape only)
changerfile "/usr/adm/amanda/DailySet1/changer"
changerfile "/usr/adm/amanda/DailySet1/changer-status"
changerfile "/usr/local/amanda/amanda..."
changerdev "/dev/null"
```

Here you'll need to make some changes. First change the /dev/null for tapedev to your tape device. This should be, as the comment suggests, the no-rewind tape device. The line that mentions ftape may not apply; newer versions of the ftape driver should provide full file-marker emulation. Comment all of the changer lines out—these are for tape changers; even if you have one, it's easier to start with a simple configuration.

The next line in the file is this:

```
tapetype HP-DAT      # what kind of tape it is (see tapetypes below)
```

Unless you're using an HP DAT drive, change this line. The list of tape types appears later in the file, with definitions like this:

```
define tapetype HP-DAT {
  comment "DAT tape drives"
  # data provided by Rob Browning
  length 1930 mbytes
  filemark 111 kbytes
  speed 468 kbytes
}
```

Make sure you change these specifications accordingly. If you can't find the specifications in your tape drive's manual, try the extensive tapetype reference available from the Amanda Web site.