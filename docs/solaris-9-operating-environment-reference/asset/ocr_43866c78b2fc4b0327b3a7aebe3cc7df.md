# cdrw 133

The following example creates an audio CD from wav files on disc.

```
example% cdrw -a song1.wav song2.wav song3.wav song4.wav
```

The following example erases all data from a CD-RW disc in a CD-RW drive.

```
example% cdrw -b all
```

The following example creates a data CD on a system with multiple CD-R/RW drives.

```
example% cdrw -d cl6d0s2 -i /home/foo/iso-image
```

The following example checks whether the system can provide data to a CD-RW disc at a rate sufficient for the write operation.

```
example% cdrw -S -i /home/foo/iso-image
```

The following example runs cdrw at a higher priority (for root user only).

```
example# priocntl -e -p 60 cdrw -i /home/foo/iso-image
```

The following example creates the first session image in a multissection disc and records it onto the disc without closing it.

```
example% cdrw -0 -i /home/foo/iso-image
```

You can then add sessions to an open disc by creating an image with mkisofs(1M), using the session start and next writable address reported by cdrw.

```
example# cdrw -M
Track No. |Type |Start address
----------|------|-----------------
Leadout Data | 166564 | Data | 0nLast session start address: 162140
Next writable address: 173464
```

```
example% mkisofs -o /tmp/image2 -r -C 0,173464 -M /dev/rdsk/c0t2d0s2 /home/
```

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
| Availability | SUNWcdrw |

# See Also

audioconvert(1), mkisofs(1M), priocntl(1), attributes(5), rbac(5),
sca2usb(7D), sd(7D)