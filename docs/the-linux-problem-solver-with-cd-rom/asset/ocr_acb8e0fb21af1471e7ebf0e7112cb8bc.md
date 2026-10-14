# status

This fetches the printer status. Since this requires a bidirectional connection and a printer that supports status in the first place, sometimes you must turn it off.

# pagecount

In order to do accounting, you need to get page counts.

# no_ps_eoj, no_pcl_eoj

Some printers don't like the end-of-job code, which the ifhp filter sends at the beginning of each job to clear any lingering errors. Use these options to turn the code off for PostScript or PCL, as appropriate.

# Selecting Other Options with ifhp.conf

The options described above are the basic ones to start with, and they may be all you need. But what about selecting other options, such as duplex for double-sided printing? This is where a new file, ifhp.conf, comes into play.

As it turns out, the default ifhp.conf file contains a large number of prebuilt option definitions for various printers, including default settings for most HPs. Type `less /etc/ifhp.conf` (or wherever you installed ifhp.conf), then type `/ps_user_opts` to jump to a line of user options that ifhp can make available. As the first line in the file, this should also include the default settings. Look them over to get an idea of what's available, keeping in mind that your printer may not support all of them.

# Two Parts to the ifhp.conf File

The ifhp.conf file is very large and contains a tremendous amount of information, but you can divide it into two parts:

**Part 1: _Default options and definitions._** Each option is defined as a printer code for each language. For example, the `ps_duplex` definition tells you what the filter will hand to the printer when PostScript is the active language. The `pcl_duplex` definition performs a similar function for PCL.

**Part 2: _Specific printer definitions._** As in Part 1, each option is defined as a printer code, except that each printer configuration begins with a label enclosed in square brackets; for example, `[apple postscript ps]`. Search for apple in the ifhp.conf file to see this definition.

> Part 2 is where the `model=name` option becomes relevant. If you put `:ifhp::model=apple:` in any entry in your `/etc/printcap`, ifhp will search for apple in the labels and use the modifications that configuration defines.

![](bbox=[0.11, 0.808, 0.19, 0.831])