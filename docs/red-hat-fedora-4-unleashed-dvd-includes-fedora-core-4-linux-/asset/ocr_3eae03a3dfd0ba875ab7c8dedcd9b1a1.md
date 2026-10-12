favorite FTP client and log in as anonymous. Because you are interested in the 2.6 kernel, change directories to `/pub/linux/kernel/v2.6`. The latest stable kernel as of this writing is `2.6.11`.

**Note**

ftp.kernel.org receives more than its share of requests for download. It is considered a courtesy to use a mirror site to reduce the traffic that ftp.kernel.org bears. http://www.kernel.org/mirrors/ has a list of all mirrors around the world. Find one close to your geographic location and substitute that address for ftp.kernel.org.

A number of different entries are on the FTP archive site for each kernel version, but because you are only interested in the full kernel it is only necessary to get the full package of source code. There are two of these packages:

```
linux-2.6.11.tar.gz
linux-2.6.11.bz2
```

Although these are the same kernel packages, they are built using different compression utilities: The `.gz` extension is the gzip package, found on almost every Linux system available. The `.bz2` extension is the newer bzip2 utility, which has better compression than gzip. Both packages have the same content, so download the one compressed with the program you use.

Once downloaded, move the package to a directory other than `/usr/src` and unpack it. If you downloaded the `.gz` package, the unpacking command is `tar -xzvf linux-2.6.11.tar.gz`. Otherwise, the bzip2 unpack command is `tar -xjvf linux-2.6.11.tar.bz2`. Once unpacked, the package will create a new directory, `linux-2.6.11`. Copy it to `/usr/src` or move it there. Then, create a symbolic link of `linux-2.6` to `linux-2.6.11` (otherwise, some scripts will not work). Here is how to create the symbolic link:

```
# rm /usr/src/linux-2.6
# ln -s /usr/src/linux-2.6.11 /usr/src/linux-2.6
```

By creating a symbolic link to `/usr/src/linux-2.6`, it is possible to allow multiple kernel versions to be compiled and tailored for different functions: You will just change the symbolic link to the kernel directory you want to work on.

**CAUTION**

The correct symbolic link is critical to the operation of make. Always have the symbolic link point to the version of the kernel sources you are working with.

# ## Patching the Kernel

It is possible to patch a kernel to the newest Linux kernel version as opposed to downloading the entire source code. This choice can be beneficial for those who are not using a