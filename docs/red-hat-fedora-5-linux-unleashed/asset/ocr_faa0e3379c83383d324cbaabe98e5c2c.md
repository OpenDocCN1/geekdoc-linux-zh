There are many approaches to providing your own PPP service. IP addresses can be assigned dynamically, or a static IP address can be doled out for a user. For example, `/etc/ppp/options.ttyS1` could contain
`192.168.1.1 192.168.1.20::192.168.1.10`

In this example, the first IP address is for the host computer, whereas the second IP address is assigned to the remote user. For details about configuring PPP for Linux, read the `pppd` man page or documentation under the `/usr/share/doc/pppd*` directory. If you’re a Linux developer, browse the source code files `ppp_async.c`, `ppp_deflate.c`, `ppp_generic.c`, and `ppp_synctty.c` under the `/usr/src/linux-2.6/drivers/net` directory.

# SAVING EVEN MORE BANDWIDTH

If you elect to use a dial-in server, one of the problems you face when using it is that you are using a telecommunications network with narrow bandwidth. Would it not be nice if you could strip out all the advertising images and compress the HTML pages before sending them over the modem? Here’s how it can be done:

One approach is to use the Fedora-supplied `privoxy` proxy server or `squid` proxy server to filter ads and the `Z::proxy` (`http://zproxy.sourceforge.net`) server to convert the images to smaller, low-quality images and compress the HTML pages before sending them on to the dial-in user. A Red Hat 9 version is available at `http://www.cs.mit.edu/people/wang/zproxy-1.2.R9.tgz`, as well as a statically compiled version (requires no additional files) at `http://aleron.d1.sourceforge.net/zproxy/zproxy-1.2b-static-i586.tar.bz2`. Z::proxy requires a library not provided by Red Hat or Fedora, `libconfuse` (available at `http://www.nongnu.org/confuse/`), where you will test a `src.rpm` file to compile on your system; refer to Chapter 8, “On the Internet: Surfing the Web, Writing Email, and Reading the News,” for information on compiling source RPM files.

Another approach is to use Rabbit (`http://www.klekheuer.org/rabbit/`), a Java web proxy server that handles both tasks. The site mentions that 2.9MB of original data was compressed to 1.3MB and transmitted in 17 minutes instead of 75 minutes, a considerable saving. The site offers a Getting Started link on the main page describing downloading, installing, configuring, and using the application.

Both applications require ImageMagick to be installed to use the `convert` function to process images into low-resolution version to save bandwidth.

# RELATED FEDORA AND LINUX COMMANDS

You will use these commands when managing network connectivity in your Fedora system:

+   - `dhclient`—Automatically acquire, and then set IP info for a NIC
+   - `ethereal`—GNOME graphical network scanner
+   - `gnome-lokkit`—Fedora’s basic graphical firewalling tool for X
+   - `ifconfig`—Displays and manages Linux network devices
+   - `iwconfig`—Displays and sets wireless network device parameters
+   - `lokkit`—Fedora’s basic graphical firewalling tool