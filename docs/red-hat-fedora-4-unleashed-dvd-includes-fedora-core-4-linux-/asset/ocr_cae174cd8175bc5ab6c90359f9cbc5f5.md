# Saving Even More Bandwidth

If you elect to use a dial-in server, one of the problems you face when using it is that you are using a connection with narrower bandwidth. Wouldn't it be nice if you could strip out all the advertising images and compress the HTML pages before sending them over the modem? Here's how it can be done:

One approach is to use the Fedora Core-supplied privoxy proxy server or squid proxy server to filter ads and the Ziproxy (http://ziproxy.sourceforge.net/) server to convert the images to smaller, low-quality images and compress the HTML pages before sending them on to the dial-in user. A Red Hat 9 version is available at http://www.ai.mit.edu/people/wang/ziproxy-1.2.rh9.tgz, as well as a statically compiled version (requires no additional files) at http://aleron.dl. sourceforge.net/sourceforge/ziproxy/ziproxy-1.2b-static.i586.tar.bz2. Ziproxy requires a library not provided by Red Hat or Fedora Core, libconfuse (available at http://www.nongnu.org/ confuse/, where you'll find a src.rpm file to compile on your system; refer to Chapter 8, "On the Internet: Surfing the Web, Writing Email, and Reading the News," for information on compiling source RPM files).

Another approach is to use RabbiT (http://www.khelekore.org/rabbit), a Java web proxy server that handles both tasks. The site mentions that 2.9MB of original data was compressed to 1.3MB and transmitted in 17 minutes instead of 75 minutes, a considerable saving. The site offers a Getting Started link on the main page describing downloading, installing, configuring, and using the application.

Both applications require ImageMagick to be installed to use the convert function to process images into low-resolution version to save bandwidth.

# Relevant Fedora Core and Linux Commands

+   * `internet-druiz`—Fedora Core's command-line name for its graphical Internet Connection Wizard.

+   * `mg tty`—An advanced serial port monitoring tool that supports data and fax modem operations with Linux.

+   * `neat`—Fedora Core's command-line name for the Network Configuration tool.

+   * `system-control-network`—Red Hat's command-line name for its graphical Network Device Control tool.

+   * `system-config-network-druiz`—Red Hat's command-line name for its Internet Connection Wizard.

+   * `system-config-network`—Red Hat's command-line name for its graphical Network Configuration tool. It offers a graphical interface and a command-line interface (when used as `system-config-network-tui`.

# Reference

http://www.tldp.org/HOWTO/Modem-HOWTO.html—The Linux Modem HOWTO provides a wealth of information. For example, Chapter 8 deals with locating your modem; Chapters 12 and 13 deal with dial-in use; Chapter 17 offers troubleshooting advice.