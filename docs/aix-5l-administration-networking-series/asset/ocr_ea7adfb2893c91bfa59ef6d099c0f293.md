The following is an example of an /etc/filesystems NFS stanza:

```
/usr/local/common:
    dev    = "/usr/local/common"
    vfs    = nfs
    nodename = yogi
    mount  = false
    type   = nfsfile
    options = bg,hard,intr
    account = false

/usr/sys/instd.images:
    dev    = "/usr/sys/instd.images"
    vfs    = nfs
    nodename = bambam
    mount  = false
    type   = nfsfile
    options = bg,hard,intr
    account = false

/usr/share/man:
    dev    = "/usr/share/man"
    vfs    = nfs
    nodename = dino
    mount  = false
    type   = nfsfile
    options = bg,hard,intr
    account = false

/sapmnt/help:
    dev    = "/sapmnt/help"
    vfs    = nfs
    nodename = sapprod1
    mount  = false
    type   = nfsfile
    options = ro,bg,hard,intr
    account = false
```

The type = nfsfile parameter may be added to the stanza definitions to identify NFS filesystems as an nfsfile group. This way, they can be mounted or unmounted as a group using the -t option of the mount and umount commands.