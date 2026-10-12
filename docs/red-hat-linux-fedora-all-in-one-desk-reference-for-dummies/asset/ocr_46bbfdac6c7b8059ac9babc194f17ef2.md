As Figure 2-2 shows, a URL has the following parts:

**Protocol:** Name of the protocol that the Web browser uses to access the data from the file the URL specifies. In Figure 2-2, the protocol is `http://`, which means that the URL specifies the location of a Web page. Here are some of the common protocol types and their meanings:

+   - `file://` means the URL is pointing to a local file. You can use this URL to view HTML files without having to connect to the Internet. For example, `file:///var/www/html/index.html` opens the file `/var/www/html/index.html` from your Red Hat Linux system.
+   - `ftp://` means you can download a file using the File Transfer Protocol (FTP). For example, `ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` refers to the image file `nasa.jpg` from the `/pub/uns/NASA` directory of the FTP server `ftp.purdue.edu`. If you want to access a specific user account via FTP, use a URL in the following form:
+   
+   `ftp://username:password@ftp.somesite.com/`
+   
+   with the user name and password embedded in the URL (note that the password is in plain text and not secure).
+   - `http://` means the file should be downloaded by using the HyperText Transfer Protocol (HTTP). This is the well-known format of URL for all Web sites, such as `http://www.redhat.com` for Red Hat's home page. If the URL does not have a filename, the Web server sends a default HTML file named `index.html` (that's the default filename for the popular UNIX-based Apache Web servers; Microsoft Windows Web servers use a different default filename).
+   - `https://` specifies that the file is to be accessed through a Secure Sockets Layer (SSL) connection — a protocol designed by Netscape Communications for encrypted data transfers across the Internet. This form of URL is typically used when the Web browser sends sensitive information (such as credit card number, user name, and password) to a Web server. For example, a URL such as `https://some.site.com/secure/takeorder.html` might display an HTML form that requests credit card information and other personal information (such as name, address, and phone number).
+   - `mailto://` specifies an e-mail address you can use to send an e-mail message. For example, `mailto:webmaster@someplace.com` refers to the Webmaster at the host `someplace.com`.
+   - `news://` specifies a newsgroup you can read by means of the Network News Transfer Protocol (NNTP). For example, `news://news.md.comcast.giganews.com/comp.os.linux.setup`