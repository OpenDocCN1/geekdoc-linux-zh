/dev/rdiskette Symbolic link providing character device access for the diskette in the primary diskette drive, usually drive 0.

/vol/dev/dsk Directory providing block device access for the PCMCIA memory and ata cards and removable media devices.

/vol/dev/rdsk Directory providing character device access for the PCMCIA memory and ata cards and removable media devices.

/vol/dev/aliases/pcmmsS Symbolic link to the character device for the PCMCIA memory card in where S represents a PCMCIA socket number.

/vol/dev/aliases/rmdisk0 Symbolic link to the generic removable medium device that is not a Zip, Jaz, CD-ROM, diskette, DVD-ROM, PCMCIA memory card, and so forth.

/dev/rdsk Directory providing character device access for the PCMCIA memory and ata cards and other removable devices.

/dev/dsk Directory providing block device access for the PCMCIA memory and ata cards and other removable media devices.

# ### Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwcsu |

# ### See Also

cpio(1), eject(1), fdformat(1), tar(1), volcancel(1), volcheck(1), volmissing(1), volmmount(1), format(1M), mkfs_pcfs(1M), mount(1M), newfs(1M), prtvtoc(1M), rmmount(1M), rpc.smserved(1M), void(1M), rmmount.conf(4), void.conf(4), attributes (5), pcfs(7FS), udfs(7FS)

# ### roffbib — Format and Print a Bibliographic Database

# ### Synopsis

```
/usr/bin/roffbib [-e] [-h] [-m filename] [-np] [-olist] [-Q] [-raM]
[-sM] [-Tterm] [-V] [-x] [filename]...
```