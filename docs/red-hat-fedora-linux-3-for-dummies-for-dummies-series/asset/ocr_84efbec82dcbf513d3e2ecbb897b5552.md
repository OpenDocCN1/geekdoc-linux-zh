Describing how to set up anything more than a simple Web server is beyond the scope of this book. Needless to say, you can configure Apache to provide a whole world (so to speak) of Web services. If you want to utilize the powers of Apache, consult such books as the excellent *Apache Server 2 Bible*, by Mohammed J. Kabir (Wiley).

# Installing and starting the Web server

Linux provides the ideal platform for providing Web services. The Apache Web server system — which is bundled with Fedora Core — is easy to set up and use.

Follow these steps to install and configure a basic Apache Web server:

+   1. Log in as any user and insert the companion DVD.
+   	The Apache software is on the DVD.
+   2. Click the Fedora menu and choose System Settings::Add/Remove Applications.
+   	The Query dialog box opens if you’re not already logged in as the superuser (root).
+   3. Enter the root password if you’re prompted.
+   	The Checking System Status dialog box opens and displays a progress bar while it determines which software is installed on your computer. The Add and Remove Software dialog box opens.
+   4. Scroll down and click the Web Server button.
+   5. Click the Update button.
+   	The Preparing system update dialog box opens while the package-installation utility prepares to install the software. The window title changes to Completed System Preparation when it finishes.
+   6. Click the Continue button.
+   	A dialog box labeled Updating system shows the installation progress.
+   7. Click the OK button.
+   	Control returns to the Package Management window.
+   8. Click the Quit button.

If you’re connected to the Internet, you can use YUM — the Yellowdog Updater, Modif ier (yucky acronym, but, er, yummy functionality) — to install the Apache (or any) package. YUM connects to the Fedora Core project’s download server and installs any packages you want; you can also use a Fedora Core mirror. YUM also performs other functions, such as updating