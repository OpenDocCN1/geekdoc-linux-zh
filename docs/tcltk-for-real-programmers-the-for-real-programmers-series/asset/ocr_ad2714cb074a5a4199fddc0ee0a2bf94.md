# Appendix D. Installing Tcl/Tk Packages

# D.12.1 Unpacking the megaWidget Distribution under Windows

The megaWidget package has been repackaged as a self-extracting zip file for the Windows users.

To unpack the self-extracting zip files:

+   Place the Tcl/Tk for Real Programmers CD-ROM in the CD-ROM drive.
Open the Run dialog box.
Enter or borse to D: \packages\mega_wid\widget09.exe. Select this as browse to the file to run.
Run the self-extracting zip file.
Click the OK button.
The next window gives you the chance to select the installation directory. You may accept the default installation directory (C:\widget) or type in the directory path you prefer.
Click the Unzip button. You will see the usual progress bar as the extension is installed.
When the installation is complete click the OK button.
Exit the installation program by clicking the Clear button.
Run the TOUR.tcl example with a command resembling C:\progra-l\tcl\bin\wish80 tour.tcl

# D.12.2 Unpacking the megaWidget Distribution under Unix

To unpack the megaWidget package on a Unix/Linux system:

+   Mount the Tcl/Tk for Real Programmers CD-ROM.
Change directory to the top of your source tree. cd /home/example/src
Unpack the widget09 source distribution. gunzip -c /cdrom/packages/mega_wid/widget09.tgz | tar -xvf - 
Change to the widget directory. cd widget
Run the TOUR.tcl example with a command resembling: /usr/local/bin/wish TOUR.tcl

676