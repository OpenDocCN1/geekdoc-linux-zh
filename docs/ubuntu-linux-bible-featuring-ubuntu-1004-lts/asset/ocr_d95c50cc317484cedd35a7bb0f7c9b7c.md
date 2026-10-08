Similarly, most administrative functions on modern CUPS servers require that you contact them using SSL (i.e., a URI that begins with https). You can either disable this requirement by commenting out the lines in cupsd.conf file that contain the word Encryption or use SSL. When using SSL, you may need to create an exception for the default SSL certificate because this is a self-signed certificate that is not guaranteed by any recognized certificate authority. You will also have to do this on every system that you want to use with the CUPS server's Web-based interface. Your browser will walk you through the steps to create an exception for your printer's certificate.

# Handling Preformatted Print Jobs

Another common update-related problem may arise if you receive an update that changes how CUPS handles types of incoming print jobs. If you are printing from a remote system, such as a Windows Windows or Mac OS X system, system performs the print jobs before sending them to the printer. If printing suddenly stops after an update and you see error messages in the error_log file about raw input, make sure that the following entry is in the file /etc/cups/mine.types and is not preceded by a hash mark (#):

```
application/octet-stream
```

The hash mark is a comment character in CUPS configuration files. This entry must be present for preformatted print jobs to be received via HTTP and sent to the printer.

After making any changes to any CUPS configuration file, you need to restart the CUPS daemon on your system using the following command:

```
sudo /etc/init.d/cupsys restart
```

# Getting Information About CUPS

As you have probably guessed, CUPS configuration is either extremely rich and powerful or extremely irritating — and usually both. The CUPS configuration file /etc/cups/cupsd.conf has so many possible options that make even the command-line gcc, is and tar commands jealous. If you try to do anything with CUPS beyond the simple print server described in this chapter, you will get more information. The following are some excellent sources of additional information about CUPS:

+   * www.cups.org/documentation.php: The online documentation for CUPS that is available from Easy Software, Inc.
* www.linuxprinting.org: Specializing in help with printing on GNU/Linux systems, this site features a very useful database of printers that are to work with Linux (www.linuxprinting.org/printer_list.cgi) and a good deal of useful