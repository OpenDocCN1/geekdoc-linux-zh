# SECURITY

# Data encryption needs to be made ubiquitous, transparent, flexible, easily deployable, integrated into the data handling process and, of course, secure enough to counter sophisticated attacks.

Newer versions of the Linux kernel contain more feature-rich versions of eCryptfs. For instance, Linux kernel version 2.6.19 is the first official kernel version that contains eCryptfs, and only passpharse mode of operation is available at that kernel. At the time of this writing, the development kernel branch version 2.6.20-mm contains public key support, so that feature may be now available in more recent mainline kernel versions. You can determine the features available in your kernel by loading the eCryptfs module and viewing the contents of /sys/encryptfs/version_str under your sysfs mountpoint.

Popular Linux distributions carry the eCryptfs user-space packages; follow the software package installation procedure for your distribution to install the eCryptfs-utils package. If the eCryptfs user-space tools are not yet available from your distribution, you can download, build and install the source tarball. You can obtain the user-space components from the eCryptfs SourceForge site (eCryptfs.sourceforge.net).

If eCryptfs is built as a kernel module, you need to load the module:

```
# modprobe eCryptfs
```

At this point, you can begin using eCryptfs with whatever filesystem you are currently using. To mount eCryptfs, specify the lower directory for the encrypted files and the eCryptfs mountpoint for the decrypted view of the files:

```
# mount -t eCryptfs /secret /secret
```

The first path is the lower directory, and the second path is the eCryptfs mountpoint. Note that the lower directory and the mountpoint have the same path in this example. These paths can be different, but I recommend doing a layer mount in order to help ensure that only eCryptfs has access to the files in the lower filesystem. This command transforms the given path from the lower directory into the eCryptfs mountpoint for the duration of the mount.

When performing a mount, the eCryptfs mount helper first attempts to read in options from the eCryptfsFile.ini in the current user home directory, and then it reads options provided via the command line. The mount helper interactively prompts for any mandatory options that are not specified in the eCryptfsFile.ini or the command line. For instance, you may be asked to choose a passphrase and a cipher.

Once the mount has completed successfully, files written to the /secret mountpoint will be encrypted transparently and written to the /secret directory in the lower filesystem. Encrypted files that exist in the lower /secret directory and that are able to be decrypted with the key specified at the time of the mount will be accessible in their unencrypted form when read from the /secret eCryptfs mountpoint.

When you unmount eCryptfs and look in /secret, you will see the encrypted lower files. You may first notice that the lower files are larger than the files viewed under the eCryptfs mountpoint. The exact size of the lower files depends on the page size of your host and on the amount of data written. In general, the minimum lower file size is either 12KB or your host page size plus 4KB, whichever is larger. This helps ensure page alignment between the eCryptfs file and the lower file, which helps performance. The lower file then grows in 4KB increments as data spills into new 4KB data extents.

The extra space at the front of each lower file contains cryptographic metadata about the file, such as attribute flags and an encrypted file encryption key. Having this information in the file contents makes it convenient to transfer or back up the files while preserving all the information necessary to access the files later. However, the headers can take up a disproportionately large amount of space if there are many small files. Newer releases of eCryptfs can store the data in the extended attribute region instead, reducing the size of the lower encrypted files; refer to eCryptfs on-line documentation at eCryptfs.sourceforge.net (for more information on using this feature.

If your kernel has public key support, you can utilize one of the eCryptfs key modules to manage your key. You can check for support in the version of eCryptfs in your kernel by viewing the contents of /sys/encryptfs/version_str under your sysfs mountpoint. If there is support, you will see pubkey listed as one of the supported features.

Key modules can be selected and parameterized via mount options. If you want to use the OpenSSL key module, you first need to generate a public/private key pair to use in eCryptfs. To generate a key pair, do the following:

+   - Run eCryptfs - Manager.
+   - Select menu option 3.
+   - Select the openssl key module.

You also need to run the eCryptfs daemon in order to manage kernel-user-space communications; the daemon can be started simply by running the executable:

```
# eCryptfsd
```

Note that running the daemon is not necessary if you are using only the passphrase mode of operation. Then, assuming you created your key in /usr/local/mykey.pem, you would mount with the following options:

```
# mount -t eCryptfs \\
- o key=openssl:keyfile=/usr/local/mykey.pem \\
/ secret /secret
```

Given these options, the eCryptfs mount helper prompts you for a passphrase that protects the private key contained in the key file. You can mount the same lower directory with many different combinations of keys and ciphers (known as a mount context), and that particular context will apply to any new files created under the mountpoint. For current versions of eCryptfs, files created under any given mount context will be accessible only when the mount is performed with that same context.

# Notes on Security

As with any filesystem, you should make regular backups of your data when using eCryptfs. This is done easily and securely by unmounting