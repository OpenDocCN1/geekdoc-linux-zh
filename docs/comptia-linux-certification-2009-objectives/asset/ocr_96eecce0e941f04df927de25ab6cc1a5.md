+   b. Enter yum localinstall \ /rhelsource/Server/=> \ php-cli-5.1.6-23.el5.i386.rpm to install the php-cli package.

> The ⇒ symbol is used in the step only to bring the step to the next line. It is not part of the code and therefore, students need not type the symbol.

+   c. Enter yum localinstall \ /rhelsource/Server/=> \ php-5.1.6-23.el5.i386.rpm to install the php package.

> The ⇒ symbol is used in the step only to bring the step to the next line. It is not part of the code and therefore, students need not type the symbol.

+   d. Clear the terminal window.

+   3. Specify alias names for the web server.

+   a. Navigate to the /var/named directory.

+   b. Using the vi editor, open the ogc.forward file.

+   c. At the end of the file, type www IN CNAME srvA to add a CNAME record.

+   d. Press Esc to switch to the command mode.

+   e. Save and close the file.

+   f. Restart the named service.

+   g. Clear the terminal window.