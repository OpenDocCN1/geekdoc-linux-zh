ncftp is a good choice for command-line use, and AxY FTP and gFTP are good choices for GUI use.

In addition to these conventional FTP clients, there are some less conventional programs available that use FTP. Some tools are designed to _mirror_ an FTP site—that is, to copy all the files from an FTP site (or a subdirectory thereof) to your computer. You might use such a tool to copy a FreeBSD FTP site to a local computer in order to facilitate installing FreeBSD on a network of computers, for instance. Some tools that aren’t primarily FTP programs use FTP to accomplish specific goals. For instance, some web page design programs enable direct upload of files to a web server via FTP. You can find some unusual FTP clients in the ftp section of the FreeBSD packages or ports systems, but others may reside elsewhere.

# Core FTP Commands

FTP supports a specific set of operations—sending a file, receiving a file, and so on. When using a text-mode FTP client, you access these operations by typing commands. In GUI FTP clients, the typed commands are replaced by menu options, button presses, or the like. The full range of FTP commands is greater than can be presented here, but the most important commands, as used by ftp and most other text-mode FTP clients, are

+   * **ascii**  One of FTP’s strengths is that it supports two transfer modes: _binary_, in which files are transferred without modification; and _ASCII_, in which the file’s end-of-line characters, and sometimes other characters, are modified for the receiving system’s standards. The **ascii** command enables ASCII transfer mode.

+   * **binary**  As you might expect, this command enables binary transfer mode. This mode is usually, but not always, the default. You should be sure to enable binary mode before transferring nontext data files, or they’re likely to be corrupted.

+   * **bye or exit or quit**  These commands terminate the session and quit from the program.

+   * **cd**  This command works much like its namesake in most FreeBSD shells—it changes the working directory, but on the FTP server system. You specify a path (in absolute or relative form) with this command.

+   * **delete**  You can delete a file on the server with this command, which takes a filename as an option.

+   * **dir or ls**  These commands display the contents of a directory on the server. You can optionally add a directory name to see the contents of the directory you specify. On some servers, the dir command creates a longer listing (similar to what ls -l does in a shell), whereas ls creates a more compact listing.

+   * **ftp or open**  These commands open a new connection. You specify a hostname after these commands, as in `open ftp.threeroomco.com`.