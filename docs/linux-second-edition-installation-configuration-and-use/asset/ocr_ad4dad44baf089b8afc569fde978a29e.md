# 484 COMMAND REFERENCE

-u or --update
extends the archive with new or modified files. This option cannot be used for compressed archives. Caution: the archive will get larger and larger, because already existing files are not overwritten. The new files are appended to the end of the archive.

-x or --extract
extracts the specified files from the archive and copies them into the current directory. The files are not deleted from the archive.

# Options

-C directory
extracts the files into the specified (instead of the current) directory.

-f file
uses the specified file as the archive (instead of accessing the streamer).

-I
compresses or uncompresses the whole archive with bzip2. See -z.

-L n or --tape-length n
specifies the capacity of the streamer in Kbytes. When the size of the archive exceeds the capacity, tar requests the magnetic tape to be changed.

-N date or --after-date date or --newer date
only archives files which are more recent than the specified date.

-T file or --files-from file
arch or extracts the file names specified in the file.

-v or --verbose
displays all file names on screen during processing. When -v is used in combination with the t command, additional information about the files is displayed (file size, and so on).When the option is specified twice, the information comes more extensive.

-w or --verify
checks the correctness of the archived files immediately after writing. Cannot be used for compressed archives.

-z or --gzip
compresses or uncompresses the whole archive with gzip. This option is useful for creating *.tgz files, but if data is actually to be stored on a streamer, this option may be dangerous:

One single error on the tape can invalidate the whole archive. (Files are destroyed without compression, but usually damage is much more limited.) DAT streamers are themselves capable of compressing the data to be processed (this is faster, but not as efficient as gzip). The -z option is incompatible with the tar versions of most other Unix dialects.