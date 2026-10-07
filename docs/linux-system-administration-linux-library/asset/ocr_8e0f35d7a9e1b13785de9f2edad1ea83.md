# Configuring Printers under Red Hat 443

advantage the CUPS's unusual features. The spooer is an optional component of Mandrake 7.2. You can learn more at http://www.cups.org.

If you want to experiment with an alternative printing system, do so on a test system, at least initially. Some packages may not get well with these new systems, because their lpd compatibility is not perfect. Once you've determined that your major applications work with the new system, you can consider installing it on your main systems, possibly including any print servers you maintain.

# Alternative Filter Packages

The rhs-filters package is quite adequate for most uses. It can distinguish raw ASCII text, PostScript, various graphics files, and a handful of others. If you use these filters as your printcap file, as described earlier, the filter will manually handle the printing of any of these file types. These print filters are also integral to using a standard Red Hat print queue to print to a printer's hosted on a Windows print server. This filter package is not the only filter available for Linux, however. Alternatives:

+   - APSFilter This package aims to be a platform-neutral filter package. It handles more file formats than the standard Red Hat rhs-printfilters package. You can learn more at http://www.aps.org.

+   - Magfilter Like APSFilter, Magfilter is a full-featured filter package, which can handle more file formats than the standard Red Hat filters. The package is available from ftp://sunite.com.edu/pub/Linux/system/printing/.

Many distributions ship with APSFilter or Magfilter, so you may already be using one of them without knowing it. In most cases, switching from one filter package to another provides few benefits and many hassles, because printing systems are built from a rather long chain of programs. If one link changes something that the system stops working. Unless you've investigated your alternative package and find that it does something you're currently using doesn't, therefore, it's generally best to stick with whatever comes with your distribution.

![](bbox=[0.883, 0.574, 0.963, 0.735])

# Configuring Printers under Red Hat

Each Linux distribution includes a preferred tool to add an entry to the printcap file and create the printer's spool directory under /var/ spool/lpd. Red Hat uses a program called Printtool. This GUI tool, shown in Figure 13.2, creates entries for the /etc/printcap file and provides links to the corresponding magic filters as well. You start this tool by typing printtool in an xterm.