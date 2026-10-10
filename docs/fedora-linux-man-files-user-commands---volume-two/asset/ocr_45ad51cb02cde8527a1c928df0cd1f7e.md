+   -**-f DIRECTORY**
+       Directory in which to write the resulting XML file. The name of the file will be the printer ID with the “.xml” extension.

+   -**-n**
+       Do not write modified versions of existing XML files, only create XML files for printers for which there is no XML file yet.

+   -**-x**
+       Create XML files independent of whether or not there are already XML files for the printers covered by the PPD. This makes the process vastly faster if you have PPD files for printers which are definitely not yet in the Foomatic database.