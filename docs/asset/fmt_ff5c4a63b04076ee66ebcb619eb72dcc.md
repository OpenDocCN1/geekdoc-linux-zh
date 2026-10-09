
Verify with `ls -l /var/spool/cups`—you should see `device for PDF: cups-pdf:` as part of the output. Or, if you plug in a real printer, it should be auto-detected. (If not, then it would be easier to print to PDF for the purposes of this lab.)

Finally, check where your files should be printed: `grep "OutputFile" /etc/cups/cups-pdf.conf`.

You may see something like `${HOME}/PDF` as the directory where your “printed” files will end up. You can change this if you like; if you do, finalize it with `sudo systemctl restart cups`
