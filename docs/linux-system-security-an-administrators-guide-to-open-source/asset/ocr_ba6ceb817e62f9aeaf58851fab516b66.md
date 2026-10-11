Table 15.5 TCFS Distribution

| Distribution File | Contents |
| --- |
| tcfs-2.2.2-distrib.tar.gz | The distribution GNU-compressed tar file. It contains all of the other tar and patch files. |
| patch-linux-2.0.x | The patch to the Linux 2.0.x kernel. |
| tcfs-2.2.2.tar.gz | The TCFS source code for the tcfs filesystem kernel module and the TCFS encryption module (3desmodule). |
| tcfslib-0.3.1.tar.gz | The TCFS library. It contains the source code used to build the key management database libraries. |
| tcfsutils-1.2.1.tar.gz | Contains the utilities used for configuring and managing TCFS users and keys. The utilities are tcfsGENkey, tcfsputkey, tcfsmkkey, tcfsliewkey, tcfsaduser, tcfsrmuser, tcfsadgroup, and tcfsrmgroup. These utilities are discussed in subsequent sections. |
| mount-2.71-tcfs.tar.gz | Contains the replacement mount, swapon, and losetup programs. |
| e2fsprog-1.12-tcfs.tar.gz | The replacement ext2 filesystem programs. Included are chattr, lasttr, mke2fs, badblocks, tune2fs, dumpe2fs, e2label, and fsck. New attributes are added to chattr as described in the section, Extended Attributes for TCFS on page 427. |
| shadow-980529-tcfs.tar.gz | Contains replacement chage, pwconv, gpcn, and other programs contained in the shadow-utils RPM. |
| xattrd-2.1.tar.gz | Contains the server-side TCFS daemon xattrd. This daemon responds to TCFS queries regarding the secure attributes associated with the TCFS resources. It is necessary because NFS cannot handle ext2 extended file attributes. The ext2 extended attributes as they relate to TCFS are discussed in Extended Attributes for TCFS on page 427. |

```
# cd /usr/src/custom/tcfs
# tar xvfz tcfs-2.2.2-distrib.tar.gz
The extraction will create the subdirectory /usr/src/custom/tcfs/tcfs-2.2.2, yielding the files listed in the Distribution File column of Table 15.5.
```

+   Apply the kernel patch
+   ```sh
+   # cd /usr/src
+   # patch -p0 < /usr/src/custom/tcfs/tcfs-2.2.2/patch-linux-2.0.x
+   ```