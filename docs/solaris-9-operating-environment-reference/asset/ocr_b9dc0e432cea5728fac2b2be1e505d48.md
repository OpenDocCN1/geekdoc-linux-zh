# 1592

# zipinfo

# zipinfo — List Detailed Information About a Zip Archive

# Synopsis

```
usr/bin/zipinfo [-12smlvhMTtz] file[.zip] [file(s)...] [-x xfile(s)...]
/usr/bin/unzip -Z [-12smlvhMTtz] file[.zip] [file(s)...]
-x xfile(s)
```

# Description

Note zipinfo is the same program as unzip (under UNIX, a link to it); on systems, however, zipinfo support may be omitted when unzip was compiled.

zipinfo lists technical information about files in a ZIP archive. Such information includes file permissions, encryption status, type of compression, version, and the operating or file system of compressing program. The default behavior (specifying file with no options) is to single-line entries for each file, with header and totals providing summary information for the entire archive. The format is a cross between UNIX ls -l and unzip -v output, as shown in the following example:

| castle%zipinfo.zip 106272 bytes 4 files |
| -rw-a-- 2.0 fat 76800 t-def 18-Aug-98 21:55 085X01.DOC |
| -rw-a-- 2.0 fat 67072 b-def 22-Aug-98 01:39 085X042.DOC |
| -rw-a-- 2.0 fat 95232 t-def 31-Aug-98 20:29 085X042.DOC |
| -rw-a-- 2.0 fat 63488 t-def 4-Oct-98 20:24 085X04E.DOC |
| 4 files, 302592 bytes uncompressed, 105898 bytes compressed: 65.0% castle$

Note You may find convenient to define an alias for zipinfo on systems that allow others. You can copy and rename the executable, create a link, or create a command file with the name ii. The ii parallels the common 11 aliases for long listings in UNIX. The similarity between the outputs of the two commands was intentional.

# Arguments

file[.zip] Path of the ZIP archive(s). If you specify a wild-card for file, each matching file in an order determined by the operating system (or file system). Only the file name can be a wild-card; Wild-card expressions are similar to UNIX egrep(1) (regular) expressions and may contain:

+   * Match sequence of zero or more characters.
* Match exactly one character.