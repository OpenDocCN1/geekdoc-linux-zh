# # Web Servers: Apache

Linux distributions provide several Web servers for use on your system. The primary Web server is Apache, which has almost become the standard Web server for Red Hat Linux and Fedora distributions. It is a very powerful, stable, and fairly easy-to-configure system. Other Web servers are also available, such as Tux. Tux is smaller, but very fast, and is very efficient at handling Web data that does not change. Red Hat and Fedora Linux provide default configurations for the Web servers, making them usable as soon as they are installed.

Apache freely supports full secure shell encryption using OpenSSL. There are also private cryptographic products available only with licensing fees. Instead of obtaining the licensing directly, you can simply buy a commercial version of Apache that includes such licensing such as Stronghold and Raven (www.covalent.net). Formerly, this kind of restriction applied to the use of RSA technology only in the United States, where it was once patented. The RSA patent has since expired, and RSA is now available for use in freely distributed products like OpenSSL.

# ## Tux

Tux, the Red Hat Content Accelerator, is a static-content Web server designed to be run very fast from within the Linux kernel. In effect, it runs in kernel space, making response times much faster than standard user-space Web servers like Apache. As a kernel-space server, Tux can handle static content such as images very efficiently. At the same time, it can coordinate with a user-space Web server, like Apache, to provide the dynamic content, like CGI programs. Tux can even make use of a cache to hold previously generated dynamic content, using it as if it were static. The ability to coordinate with a user-space Web server lets you use Tux as your primary Web server. Anything that Tux cannot handle, it will pass off to the user-space Web server.

> **NOTE** Tux is freely distributed under the GNU Public License and is included with many distributions.

The Tux configuration file is located in /proc/sys/net/tux. Here you enter parameters such as serverport, max_doc_size, and logfile (check the Tux reference manual at www.redhat.com/docs/manuals/tux for a detailed listing). Defaults are already entered; serverport, clientport, and documentroot are required parameters that must be set.