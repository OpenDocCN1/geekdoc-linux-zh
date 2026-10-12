The lpr command has a variety of options that enable lpr to interpret and format several different types of documents. The following are options that you can use on the command line and the types of text those options can process:

+   * **-c** — Processes ciplot data.
+   * **-d** — Processes TeX data in DVI format.
+   * **-f** — Interprets the first character of each line as a standard FORTRAN carriage control character.
+   * **-g** — Processes plot data.
+   * **-l** — Processes content so that control characters can print and page breaks are suppressed.
+   * **-n** — Processes data in ditroff (device independent troff) format.
+   * **-t** — Processes data produced by troff commands.
+   * **-v** — Processes raster images for devices such as the Benson Varian.

The following lpr options are available for handling the print job itself:

+   * **-m** — Sends mail after the job has been printed.
+   * **-r** — Removes the file after it has been spooled.
+   * **-s** — Uses a symbolic link to obtain the file to print, instead of copying the file to a spool directory. This prevents very large print jobs from taking up space in the print queue. If you do this, however, you must be sure not to delete the original file until after it has been printed.
+   * **-#n** — Replace the n with a number representing the number of copies you want to print.

A burst page can be printed with each document to identify its contents and owner. Here are several options that you can use that relate to the burst page:

+   * **-h** — Suppresses output of a burst page.
+   * **-C class** — Identifies a job classification to use on the burst page. Replace class with a word or words to appear on the page. This value replaces the host name that is usually printed here.
+   * **-J job** — Identifies a job name to appear on the burst page. The value of job replaces the name of the first printed file on the burst page.
+   * **-P printer** — Identifies the printer to which the print job will be sent. Without the -P option, the default printer is used.
+   * **-U user** — Identifies the user name that is to appear on the burst page.