# Working with zip Archives

The common zip archive format (associated with the DOS and Windows programs PKZIP and WinZip among others) is supported on Linux. To unzip a zip archive, simply do the following:

```
user@blog:~ unzip zipfile.zip
```

To create a zip archive of the current directory:

```
user@blog:~ zip -r ~/newzip.zip
```

This will recursively zip the current directory and create the zip file newzip.zip in your home directory (-).

The program zipinfo will give a listing and information about compression ratios:

```
user@blog:~ zipinfo zipfile.zip
Archive: zipfile.zip 7762 bytes 2048 bytes stor 21-Jun-04 20:06 file
-w-r-r- 2.3 unx 4096% stor 21-Jun-04 20:07 file
dwc-x-X- 2.3 unx 21-Jun-04 20:10 directory/
-w-r-r- 2.3 unx 2048 bytes deflate 21-Jun-04 20:10 directory/cfile
4 files, 8192 bytes compressed, 11.7%
```

# Unpacking RPM Packages

Typically, you can do everything you need to manipulate RPM packages using the rpm command, but it is sometimes to know how to convert an RPM package to a cpio archive as:

```
user@blog:~ rpm2cpio package-0.6.2-15.258.rpm >package.cpio
```

You can unpack the archive under the current directory with:

```
user@blog:~ cpio -ivd < package.cpio
```

Here again, the i option unpack the archive, the d option creates the necessary directories as cpio verbely () on the archive. You will find-directories under the current directory corresponding to the system locations where rpm will install the particular files. This corresponds to what you see if you look inside the rpm package with mc, for example.

# Using pax

A nice alternative to tar and cpio is pax, which is capable of unpacking archives in both of these formats. Its command syntax is simpler to learn than either tar or