
# zipinfo 1595

Values for the second character are summarized below.

- Neither the header nor the extra field exists.
- 1 The file has an extended local header but no extra field.
- x The file has an extra field but no extended local header.
- x The file has an extra field and an extended local header.

Thus, the file in this example is (probably) a text file, is not encrypted, and has neither an extra field nor an extended local header associated with it. The sixth field indicates the compression method and possible submethod used. Methods are known at present:

- Storing (no compression).
- Reducing.
- Shrinking.
- Imploding.
- Tokenizing (never publicly released).
- Deflating.

In addition, there are four levels of Redundon (1 through 4); four types of imploding (4K or 8K sliding dictionary, and 2 or 3 Shannon-Fano trees); and four levels of defl (superfast, normal, maximum compression). zipinfo represents these methods and their submethods as follows: stor; re:1, re:2, etc.; shrk; 14:2, 18:3, etc.; tokn; deFS, deFF, deffin, and defn.

The last three lines contain the modification date and time of the file and its name. The case of the file name is respected so that files that come from MS-DOS PKZIP are always capitalized. If the file was zipped with a stored directory, that name is also displayed as part of the file name.

The example is an encrypted binary file with an extra field. The attributes are in the first line listed in VMS format.

| RWD, R | 0.9 vms | 168 Bx shr | 9-Aug-91 19:15 perms.0644 |
| --- | --- | --- | --- |

Extra fields are used for various purposes (see the discussion of the -v option), including the storage of VMS file attributes, which is presumably the case here. Here other possibilities for the host file system (HPFS), MS-DOS, OS/2 or NT with File Allocation Table (FAT) file system, and Macintosh are denoted as:

```
-rw-a---- 1.0 hpf 5358 TI 14:3 4-Dec-91 11:33 longfilename.hpfs
--r--a---- 1.1 fat 4096 -b 14:2 14-Jul-91 12:58 EA DATA. SF
---------- 1.0 mac 17357 bx 18:2 4-May-92 04:02 unzip.macr
```

File attributes in the first two cases are indicated in a UNIX-like format, with seven fields specify the following information:

1. The file is a directory.
2. The file is readable (always true).
3. The file is writable.
4. The file is executable (guessed on the basis of the extension)—exe, .com, .bat, .cmd, or .btml.
5. The file has its archive bit set.

# 1596 zipinfo

6. The file is hidden.
7. The file is a system file.

Interpretation of Macintosh file attributes is unreliable because some Macintosh archivers do not store any attributes almost identical to the short format except that they add information on file compression. The medium format lists the file compression as a factor, indicating the amount of space that has been removed. In the following example, the file has been compressed by more than a factor of five; the compressed data is only 19 percent of the original size.

```
-rw-rw---- 1.5 unix 2802 t- 81% defx 11-Aug-91 13:48 perms.2660
```

The long format shows the compressed file's size in bytes, as shown in the following example.

```
-rw-rw---- 1.5 unix 2802 t- 538 defx 11-Aug-91 13:48 perms.2660
```

You can add the -Option to change the file and time to decimal format, as shown below.

```
-rw-rw---- 1.5 unix 2802 t- 538 defx 910811.134804 perms.2660
```

Note because of limitations in the MS-DOS format used to store file times, the second field is always rounded to the nearest even second. For UNIX files, this is expected to change in the next major releases of zip and unzip().

In addition to file information, a default file list also includes headers and totals, as shown in the following example.

| Archive: OS2.zip 5453 5 files |
| --- |
| rw, 1.0 hpf 731 b- 14:23-Jun-92 23:40 Contents |
| rw, 1.0 hpf 3710 b- 14-Jun-92 23:33 myfile.02 |
| rw, 1.0 hpf 8753 b- 18:26-Jun-92 15:29 osunzip.c |
| rw, 1.0 hpf 98 b- 21-Aug-91 15:34 unzip |
| rw, 1.0 hpf 95 b- 21-Aug-91 17:51 zipinfo.def |
| 5 files, 13386 uncompressed, 495 bytes compressed: 63.0% |

The header line shows the name of its archive, size, and the total number of files. The totals show the files listed, their total uncompressed size, however, if you specify one or more file(s), the headers and totals are not listed. This behavior is also similar to that of ls -l command. You can override this behavior by specifying the -h and -t options. If you specify the -h or -t options, you must also specify the listing format; for example, zipinfo -ht. If you do not specify a listing format with -h, or -t, only the specified files are listed. The verbose list is self-explanatory. It lists file contents, if any, and the type and number of bytes in any stored fields. Currently known types of extras include PKWARE's annotation; VMS system information; Macintosh resource forks; HPFS information, and so. In OS/2 extended attributes—the most common use of extra fields—the size of the stored EAs as reported by zipinfo may not match the number given by OS/2's dir command: OS/2 always reports the number of required bytes in 16-bit format, whereas zipinfo reports 32-bit.

