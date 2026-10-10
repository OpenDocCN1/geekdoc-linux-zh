```
```
/etc/rc.config.d/vpqstd
/etc/rc.config.d/vparhb
/etc/rc.config.d/vparinit

/sbin/init.d/vpard
/sbin/init.d/vparhb
sbin/init.d/vparinit
```
```

These files are covered in detail in Chapter 8, which covers vPars start-up in detail. Of particular interest is vparhp, which is the heartbeat daemon related to keeping vpdh synchronized on all of your vPars.

Very important to your work related to vPars are the online man pages. The following listing shows the man pages loaded on my system at the time of this writing.

```
```
# man -k vpar
vparboot (1M)           - boot a virtual partition
vparcreate (1M)         - create a virtual partition
vpardump (1M)           - manage monitor dump files
vparextract (1M)        - extract memory images from a running virtual
                        partition system
vparmodify (1M)         - modify the attributes of a virtual partition
vparreloc (1M)          - relocate the load address of a vmunix file,
                        determine if a vmunix file is relocatable,
                        or promote the scope of symbols in a
                        relocatable vmunix file
vparremove (1M)         - remove a virtual partition
vparreset (1M)          - reset a virtual partition
vparresources (5)       - description of virtual partition resources
                        and their requirements
vparstatus (1M)         - display information about one or more
                        virtual partitions
vpartition (1)          - display information about the Virtual
                        Partition Command Line Interface
vparutil (1M)           - get and set SCSI parameters for SCSI
                        controllers from a virtual partition
#```
```

Many of these man pages appear in Appendix A, so you can refer to them as you read the chapters in this book.

At this point we have HP-UX 11i and the Virtual Partitions software loaded on the system. In the next chapter we’ll configure Virtual Partitions which will allow us to run multiple instances of HP-UX 11i simultaneously on the same server.

The remainder of this chapter covers background related to loading HP-UX 11i. This will need to be done on a volume for every HP-UX 11i you wish to run simultaneously on your vPars server. This is a step-by-step proce-