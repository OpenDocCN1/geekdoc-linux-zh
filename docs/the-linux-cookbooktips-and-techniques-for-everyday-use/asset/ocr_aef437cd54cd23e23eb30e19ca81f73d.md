+   To list the contents of an archive called `project.tar`, type:

```
$ tar -tvf project.tar RET
```

This command lists the contents of the `project.tar` archive. Using the `-v` option along with the `-t` option causes tar to output the permissions and modification time of each file, along with its file name—the same format used by the ls command with the `-l` option (see section Listing File Attributes).

Include the `-z` option to list the contents of a compressed archive.

+   To list the contents of a compressed archive called `project.tar.gz`, type:

```
$ tar -ztvf project.tar RET
```

# 9.6.3 Extracting Files from an Archive

To extract (or unpack) the contents of a tar archive, use tar with the `-x` ("extract") option.

+   To extract the contents of an archive called `project.tar`, type:

```
$ tar -xvf project.tar RET
```

This command extracts the contents of the `project.tar` archive into the current directory.

If an archive is compressed, which usually means it will have a `.tar.gz` or `.tgz` extension, include the `-z` option.

+   To extract the contents of a compressed archive called `project.tar.gz`, type:

```
$ tar -zxvf project.tar.gz RET
```

NOTE: If there are files or subdirectories in the current directory with the same name as any of those in the archive, those files will be overwritten when the archive is extracted. If you don't know what files are included in an archive, consider listing the contents of the archive first (see section Listing the Contents of an Archive).

Another reason to list the contents of an archive before extracting them is to determine whether the files in the archive are contained in a directory. If not, and the current directory contains many unrelated files, you might confuse them with the files extracted from the archive.