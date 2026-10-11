**Please Note**

If you do accidentally start a second copy of a tool, you should quit it immediately. Also, do not manually edit any files managed by the control-panel tools while the tools are running. Similarly, do not run any other programs (such as `linuxconf`) that may change those files while the tools are running.

# ### 3.2.1 Printer Configuration

Please note that the *Official Red Hat Linux Getting Started Guide* contains more up-to-date documentation on **printtool**, so be sure to check that document before using **printtool**.

The printer configuration tool (**printtool**) maintains the `/etc/printcap` file, print spool directories, and print filters. The filters allow you to print many different types of files, including:

+   - plain text (ASCII) files
+   - PostScript files
+   - TeX `.dvi` files
+   - GIF, JPEG, TIFF, and other graphics formats
+   - RPMs

In other words, simply printing a GIF or RPM file using the `lpr` command will result in the printer doing "the right thing."