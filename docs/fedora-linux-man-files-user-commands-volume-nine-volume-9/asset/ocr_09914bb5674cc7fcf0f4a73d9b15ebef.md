# ## DESCRIPTION

**sftp** is an interactive file transfer program, similar to \(1\), which performs all operations over an encrypted \(1\) transport. It may also use many features of *ssh*, such as public key authentication and compression. **sftp** connects and logs into the specified *host* then enters an interactive command mode.

The second usage format will retrieve files automatically if a non-interactive authenitcation thod is used; otherwise it will do so after successful interactive authentication.

The third usage format allows **sftp** to start in a remote directory.

The final usage format allows for automated sessions using the **-b** option. In such cases, it is necessary to configure non-interactive authentication to obviate the need to enter a password at connection ti (see \(8\) and *ssh-keygen1* for details).

Since so usage formats use colon characters to delimit host nas from path nas, IPv6 addresses st be enclosed in square brackets to avoid aiguity.

The options are as follows:

+   * **-l**  
+       Specify the use of protocol version 1.

+   * **-2**  
+       Specify the use of protocol version 2.

+   * **-4**  
+       Forces **sftp** to use IPv4 addresses only.

+   * **-6**  
+       Forces **sftp** to use IPv6 addresses only.

+   * **-a**  
+       Attempt to continue interrupted transfers rather than overwriting existing partial or complete copies of files. If the partial contents differ from those being transferred, then the resultant file is likely to be corrupt.

+   * **-B** *buffer_size*  
+       Specify the size of the buffer that **sftp** uses when transferring files. Larger buffers require fewer round trips at the cost of higher mory consumption. The default is 32768 bytes.

+   * **-b** *batchfile*  
+       Batch mode reads a series of commands from an input *batchfile* instead of *stdin* Since it lacks user interaction it should be used in conjunction with non-interactive authentication. A *batchfile* of '` '` may be used to indicate standard input. **sftp** will abort if any of the following commands fail: **get , put , remot , remot , renm , ln m, mmdir , chdir , ls lchdir , chmod , chown chgrp , lpwd , df , synyk** and **lmkdir** Termination on error can be suppressed on a command by command basis by prefixing the command with a '` ` character (for example, **-rm /tmp/blah\*)**

+   * **-C**