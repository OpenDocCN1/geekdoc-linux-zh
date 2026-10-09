view it directly. These utilities work particularly well on files that contain a lot of repeated information, such as text and image data, although most image data is already in a compressed format. The $x\mathrm{z}$ utility can yield a smaller compressed file than bzip2 and bzip2 can yield a smaller compressed file than gzip.

Normally these utilities do not overwrite a file; you must use --force to overwrite a file during compression or decompression.

# **gzip versus zip**

> Do not confuse gzip and gunzip with the zip and unzip utilities. The $zip$ and $unzip$ utilities pack and unpack an archive that might contain several files compressed into a single file. That compressed file is typically imported from or exported to a Windows system.
> 
> In contrast, when given multiple filenames as arguments, $gzip$ compresses each file individually and $gunzip$ decompresses individual files. It does not create an archive.
> 
> The $zip$ and $unzip$ utilities are compatible with WinZip, a Windows program that compresses and archives files.

# **ARGUMENTS**

The arguments are the pathnames of one or more ordinary files (no directories except when you call $gzip$ with the -r option) that are to be compressed or decompressed. Without arguments, or if the special option — is present, these utilities read from standard input. By default, when these utilities compress a file, they create a new, compressed version of the file with a filename extension of $xz$ ($xz$), $bz2$ ($bzip2$), or $gz$ ($gzip$) and delete the original file. We reverse the process when they decompress a file.

In the following example, $x\mathrm{z}$ compresses the myprog file, reducing its size, deleting the original file, and creating a new file named myprog.$xz$.

```
$\$\ ls\ -1$
$-\ rwxr-xr-x.\ 1\ sam\ sam\ 982296\ 06-07\ 13:50\ myprog$
$\$\ xz\ myprog$
$\$\ ls\ -1$
$-\ rwxr-xr-x.\ 1\ sam\ sam\ 387535\ 06-07\ 13:50\ myprog.xz$
```

# **OPTIONS**

**Standard output** The -c (--stdout) option writes the results of compression or decompression to standard output. This option implies the -k option.

**Decompress** The -d (--decompress) option decompresses a file that was compressed using $x\mathrm{z}$. This option with $x\mathrm{z}$ is equivalent to the $unxz$ utility ($unxz$ is a link to $x\mathrm{z}$). With $bzip2$ it is equivalent to $bunzip2$, and with $gzip$ it is equivalent to $gunzip$.

```
$\$\ xz\ -d\ myprog.xz$
$\$\ ls\ -1$
$-\ rwxr-xr-x.\ 1\ sam\ sam\ 982296\ 06-07\ 13:50\ myprog$
```

**Quality** The -n option sets the compression level when compressing a file. Under $x\mathrm{z}$, the $n$ is a digit from 0 to 9; under $bzip2$ and $gzip$ it is from 1 to 9. Level 0 or 1 compression