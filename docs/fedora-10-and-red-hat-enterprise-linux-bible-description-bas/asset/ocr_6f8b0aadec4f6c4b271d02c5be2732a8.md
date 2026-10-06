# Chapter 13: Backing Up and Restoring Files 565

```
}

# Note that, although the keyword below is infofile, it is
# only so for historic reasons, since now it is supposed to
# be a directory (unless you have selected some database
# format other than the 'text' default)

infile "/var/lib/amanda/normal/curinfo" # database DIRECTORY
logdir "/var/lib/amanda/normal" # log directory
indexdir "/var/lib/amanda/normal/index" # index directory

# tapypes

# Define the type of tape you use here, and use it in "tapetype"
# above. Some typical types of tapes are included here.
# tapetype amanda how many MB will fit on the tape, how
# big the filemarks are, and how fast the tape device.

tapetype HF-DAT {
  comment "DAT drives"
  # data provided by Rob Browning <rlb@cs.texas.edu>
  length 1930 mbytes
  filemarker 111 kbytes
  speed 468 kbytes
}

# dumptypes
# These are referred to by the disklist file.

dumpt global {
  comment "Global definitions"
# This is quite useful for setting global parameters, so you
# don't have to type them everywhere.
}

dumpt always-full {
  global
  comment "Full dump of this filesystem always"
  compress none
  priority high
  dumpcycle 0
}
```

This example amanda.conf file was trimmed down from a larger example I copied from the
/etc/amanda/DailySet1 The example amanda.conf provides additional information on the available configuration options. Also, the online man page for Amanda should be helpful (type man amanda to read it). You can find more instructions in the
/usr/share/doc/amanda-server/ directory. Generally, you have to do the following: