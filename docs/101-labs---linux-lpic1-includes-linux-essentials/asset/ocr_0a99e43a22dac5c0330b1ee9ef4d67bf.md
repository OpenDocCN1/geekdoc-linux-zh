
# LAB 86

## Manage Printers and Printing

**Lab Objective:**

Learn how to manage print jobs using `CUPS`.

**Lab Purpose:**

In this lab, you will learn about managing print queues and jobs using `CUPS` and the `LPD` compatibility interface.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

To eliminate variability around printer hardware and all the problems it brings (and in case you don't have a printer handy), this lab will assume printing to a PDF file instead. If you would like to print to a real printer, ignore this step. Otherwise, run `sudo apt install printer-driver-cups-pdf` (you may have to run `apt-get update --fix-missing` in order to install `cups-pdf` correctly).

Verify with `lstat -t`—you should see "device for PDF: `cups-pdf`:" as part of the output. Or, if you plug in a real printer, it should be auto-detected. (If not, then it would be easier to print to PDF for the purposes of this lab.)

Finally, check where your files should be printed: `grep "out" /etc/cups/cups-pdf.conf`.

You may see something like `${HOME}/PDF` as the directory where your “printed” files will end up. You can change this if you like; if you do, finalize it with `sudo systemctl restart cups`
