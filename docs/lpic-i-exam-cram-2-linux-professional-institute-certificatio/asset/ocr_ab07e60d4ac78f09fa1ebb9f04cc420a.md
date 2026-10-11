+   ▶ `sn`—The shell used by filters; it defaults to `/bin/sh.`
+   
+   ▶ `lp`—The device or pipe that data is sent to (for local system printers).
+   
+   ▶ `if`—The filter used on each file (much like a printer driver).

The `printcap` file’s entries each describes a particular printer. As shown in the previous example, entries are typically broken up into many individual lines, each of which contains a setting and the value(s) that corresponds to that setting. The use of the backslash character at the end of these lines simply means to begin the next field on the next newline. A `printcap` entry could be one long line of fields, but that would be difficult to parse for humans.

Red Hat and Debian differ on what you can use to configure printers. The Red Hat distribution has had many changes in what is used as a tool to add and remove printers, including `printconf`, `printtool`, and recently the duo of `redhat-config-printer-tui` and `redhat-config-printer-gui`.

Debian, on the other hand, defaults to an editor for its printer configuration, unless you’re running X or not using the `lpr` or BSD-style of printing—for instance, if you’re using Common Unix Printing System (CUPS).

> **NOTE** We don’t cover either CUPS or LPD in this discussion; they are both excellent but beyond the scope of this book.

# ### Remote Printing Entries

When you are printing to another host across the network, the same set of tools and daemons is present; however, some are on another machine, such as in Figure 16.2.

![](bbox=[0.06, 0.74, 0.82, 0.89])

As you can see, the host on the left is submitting a print job and the process is the same as the process shown in Figure 16.1, but it has been simplified for readability.