Don't forget to use the appropriate filename, because your version or architecture might be different from what was just described.

Logging is very important for FTP service, because you want to be able to tell who is doing what with your files. The **wu-ftpd** server logs transfers into the `xferlog` file, which typically resides in the `/var/log` directory. You can customize logging by using the `log` commands and `log transfers` keywords discussed earlier.

If you are interested in monitoring `xferlog` on a regular basis, try **Dumpxfer**, which you can download from `ftp://ftp.microimages.com/tools/dumpxfer.1.2.tar.gz`.

# # Using a Commercial FTP Server

The **wu-ftpd** server is free and provides reasonably good configurability when it comes to providing standard FTP service. However, **wu-ftpd**'s performance is deficient under heavy loads and does not have a very clean and customizable virtual FTP service solution. If you need a high-performance FTP server and don't mind paying for it, consider the **NcFTPd** package, a commercial FTP server that has the following interesting features:

+   - Does not run via `inetd` and therefore has much better startup performance than **wu-ftpd**. The `inetd`-based processes were never intended for high performance.

+   - Built-in directory listing capabilities, whereas **wu-ftpd** has to form an `ls` process per directory listing request. Thus, **NcFTPd** is better at handling directory listings. It can even cache directory listings in memory to provide faster transfer of such listings in a high-volume FTP site.

+   - Highly configurable virtual hosting capabilities. Each virtual host can have its own welcome message, anonymous FTP directory tree, password authentication scheme, user limit, and log files.

Try out this commercial FTP server by downloading it from `http://www.ncftp.com/download/`.

**NcFTPd** is free for educational organizations with certain top-level domains, such as `.edu` and `.us`.