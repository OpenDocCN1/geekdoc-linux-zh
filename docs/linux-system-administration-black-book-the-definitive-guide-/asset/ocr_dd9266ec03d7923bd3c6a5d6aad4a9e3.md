2. Unpack the tarballs into your preferred source directory—/usr/src by default.

3. Change into the new directory created for the filter source.

4. Do the following to start the automated setup and installation process:

+   - Type "/.SETUP" for **apsfilter**. This program walks you through the entire filter setup process.

+   - Type "/.configure" for **magicfilter**. Now, you need to compile the code. Type the following sequence of commands: "make" and then "make install".

> NOTE: Both of these programs alter your /etc/printcap file. Take a look to see what it did.

| Related solution: | Found on page: |
| :--- | :--- |
| Opening Or Creating Tarballs | 110 |

# ## Testing The Printer

To test your printer, which means printing raw text while skipping the print daemon, do the following:

+   1. Choose a short file that is raw ASCII text, rather than an image or word processing document.

+   2. Determine the device corresponding to the printer you want to test—it should be a local printer; do not do this test over a network.

+   3. Type `cat_file > /dev/device`. For example, "cat /root/test.txt > /dev/lp0". If the printer is hooked up properly, the file prints out. If the job does not print, check the items listed in the section "Nonsoftware Technical Problems" in the In Depth section.

# ## Printing A File

To print a file through the print daemon, do the following:

+   1. Determine which file you want to print.

+   2. Determine which printer—by one of the name listings in /etc/passwd—you want to print to.

![](bbox=[0.0, 0.64, 0.06, 0.74])