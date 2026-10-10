can do in various ways, ranging from available disk space to limits on the types of web scripting you can perform. When you control the server, you can configure it precisely the way you want. Your own web server may also be more convenient if you want to tie it to other systems—for instance, linking a web site to an internal database. Another advantage of running your own web server is that you can configure it for purely internal use.

> **Note**
> *Some of the advantages of running your own web server relate to very advanced uses. Such uses are beyond the scope of this book. To learn more, consult a book on Apache, such as Arnold’s Administering Apache (Osborne, 2000).*

# ## Web Servers for FreeBSD

Although Apache is by far the most popular web server for FreeBSD, it’s not the only one. Some of the more popular options include

+   ■ **Apache** As noted, Apache is the most popular web server for UNIX systems generally, and for FreeBSD in particular. Apache is a complex and powerful server, but its basic configuration when first installed is reasonable for small sites. Thus, despite its power and complexity, it’s also the easiest web server to use for a simple site. The main Apache web site is http://httpd.apache.org.
+   
+   ■ **Roxen** This web server is a strong competitor to Apache in features and overall power. It’s designed for large web sites with advanced needs. You can learn more about it at http://www.roxen.com.
+   
+   ■ **thttpd** The Tiny/Turbo/Throttling HTTP Server (http://www.acme.com/software/thttpd/) is, as its expanded name suggests, designed to be small (about 50KB, versus about 330KB for Apache) and fast. This server’s small size helps it handle busy sites on limited hardware.
+   
+   ■ **Mithopd** This server, like thttpd, is designed to be small and fast, but its emphasis lies more in efficiently handling a large number of connections. Its main web site is http://www.mithopd.org.
+   
+   ■ **Boa** This is yet another small web server. It’s especially popular in embedded applications—that is, computers built into devices that aren’t traditional workstation or server computers, such as gas pumps or household appliances. You can read more at http://www.boa.org.
+   
+   ■ **Specialized tools** Some servers aren’t usually thought of as web servers, but they use HTTP on ports reserved for themselves. This feature allows these tools to be used with ordinary web browsers, thus obviating the need to design specialized clients. Examples include the Samba Web Administration Tool (SWAT), which provides GUI administration for Samba; and the Webmin system administration tool (http://www.webmin.com).