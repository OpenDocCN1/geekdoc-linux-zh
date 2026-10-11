running the patch from the /usr/src/linux-2.4 directory and should therefore use the following command:

```
cat patchfile.txt | patch -p3
```

This applies the patch with no applied pathnames because the first / was removed with the -p1. Then usr/ is removed by the -p2 option, and finally the /linux section is removed by the -p3 option.

Additionally, if you are patching the kernel source code and the patch file is a compressed file in the gzip format, such as patch.gz, you can apply the patch without having to uncompress it:

```
zcat patch.gz | patch -p0
```

If you are using the bzip2 format for a compressed patch file, such as patch.bz2, you can use the bzcat command in a similar fashion:

```
bzcat patch.bz2 | patch -p0
```

# # Getting Kernel Source Code

When you decide to download the source code for the Linux kernel, be sure to get it either from your distribution vendor, such as a Red Hat source .rpm file, or from the http://www.kernel.org site.

It’s also very important that you validate the integrity for your kernel source code, taking care to either download the gpg or PGP signature file for the package or check the MD5 checksum with the md5sum utility.

To verify the MD5 checksum of a patch file, use this command:

```
md5sum patchfile.gz
```

This returns output similar to what’s shown here:

```
045d532750c91f05261e0012d5491792 patch.gz
```

To verify the gpg signature of a patch file, first download the patch.bz2.sign file that matches the version number of the patch code. The www.kernel.org site lists the appropriate signature files below or next to the patches. Then verify the code with this command:

```
gpg --verify patch.bz2.sign patch.bz2
```

This returns output similar to the following:

```
gpg: Signature made Fri 02 Aug 2002 06:43:54 PM EDT using DSA key ID
2517D0F0E
```