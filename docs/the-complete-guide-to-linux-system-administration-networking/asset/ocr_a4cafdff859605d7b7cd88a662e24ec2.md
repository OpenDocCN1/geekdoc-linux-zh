Most Linux distributions use a “super print filter” or magic filter that can convert documents into formats for many different printers. This makes it convenient to support hundreds of printers on Linux, but it doesn’t generally allow Linux to use the specialized features of each printer. For example, if you have used expensive laser printers on Microsoft Windows systems, you have seen graphical configuration utilities that let you access and configure dozens of features for your particular printer. Few manufacturers are yet providing such tools for Linux (one exception from Hewlett-Packard is mentioned in the next section), though the Linux printing architecture makes it easy to use such tools when they appear.

Red Hat Linux and Fedora are both good examples of how most Linux distributions handle print filters. When you configure a print queue (as described in the next section), the configuration utility lets you select a printer from a list of supported devices. The printer model that you select is stored in the printer configuration file and used to direct the print filter.

The main print filter in Red Hat Linux and Fedora is a script called /usr/share/printconf/util/mf_wrapper. You can view this script in any text editor, but don’t alter it! This script starts the magicfilter-t program with a parameter describing the printer for which output should be generated. To see some of the details behind magicfilter-t, enter this command:

```
$ magicfilter-t --dump
```

The magicfilter-t program (sometimes just called the magic filter) accepts many different printing options and produces output for many different printers. You see the list of printers that the magic filter supports as you configure a printer in the next section. The magic filter uses several other programs such as gs, enscript, and newsprint, to convert documents for various formats.

![](bbox=[0.12, 0.8, 0.18, 0.9])

Another popular tool that manages filtering for multiple printer models is foomatic. You can learn more about this program at www.linuxprinting.org.

Besides not having access to all printer features, using multiple interpreted programs to convert each print job to the appropriate page description language is much slower than a single dedicated program. Later in this section you learn about PostScript Printer Description (PPD) files, which are a great improvement on the print filter system described here, but which LPRng does not use.