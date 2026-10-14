Manually adjust the print filter configuration files to add any special settings. Every queue has its own separate configuration file `/etc/lpdfilter/queue/conf` (replace queue here with the actual queue name), which also contains information on each option.

# Adding Special Settings to the Print Filter

+   1. If the print data is not in PostScript format, it is, by default, converted to PostScript using `/usr/lib/lpdfilter/filter/type2ps` (replace type with the actual type of data to be printed). If there an appropriate script saved to `/etc/lpdfilter/queue/type2ps` (replace queue with the actual queue name and type with the actual type of data to be printed), the script will be used to convert the data to PostScript. This script receives the print data from stdin and sends PostScript to stdout.
+   
+   2. The PostScript data can be reformatted if there is an appropriate script in `/etc/lpdfilter/queue/pre`. You can also add your own PostScript preloads using a script for this purpose. This script receives PostScript data from stdin and sends the PostScript output to stdout. Programs for reformatting PostScript data can be found in the package `psutils`. `pstops`, in particular, features extensive reformatting functions. Refer to the man page for pstops (man `pstops`) for more information on this.
+   
+   3. Special Ghostscript parameters: The parameters for running Ghostscript are saved to the `/etc/lpdfilter/queue/upp` file when configuring with YaST2. Special Ghostscript parameters can also be added manually to this file. See Section *A Little About Ghostscript* on page 215 for more information about Ghostscript parameters.
+   
+   4. The output of Ghostscript can also be reformatted if an appropriate script is located in `/etc/lpdfilter/queue/post`. This script receives the Ghostscript output from stdin and sends the printer-specific data to stdout.

# A Hardware-Independent Example

Suppose you want a queue called `test` to print out ASCII text with numbered lines and with two pages reduced to fit on one. Then, you could create the scripts `/etc/lpdfilter/test/ascii2ps` and `/etc/lpdfilter/test/pre`:

```
```bash
#!/bin/bash
cat -n - | a2ps -1 --stdin=',' -o -
```
```