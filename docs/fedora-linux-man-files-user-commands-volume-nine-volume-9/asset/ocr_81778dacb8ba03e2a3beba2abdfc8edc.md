# ## NOTES

Supported image file formats:

**raw**  
Raw disk image format (default). This format has the advantage of being simple and easily exportable to all other elators. If your file system supports *holes* (for example in ext2 or ext3 on Linux or NTFS on Windows), then only the written sectors will reserve space. Use `qe-img info` to know the real size used by the image or `ls -ls` on Unix/Linux.

Supported options:

preallocation  
Preallocation mode (allowed values: off, falloc, full). falloc mode preallocates space for image by calling *posix_fallocate()*. full mode preallocates space for image by writing zeros to underlying storage.

**qcow2** QEMU image format, the most versatile format. Use it to have smaller images (useful if your filesystem does not supports *holes*, for example on Windows), optional AES encryption, zlib based compression and support of multiple VM snapshots.

Supported options:

compat  
Determines the qcow2 version to use. `compat=0.10` uses the traditional image format that can be read by any QEMU since 0.10. `compat=1.1` enables image format extensions that only QEMU 1.1 and newer understand (this is the default). Amongst others, this includes *zero clusters*, which allow efficient copy-on-read for sparse images.

backing_file  
File na of a base image (see **create** subcommand)

backing_fmt  
Image format of the base image

encryption  
If this option is set to on, the image is encrypted with 128-bit AES-CBC.

The use of encryption in qcow and qcow2 images is considered to be flawed by modern cryptography standards, suffering from a nuer of design problems:

+   - <The AES-CBC cipher is used with predictable initialization vectors based on the sector nuer. This makes it vulnerable to chosen plaintext attacks which can reveal the existence of encrypted data.  
+   - <The user passphrase is directly used as the encryption key. A poorly chosen or short passphrase will compromise the security of the encryption.  
+   - <In the event of the passphrase being compromised there is no way to> change the passphrase to protect data in any qcow images. The files st be cloned, using a different encryption passphrase in the new file. The original file st then be