+   Open a Terminal window on the local computer.

+   Allow access for the remote computer (for example, `remote1`) to the local X display by typing the following from the Terminal window:
+   ```
+   $ xhost +remote1
+   ```
+   `remote1` being added to access control list

+   Log in to the remote computer using any remote login command. For example:
+   ```
+   $ telnet -l user remote1
+   Password:
+   ```
+   Replace *user* with the name of the user login that you have on the remote computer. You will be prompted for a password.

> **NOTE:** By default, the telnet service is not enabled in Red Hat Linux. The server (in this example, `remote1`) must consider the security consequences of enabling remote login services.

+   Type the password for the remote user login. (You are now logged in as the remote user in the Terminal window.)

+   Set the DISPLAY variable on the remote computer to your local computer. For example, if your computer were named `pine` in the local domain, the command could appear as:
+   ```
+   $ export DISPLAY=pine:0
+   ```
+   (If you are using a csh shell on the remote system, you may need to type `setenv DISPLAY pine:0:`)

+   At this point, any X application you run from the remote system from this shell will appear on the local display. For example, to run a remote Terminal window so that it appears locally, type:
+   ```
+   $ xterm -title "Terminal from Remote1"
+   ```
+   The Terminal window appears on the local display with *Remote1* in the title bar.

> **TIP:** As a rule, I use the -title option when I run remote X applications. In the title, I try to indicate the remote computer name. That way, I am reminded that the application is not running locally.

You need to remember some things about the remote application that appears on your display:

+   If you only use the login to run remote applications, you can add the line exporting the DISPLAY variable to a user configuration file on the remote system (such as .bashrc, if you use the *bash* shell). After that, any application that you run will be directed to your local display.

+   Even though the application looks as though it is running locally, all the work is being done on the remote system. For example, if you ran a word processing program