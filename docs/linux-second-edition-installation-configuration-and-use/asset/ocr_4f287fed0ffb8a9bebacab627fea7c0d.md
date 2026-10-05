# 446 COMMAND REFERENCE

/bin/csh. csh modifies the file /etc/passwd by entering the new shell. The shell of any other user can only be changed by root (whereas each user can arbitrarily change his/her own shell).

# cksum file

cksum determines the checksum and the length of the file in bytes. The checksum can be used to find out quickly and reliably verify whether two files are identical (for example, after a data transmission via a modem or when a virus infection is suspected). cksum supplies more reliable results than the related sum command.

# clear

empties the screen (the text console). The command corresponds to the DOS command cls.

# cmp [options] file1 file2

cmp two files byte by byte and supplies the position of the first discrepancy. When the files are identical, the command does not display any message at all (see also diff on page 451).

+   -c --show-chars
displays the first character in each file where the files differ from one another.
-l --verbose
supplies a list of all discrepancies.

# compress [options] file

compress compresses or decompresses the specified file. Compressed files are indicated by .2 appended to the file name. A more powerful command than compress is gzip (see page 460).

+   -d
decompresses the specified file instead of compressing it (corresponds to uncompress).

# cp [-options] source target
cp [-options] files target_directory

cp is used to copy files. Single files can be renamed. When several files are processed (for example, through the specification of wildcards), these can only be copied to a different directory, but not renamed. Instructions of the type *.tex *.bak are not allowed. Commands comparable to cp are mv for moving and renaming files, and ln for the creation of links. Amongst others, cp supports the following options: