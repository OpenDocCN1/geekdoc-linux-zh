
This parameter specifies if we want to record SSID beacon frames. Most networks by default, spew these out at a fairly high rate, so it might save some disk space if you don’t want them. Setting *beaconlog* to false would be a good idea on a headless monitoring system or an automated system with limited storage space.

```
# Do we log PHY layer packets or do we filter them out of the dumpfile
phylog=true
```

Logging PHY layer packets is usually a good idea for troubleshooting purposes. Set to false if you don’t want to.

```
# Do we mangle packets if we can decrypt them or if they’re fuzzy-detected
mangledatalog=true
```

If we receive a damaged packet and we can mangle it into being correct, should we decrypt it? Normally this is a good idea, but packets decoded this way may not be 100 percent correct, but can be useful for troubleshooting.

```
# Do we do “fuzzy” crypt detection? (byte-based detection instead of 802.11
# frame headers)
# valid option: Comma seperated list of card types to perform fuzzy detection
# on, or ‘all’
fuzzycrypt=wtapfile,wlanng,wlanng_legacy,wlanng_avs,hostap,wlanng_wext,
ipw2200,ipw2915
```

Sometimes it may be necessary to detect packets for encryption based on their size, rather than what the packet flags say. This depends a lot on the card type, as some drivers add extra information. Comment out the *fuzzycrypt=* line if you need or want to trust the frames to report their encryption status, rather than actually checking the bytes in the packet.

```
# Do we do forgiving fuzzy packet decoding? This lets us handle borked drivers
# which don’t indicate they’re including FCS, and then do.
# fuzzycode=wtapfile,radiotap_bsd_a,radiotap_bsd_g,radiotap_bsd_bg,radiotap_bsd_b,
# pcapfile
```

Some drivers are better than others for claiming one set of capabilities and reporting another. As above, if you want to double check packets and make sure all is as is being reported, enable this option.

```
# Do we use network-classifier fuzzy-crypt detection? This means we expect
# packets that are associated with an encrypted network to be encrypted too,
# and we process them by the same fuzzy compare.
# This essentially replaces the fuzzycrypt per-source option.
netfuzzycrypt=true
```

This parameter overrides the *fuzzycrypt* parameter and basically assumes that if a network is encrypted, any associated clients must be encrypted too.

```
# What type of dump do we generate?
# valid option: "wiretap"
dumptype=wiretap
```

At this point, Kismet will only generate wiretap dump files. In the future, more options may be available, but for now, just leave it at wiretap.

```
# Do we limit the size of dump logs? Sometimes ethereal can't handle big ones.
# 0 = No limit
# Anything else = Max number of packets to log to a single file before closing
# and opening a new one.
dumplimit=0
```

Sometimes you may want to limit the size of your dump files. Maybe you have limited storage or want to make things more manageable for storage. A setting of 0 is the default and has no size limit. Anything else is the number of packets to record before closing the file and starting a new one.

```
# Do we write data packets to a FIFO for an external data-IDS (such as Snort)?
# See the docs before enabling this.
#fifo=/tmp/kismet_dump
```

This setting allows you to pipe the data out a First In, First Out (FIFO) pipe to share real time information with other programs that can read from a file. This requires that the program connect to the FIFO pipe before Kismet will start. The *fifo=* setting specifies the location of the FIFO pipe. The third-party programs need to have access to where the FIFO pipe is, so make sure that if your program is running as a normal user and that you don’t have the FIFO pipe in a root-only directory.

```
# Default log title
logdefault=Kismet
```

The log file output filename can be tweaked to your hearts content. Kismet by default has a name structure of “Kismet” – “Month – Date – Year” and the number of file in the sequence (i.e., Kismet-Sep-26-2006-1.gps). The *logdefault* parameter starts the file name specifying “Kismet” by default. If you want a different start to the filename, just change it here (no spaces).

```
# logtemplate - Filename logging template.
# This is, at first glance, really nasty and ugly, but you'll hardly ever
# have to touch it so don't complain too much.
#
# $n is replaced by the logging instance name
# $d is replaced by the current date as Mon-DD-YYYY
# $D is replaced by the current date as YYYYMMDD
# $t is replaced by the starting log time
# $i is replaced by the increment log in the case of multiple logs
# $l is replaced by the log type (dump, status, crypt, etc)
# $h is replaced by the home directory
# ie, "netlogs/$n-$d-$i.dump" called with a logging name of "Pok" could expand
# to something like "netlogs/Pok-Dec-20-01-1.dump" for the first instance and
# "netlogs/Pok-Dec-20-01-2.$1" for the second logfile generated.
# $h/netlogs/$n-$d-$i.dump could expand to
# /home/foo/netlogs/Pok-Dec-20-01-2.dump
#
# Other possibilities: Sorting by directory
# logtemplate=$l/$n-$d-$i
# Would expand to, for example,
# dump/Pok-Dec-20-01-1
# crypt/Pok-Dec-20-01-1
# and so on. The "dump", "crypt", etc, dirs must exist before kismet is run
# in this case.
logtemplate=$n-$d-$i.$l
```

As the comments for the log template say, it looks scary, but it isn't. Using the listed `$` variables, you can change the order and even the whole filename of the log files. Specifying the `$l/` variable at the beginning will split the log files into separate log files, based on the type of file (dump/ crypt/ and so forth).

The possibilities are endless, so adjust to your needs. The default of logtemplate=$n-$d-$i.$l is replaced with Kismet, $d is replaced with the date, $i is replaced with the log increment, and $l is the file type, in this case it is also used as an extension.

```
# Where do we store the pid file of the server?
piddir=/var/run/
```

The pid file of the server when it's running. There should be no reason to change this unless you are running an odd UNIX variant and need to specify something else.

```
# Where state info, etc, is stored. You shouldn't ever need to change this.
# This is a directory.
confdir=$h/.kismet/
```

This setting is where Kismet stores its state info. This directory is usually in the home directory of your `SUID` user. There shouldn't be a need to change this at all.

```
# cloaked SSID file. You shouldn't ever need to change this.
ssidmap=ssid_map
```

The `ssidmap=` parameter specifies the file that Kismet should use to keep a tab on what BSSID matches each SSID. This is usually stored within the directory specified in the `confdir` parameter. If you discover the BSSID from a cloaked network and you have previously determined the SSID, this will fill in the blank automatically from this file. You shouldn't need to change this parameter unless you are running on a weird distribution without home directories.

```
# Group map file. You shouldn't ever need to change this.
groupmap=group_map
```

The `groupmap=` parameter specifies the file that Kismet should use to keep a running list of network groups as specified by the user. This is usually stored within the directory specified in the `confdir` parameter. You shouldn't need to change this parameter.

```
# IP range map file. You shouldn't ever need to change this.
ipmap=ip_map
```

The `ipmap=` parameter specifies the file that Kismet should use to keep a tab on what networks are using what IP range. This is usually stored within the directory specified in the `confdir` parameter. This file holds the previously detected mappings of networks and their IP spaces to help fill in the blanks. You shouldn't need to change this parameter.

## Kismet Server Command Line

The Kismet server, in addition to the config file, can be controlled at start by command-line switches. Previously this was how all parameters were set on early versions of Kismet, but the config file became necessary when so many options were added. There are times, however, that you want to change a parameter for that one run of the server, and many are still available as command-line switches.

These options override the settings in the config file, and require that the server be launched separate from the client. You can't use the Kismet command/script to start the server and client, you will need to start the `kismet_server` and `kismet_client` separately:
