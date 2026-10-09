mounted. If you really want to protect your data, create your key directly on the USB device and don’t leave it on your filesystem where a hypothetical intruder could recover it. (Even deleting the file still leaves remnants that a skilled attacker could conceivably extract.)

```
# dd if=/dev/random of=/media/da0p1.key bs=64 count=1
1+0 records in
1+0 records out
64 bytes transferred in 0.000149 secs (429497 bytes/sec)
```

The 64 bytes of data constitute a 512-bit key. You can increase the size of the key if you like, at the cost of extra processor overhead when accessing the encrypted filesystem. Don’t forget that your passphrase also increases key complexity.

To assign a passphrase to the key, use geli init. The -s flag tells geli(8) the desired sector size on the encrypted filesystem; 4,096 bytes, or 4KB, is usually a decent sector size for this application. The -k indicates the key file. You must also specify the device to be encrypted.

```
# geli init -s 4096 -K /media/da0p1.key /dev/da0p1
Enter new passphrase:
Reenter new passphrase:
```

A passphrase is much like a password except that it can contain spaces and be of any length. If you really want to protect your data, I recommend using a passphrase that is several words long, contains nonalphanumeric characters, and is not a phrase in your native language.

Now that you have a key, attach it to the device to be encrypted.

```
# geli attach -k /media/da0p1.key /dev/da0p1
Enter passphrase:
```

GLI now knows that /dev/da0p1 is an encrypted disk and that the file /media/da0p1.key contains the key file. Once you enter the passphrase, you can access the decrypted contents of the encrypted disk at the new device node, /dev/da0p1.el. Of course, you need a filesystem to put any data on that disk.