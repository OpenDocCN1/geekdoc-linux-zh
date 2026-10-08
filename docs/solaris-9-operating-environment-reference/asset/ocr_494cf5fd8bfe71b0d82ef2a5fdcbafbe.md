# 407

The outpattern determines the resulting mapped file name. The sequences $1, $2, ..., $9 are replaced by any value resulting from the inpatterntemplate. The sequence $0 is replaced by the original file name. Additionally, the sequence [seq1,seq2] is replaced by seq2 if seq1 is not a null string; it is replaced by seq2.

For example, the command mmap $1,$2 $3 [$1], [$2] yields the output file name myfile.data for input file names myfile.data and myfile.old; myfile.file for the input file name myfile.data and myfile.myfile for the input file name myfile. You can include space characters in outpattern, as in the example mmap $1 | sed "s*/*/" ,, characters.

ntrans [outchars]

Set or unset the file-name character translation mechanism. If you specify no arguments, the file-name character translation mechanism. If you specify arguments, translate characters in remote file names during mput and put commands issued without a remote target file name, and translate characters in local file names during mget and get commands issued without a specified local target file name.

The ntrans command is useful when connecting to a non-UNIX system remote host with different file-naming conventions or practices. Characters in a file name matching a character in inchars are replaced with the corresponding character in outchars. If the character's position in inchars is longer than the length of outchars, delete the character from the file name.

You can translate only 16 characters when using the ntrans command over ftp. Use case if you need to convert the entire alphabet.

open host [port]

Establish a connection to the specified host FTP server. You can supply an optional port number, in which case, ftp contacts an FTP server at that port. If the auto-login option is on (default setting), ftp tries to automatically log the user in to the FTP server.

prompt

Toggle interactive prompting. Interactive prompting occurs during multiple files to enable you to selectively retrieve or store files. By default, prompting is turned on. If you try prompting off, anyget transfers all files, and any mdelete deletes all files.

proxy ftp-command

Execute an FTP command on a secondary control connection. The proxy command allows simultaneous connection to two remote FTP servers for transferring files between the two servers. The first proxy command should be an open, to establish the secondary control connection. Enter the command proxy ? to see other FTP commands executable on the secondary connection.