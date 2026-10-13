```
```text
tapetype SONY-AIT        # what kind of tape it is (see tapetypes below)
labelstr ^bcw[0-9]-$ # label constraint regex: all tapes must
#                         match
#
# Specify holding disks. These are used as a temporary staging area
# for dumps before they are written to tape and are recommended for
# most sites.
# The advantages include: tape drive is more likely to operate in
# streaming mode (which reduces tape and drive wear, reduces total
# dump time); multiple dumps can be done in parallel (which can
# dramatically # reduce total dump time.
# The main disadvantage is that dumps on the holding disk need to be
# flushed (with amflush) to tape after an operating system crash or
# a tape failure.
# If no holding disks are specified then all dumps will be written
# directly to tape. If a dump is too big to fit on the holding disk
# than it will be written directly to tape. If more than one
# holding disk is specified then they will all be used round-robin.
holdingdisk hd1 {
comment "main holding disk"
directory "/disk4"    # where the holding disk is
use 2 Gb              # how much space can we use on it
# a negative value mean:
#       use all space except that value
chunksize 1 Gb # size of chunk if you want big dump to be
# dumped on multiple files on holding disks
# N Kb/Mb/Gb split disks in chunks of size N
# 0 split disks in INT_MAX/1024 Kb chunks
# -1              same as -INT_MAX/1024 (see below)
# -N Kb/Mb/Gb dump split, dump larger
#               filesystems directly to tape
#               (example: -2 Gb)
}
holdingdisk hd2 {
directory "/disk2"
use 2 Gb
}
# If amanda cannot find a tape on which to store backups, it will
# run as many backups as it can to the holding disks. In order to
# save space for unattended backups, by default, amanda will only
# perform incremental backups in this case, i.e., it will reserve
# 100% of the holding disk space for the so-called degraded mode
# backups.
# However, if you specify a different value for the `reserve'
# parameter, amanda will not degrade backups if they will fit in the
# non-reserved portion of the holding disk.
# reserve 30 # percent
# This means save at least 30% of the holding disk space for
# degraded mode backups.
# Amanda needs a few Mb of diskspace for the log and debug files,
# as well as a database. This stuff can grow large, so the conf
# directory isn't usually appropriate. Some sites use
# /usr/local/var and some /usr/adm.
# Create an amanda directory under there. You need a separate
# # infofile and logfile for each configuration, so create
# subdirectories for each conf and put the files there. Specify the
# locations below.
# Note that, although the keyword below is infofile, it is only so
```
```