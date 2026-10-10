# 732 Appendix A

Mcopy copies the specified file to the named file, or copies multiple files to the named directory. The source and target can be either MS-DOS or Unix files.

The use of a drive letter designation on the MS-DOS files, 'a:' for example, determines the direction of the transfer. A missing drive designation implies a Unix file whose path starts in the current directory. If a source drive letter is specified with no attached file name (e.g. mcopy a:: . ), all files are copied from that drive.

If only a single, MS-DOS source parameter is provided (e.g. "mcopy a:\foo.exe"), an implied destination of the current directory ('.') is assumed. A filename of '-' means standard input or standard output, depending on its position on the command line.

Mcopy accepts the following command line options:

+   * Q When mcoping multiple files, quits as soon as one copy fails (for example due to lacking storage space on the target disk).
+   * t Text file transfer. Mcopy translates incoming carriage return/line feeds to line feeds.
+   * n No confirmation when overwriting Unix files. Mcopy doesn't warn the user when overwriting an existing Unix file. In order to switch off confirmation for DOS files, use -o.
+   * m Preserve the file modification time. If the target file already exists, and the -n option is not in effect, mcopy asks whether to overwrite the file or to rename the new file ('name clashes') for details.

# BUGS

Unlike MS-DOS, the '+' operator (append) from MS-DOS is not supported. However, you may use mtype to produce the same effect:

```
```
mtype a:file1 a:file2 a:file3 >unixfile
mtype a:file1 a:file2 a:file3 | mcopy - a:msdosfile
```
```

# MDEL

The mdel command is used to delete an MS-DOS file. Its syntax is

```
```mdel [-v] msdosfile [msdosfiles ... ]```
```

Mdel deletes files on an MS-DOS filesystem.

Mdel asks for verification prior to removing a read-only file.