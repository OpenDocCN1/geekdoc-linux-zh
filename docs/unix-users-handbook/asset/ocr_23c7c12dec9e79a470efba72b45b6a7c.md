Note that runique does not affect local files generated from a shell command (see below). The default value is off.

send local-file [remote-file]
A synonym for put.

sendport
Toggle the use of PORT commands. By default, ftp attempts to use a PORT command when establishing a connection for each data transfer. If the PORT command fails, ftp uses the default data port. When the use of PORT commands is disabled, ftp makes no attempt to use PORT commands for each data transfer. This is useful for certain FTP implementations that ignore PORT commands but (incorrectly) indicate that they've been accepted. See ftpd(1M). Turning sendport off may cause delays in the execution of commands.

site arguments
Send arguments, verbatim, to the server host as a SITE command. See ftpd(1M).

size remote-file
Show the size of remote-file.

status
Show the current status of ftp.

struct [struct-name]
Set the FTP file transfer struct to struct-name. The only supported struct is file.

sunique
Toggle storing of files on remote machine under unique file names. The remote server reports the unique name. By default, sunique is off.

system
Show the type of operating system running on the remote machine.

tenex
Set the FTP file transfer type to tenex.

type [type-name]
Set the FTP file transfer type to type-name. If type-name is unspecified, write the current type to stdout. Ascii, binary, and tenex are the types currently supported.

umask [newmask]
Set the default umask on the remote server to newmask. If newmask is omitted, the current umask is printed.

user user-name [password] [account]
Log into the server host on the current connection, which must already be open. A .netrc file in the user's local home directory can provide the user-name, password, and optionally the account; see netrc(4). Otherwise ftp prompts the user for this information. The HP-UX FTP server does not require an account. For security reasons, ftp always requires a password. It does not log into remote accounts that do not have a password.

verbose
Toggle verbose output. If verbose output is enabled, ftp displays responses from the server host, and when a file transfer completes it reports statistics regarding the efficiency of the transfer.