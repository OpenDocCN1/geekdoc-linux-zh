# Using the at Utilities

The at command can be controlled by two utilities:

+   - atrm: Deletes tasks. Type: atrm job.
+   - atq: Lists tasks for the current user, or all jobs if used by the root user. Type: atq.

# Compressing and Archiving Files From the Command Line

Compressing and archiving files are useful for making backups and e-mail attachments.

Compression reduces the size of files and places them in a single file. Archiving creates a single file in which to store multiple files.

In both cases, the individual files cannot be accessed by file managers or normal commands for manipulating files. Instead, you must use special tools designed for the utility that you used for compression.

The processes of decompressing and unarchiving are both referred to as extracting. You can use special commands for extracting, or options in the same tools that you use for compressing or archiving.

Archived files are called tar files, tarred files, or tarballs.

Linux includes several tools for compressing and archiving:

+   - tar: mainly an archive tool, but also compresses files. Many long time users prefer tar to the alternatives.
+   - gzip: a compression tool. Sometimes, gzip can decompress a zip file from another operating system, but do not confuse the two formats or expect them to be always interchangeable.
+   - bzip2: another compression tool. The bzip2 tool is capable of greater compression than gzip, and includes a recovery tool, but less widely used.

In addition, Linux includes tools for viewing, searching, and comparing files compressed using gzip.