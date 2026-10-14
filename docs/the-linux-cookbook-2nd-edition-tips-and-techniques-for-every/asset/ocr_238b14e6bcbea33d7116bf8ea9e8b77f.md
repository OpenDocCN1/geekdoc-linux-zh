| X100 | DVI preview in X at 100 dpi (no output file necessary) |
| ascii | Plain text |
| latin1 | Plain text in the ISO Latin-1 character set (extended ASCII) |
| lj4 | PCL5 printer format, for HP LaserJet 4 printers and compatibles |
| html | HTML |

By default, groff writes to the standard output; to save it to a file, redirect the output.

⇒ Here are some ways to use this.

+   - To preview the contents of the GROFF file doc.ms in a new X window at 100 dpi, type:
+     ```
+     $ groff -T X100 doc.ms RET
+     ```

+   - To process the GROFF file doc.ms and send the output to an HP LaserJet 4 printer named frontoffice, type:
+     ```
+     $ groff -T lj4 doc.ms | lpr -Pfrontoffice RET
+     ```

+   - To display the first 20 lines of the document contained in the GROFF file doc.ms, ignoring any error messages, type:
+     ```
+     $ groff -T ascii doc.ms 2> /dev/null | head -20 RET
+     ```

+   - To mail the contents of the GROFF file doc.ms as plain text to the email address home@example.net, type:
+     ```
+     $ groff -T ascii doc.ms | mail home@example.net RET
+     ```

# 15.5.2 Determining the Command Line Options for a GROFF File

Some GROFF input files require command line options to be passed to groff when you process them. These options set various preprocessing flags and otherwise control how groff will typeset the document.

To determine which command line options should be used with a particular GROFF file, give the name of the file as an argument to grog, the “GROFF option generator.” This tool is part of the GROFF system, and its purpose is to determine and output the correct groff command line to use for a particular file.