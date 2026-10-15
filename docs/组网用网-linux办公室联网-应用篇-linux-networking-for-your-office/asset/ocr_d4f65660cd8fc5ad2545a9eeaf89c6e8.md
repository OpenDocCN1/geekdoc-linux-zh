3. If the printer is local to the Linux server you're configuring, choose Tests, Print ASCII directly to port. You should see a page appear from the printer. If you do not, you might need to select a different port or recompile your kernel with printer support, as described in Chapter 6, "Compiling a Kernel for Networking." (The text you get at this stage may suffer from stair-stepping, as shown in Figure 14.7, but if so, don't be concerned, since this test doesn't apply the filter that corrects for this effect.)

4. Reselect the printer, if necessary, and choose Tests, Print ASCII test page. A text test page should print. If there are problems with it, go back over your printer configuration. One common problem at this point is stair-stepped text, as shown in Figure 14.7, which can be fixed with the appropriate option on the Configure Filter dialog box.

5. Reselect the printer, if necessary, and choose Tests, Print Postscript test page. You should see a PostScript test page print, as shown in Figure 14.8. If the printer is a color model, the output should include color samples. Again, if there's a problem, you should go back to the Configure Filter dialog box and try new options to fix the problem.

It's possible that you won't get satisfactory results at this point, particularly if you have a printer that's poorly supported by Ghostscript. The Red Hat printtool utility doesn't know about all the available Ghostscript drivers, particularly drivers in the latest releases of Ghostscript or from nonstandard binaries that include extra or experimental drivers. If you find yourself in this situation, you might need to edit your printer files manually. After you're done, you can restart printtool to run the tests again.

# Tweaking the Configuration Manually

You're likely to need to edit one of two files when you edit your printer configuration manually: /etc/printcap and /var/spool/lpd/queuename/postscript.cfg, where queuename is the name of the printer queue you defined in printtool. The first of these files is common across Linux distributions, whereas the second is unique to Red Hat and similar distributions. If you're using a radically different distribution, you might need to look elsewhere to configure the printer filter, which is what the postscript.cfg file controls. Consult your distribution's documentation for more details.

# Printer printcap Entries

Here's a sample /etc/printcap entry:

```
lp:|hp4000:\n:sd=/var/spool/lpd/lp:\n::mx#0:\n:sh:\n:lp=/dev/lp1:\n:if=/var/spool/lpd/lp/filter:
```