# Environment Options

Modifying the zipinfo default behavior with options in an environment variable is a bit to explain because zipinfo tries to handle various defaults in an intuitive, yet UNIX-like, manner (Try not to laugh.) zipinfo has three priority levels of options:

- Default options
- Environment options, which can override or add to defaults.
- Explicit options on the command line, which can override or add to either.

The default variable is ZIPINFO_OPTS for VMS (where the symbol used to install zipinfo as foreign would otherwise be confused with the environment variable) and ZIPINFO for all other systems. With zip, ZIPINFO is also accepted (dont ask). If you define both ZIPINFO and ZIPINPUT, ZIPINFO takes precedence. The default listing format corresponds roughly to the zipinfo -hst command (except when you specify individual files). If you prefer the long format (-1), you can change the default by using the ZIPINFO environment variable, as shown below.

```
ZIPINFO=-1
```
- Bourne shell
```
setenv ZIPINFO -1
```
- UNIX C shell
```
ZIPINFO=-1
```
- OS/2 or MS-DOS.
```
You can also specify negative options to override defaults. Precede the undesired option with one or more dashes. For example, if you don't like the totals, you can specify -t or --t. The first dash is the regular switch character, but the second one is also interpreted as a minus sign. This dual use of dashes may seem a little awkward, but its reasonably intuitive. After the first dash, any other dashes signify a negative option. This syntax is consistent with the behavior of the UNIX command.

# Bugs

With unzip, zipinfo -M option is overly simplistic in its handling of output. It fails to detect the wrapping of long lines and scroll lines at the top of the screen before they are read. zipinfo should detect and treat each occurrence of line wrap as an additional line print, which requires knowledge of both the screen width and height. In addition, zipinfo should detect the true screen geometry on all systems. The multiple listing formats are unnecessarily complex and should be simplified (That is not to say they will.).

# Examples

The following example displays a basic, short-format listing of the complete contents of the 085DOC.ZIP archive, with both header and totals lines.

```
castle$ zipinfo 085XDOCS 106272 bytes 4 files
Archive: 085XDOCS.zip
-rw-a-- 2.0 fat 76800 t- defN 18-Aug-98 21:55 085X01.DOC
-rw-a-- 2.0 fat 67072 b- defN 22-Aug-98 01:39 085X02.DOC
-rw-a-- 2.0 fat 95232 t- defN 31-Aug-98 20:29 085X04.DOC
-rw-a-- 2.0 fat 63488 t- defN 4-Oct-98 20:24 085X04E.DOC
4 files, 302592 bytes uncompressed, 105858 bytes compressed: 65.0%
castle$
```

The following example displays a basic, long-format (not verbose), including header and totals lines.

```
castle$ zipinfo -1 085XDOCS 106272 bytes 4 files
Archive: 085XDOCS.zip
-rw-a-- 2.0 fat 76800 t- defN 18-Aug-98 21:55 085X01.DOC
-rw-a-- 2.0 fat 67072 b- defN 22-Aug-98 01:39 085X02.DOC
-rw-a-- 2.0 fat 95232 t- defN 31-Aug-98 20:29 085X04.DOC
-rw-a-- 2.0 fat 63488 t- defN 4-Oct-98 20:24 085X04E.DOC
4 files, 302592 bytes uncompressed, 105858 bytes compressed: 65.0%
castle$
```

The following example lists the contents without header and totals.

```
castle$ zipinfo -h-t 085DOCS
-rw-a-- 2.0 fat 76800 t- defN 18-Aug-98 21:55 085X01.DOC
-rw-a-- 2.0 fat 67072 b- defN 22-Aug-98 01:39 085X02.DOC
-rw-a-- 2.0 fat 95232 t- defN 31-Aug-98 20:29 085X04.DOC
-rw-a-- 2.0 fat 63488 t- defN 4-Oct-98 20:24 085X04E.DOC
castle$
```

The following example produces the same result as the previous one, using a different syntax. The backslash is required only if the shell would otherwise expand the * in double quotes.

```
castle$ zipinfo 085XDOCS\*
```

The following example uses the ZIP environment variable to turn off the lines.

```
castle$ setenv ZIPINFO --t
castle$ zipinfo 085XDOCS
Archive: 085XDOCS.zip 106272 bytes 4 files
-rw-a-- 2.0 fat 76800 t- defN 18-Aug-98 21:55 085X01.DOC
-rw-a-- 2.0 fat 67072 b- defN 22-Aug-98 01:39 085X02.DOC
-rw-a-- 2.0 fat 95232 t- defN 31-Aug-98 20:29 085X04.DOC
-rw-a-- 2.0 fat 63488 t- defN 4-Oct-98 20:24 085X04E.DOC
castle$
```
