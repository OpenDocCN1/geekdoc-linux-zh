a set of definitions as part of the main CUPS package or in an add-on package, such as cups-drivers, without explicit instruction. In either of these cases, you're set and need not do anything else. If you start configuring printers and can't find your model, though, you should look for an additional printer definition set from one of the preceding sources.

# Using the Web-Based CUPS Utilities

CUPS uses a network printing protocol known as the Internet Printing Protocol (IPP), which is closely related to the Hypertext Transfer Protocol (HTTP) used on the Web. The protocol is so similar, in fact, that you can access a CUPS daemon by using a Web browser. You need only specify that you want to access the server on port 631—the normal IPP printer port. To do so, enter http://localhost:631 in a Web browser on the computer running CUPS. (You may be able to substitute the hostname, or access CUPS from another computer by using the other computer's hostname, depending on settings in the cupsd.conf file in /etc/cups.) This action brings up a list of administrative tasks you can perform. Click Manage Printers to open the printer management page, shown in Figure 6.4.

# **FIGURE 6.4**	CUPS provides its own Web-based configuration tool.

![](bbox=[0.22, 0.46, 0.85, 0.9])