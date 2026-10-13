# Installing Software from Compressed Archives: .tar.gz

Linux software applications in the form of source code are available at different sites on the Internet. You can download any of this software and install it on your system. Recent releases are often available in the form of compressed archive files. Applications will always be downloadable as compressed archives, if they don't have an RPM version. This is particularly true for the recent versions of GNOME or KDE packages. RPM packages are only intermittently generated.

# Decompressing and Extracting Software in One Step

Though you can decompress and extract software in separate operations, you will find that the more common approach is to perform both actions with a single command. The tar utility provides decompression options you can use to have tar first decompress a file for you, invoking the specified decompression utility. The z option automatically invokes gunzip to unpack a .gz file, and the j option unpacks a .bz2 file. Use the z option for .z files. For example, to combine the decompression and unpacking operation for a tar.gz file into one tar command, insert a z option to the option list, xzvf ( see the section "Extracting Software" later in this chapter for a discussion of these options). The next example shows how you can combine decompression and extraction in one step:

```
```bash
# tar xzvf htdig-3.1.6.tar.gz
```
```

For a .bz2 compressed archive, you would use the j option instead of the z option.

```
```bash
# tar xvjf htdig-3.1.6.tar.bz2
```
```

# Decompressing Software

Many software packages under development or designed for cross-platform implementation may not be in an RPM format. Instead, they may be archived and compressed. The filenames for these files end with the extension .tar.gz, tar.bz2, or .tar.Z. The different extensions indicate different decompression methods using different commands: gunzip for .gz, bunzip2 for .bz2, and decompress for .Z. In fact, most software with an RPM format also has a corresponding .tar.gz format. After you download such a package, you must first decompress it, and then unpack it with the tar command. The compressed archives could hold either source code that you then need to compile or, as is the case with Java packages, binaries that are ready to run.

A compressed archive is an archive file created with tar, and then compressed with a compression tool like gzip. To install such a file, you must first decompress it with a decompression utility like gunzip utility, and then use tar to extract the files and directories making up the software package. Instead of the gunzip utility, you could also use gzip -d. The next example decompresses the htdig-3.1.6.tar.gz file, replacing it with a decompressed version called htdig-3.1.6.tar:

```
```bash
# ls
htdig-3.1.6.tar.gz
# gunzip htdig-3.1.6.tar.gz
# ls
htdig-3.1.6.tar
```
```

You can download compressed archives from many different sites, including those mentioned previously. Downloads can be accomplished with FTP clients such as ncftp and Gftp, or with any Web browser, such as Mozilla. Once downloaded, any file that ends with .Z, .bz2, .zip, or .gz is a compressed file that must be decompressed.

For files ending with .bz2, you would use the bunzip2 command. The following example decompresses the Java 2 SDK downloaded from www.blackdown.org:

```
```bash
# bunzip2 j2sdk-1.3.0-FCS-linux-i386.tar.bz2
```
```