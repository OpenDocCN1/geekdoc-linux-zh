Detailed information about how to install and remove a patch is provided in the Install.info file included with each patch. Each patch also contains a README file that contains specific information about the patch.

Patches come in three different formats. Solaris 8 patches come in zip format, such as 104945-02.zip. For Solaris 8 patches, use the unzip command to extract the patch files as follows:

```
/usr/bin/unzip 104945-02.zip
```

For Solaris 2.6 and earlier operating environments, patches might come in compressed tar format, such as 104945-02.tar.Z. Use the zcat command to decompress this type of patch file and the tar command to create the patch directories, as follows:

```
/usr/bin/zcat 104945-02.tar.Z | tar xvf -
```

Other Solaris patches might come as gzip compressed tar files, such as 102945-02.tar.gz. To extract a gzip compressed tar file, use the gzcat command to decompress and create the patch directories as follows:

```
/usr/bin/gzcat 104945-02.tar.gz | tar xvf -
```

The patchadd command is used to install directory-format patches to a Solaris 8 system. It must be run as root. The syntax is as follows:

```
patchadd [ -d ] [ -u ] [ -B backout_dir ]
```

The patchadd command is described in Table 4.4.

# TABLE 4.4

# patchadd Command Options

| Common Option | Description |
|---|---|
| -d | Does not create a backup of the files to be patched. The patch cannot be removed when this option has been used to install the patch. By default, patchadd saves a copy of all files being updated so that the patch can be removed if necessary. Do not use the -d option unless you're positive the patch has been tested. |
| -p | Displays a list of the patches currently applied. |