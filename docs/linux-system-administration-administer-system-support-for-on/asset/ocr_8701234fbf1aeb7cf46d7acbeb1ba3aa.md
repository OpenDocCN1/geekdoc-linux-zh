![](bbox=[0.07, 0.1, 0.16, 0.18])

> Take special care to keep the syntax of this command accurate. Reversing the syntax just given, for example, would dump the contents of the floppy drive to the /zImage file. I probably don't have to tell you not to do it. But don't do it.

# ## Backing Up with cpio

The cpio command copies files in and out of an archive and from directory to directory. It works really nicely with the find command, so you can assemble some nice commands that will backup for you.

The find command has an option of -cpio that will let you archive the files you found. For example, you found all the .rhosts files. You want to archive these files onto your tape drive so you have record of which users are being sloppy:

```
find / -name .rhosts -cpio /dev/rmt0;
```

Listing 10-3 illustrates using the cpio command for backup.

# Listing 10-3: Using cpio for backup

```
# cpio -help

Usage: cpio [-o|--create] [-OacvABLV] [-C bytes] [-H format] [-M message]
    [-0 [user@]host::archive] [-F [user@]host::archive]
    [--file=[user@]host::archive] [--format=format] [--message=message]
    [-null] [--reset-access-time] [-verbose] [-dot] [--append]
    [-block-size=blocks] [--dereference] [-io-size=bytes] [--quiet]
    [--force-local] [--help] [-version] < name-list > archive
    cpio [-i|--extract] [-bcdfmnrtuvBSV] [-C bytes] [-E file] [-H format]
    [-M message] [-R [user]::[group]] [-I [user@]host::archive]
    [-F [user@]host::archive] [--file=[user@]host::archive]
    [-make-directories] [--nomatching] [--preserve-modification-time]
    [--numeric-uid-gid] [--rename] [-list] [-swap-bytes] [-swap] [-dot]
    [-unconditional] [-verbose] [-block-size=blocks] [-swap-halfwords]
    [-io-size=bytes] [-pattern-file=file] [-format=format]
    [-owner=[user]::[group]] [-no-preserve-owner] [--message=message]
    [-force-local] [-no-absolute-filenames] [-sparse] [-only-verify-crc]
    [-quiet] [-help] [-version] [pattern...] < archive
    cpio [-p|--pass-through] [-OadmuvLV] [-R [user]::[group]]
    [-null] [--reset-access-time] [--make-directories] [-link] [--quiet]
    [--preserve-modification-time] [-unconditional] [-verbose] [-dot]
    [--dereference] [-owner=[user]::[group]] [-no-preserve-owner]
    [-sparse] [-help] [-version] destination-directory < name-list
```