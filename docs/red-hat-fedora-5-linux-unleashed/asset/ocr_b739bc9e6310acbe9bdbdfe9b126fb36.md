Here is a short list of advice for moving smoothly through the installation process on a Fedora system (this list assumes that you are performing an installation as the root user and are reading the TWiki installation instructions from the TWiki website):

+   * You need to create the directory `/home/httpd/twiki`; `unzip TWiki` into this directory.
+   * The installation instructions mention the file `/etc/httpd/httpd.conf`. For Fedora, this file is found at `/etc/httpd/conf/httpd.conf`. You simply copy and paste the entries shown in the example supplied by the downloaded instructions.
+   * The path to Perl for Fedora is `/usr/bin/perl`.
+   * Fedora Core runs CGI scripts as the user `apache`, not the user `nobody`, as assumed in the default TWiki installation. You can browse to `http://localhost/twiki/bin/testenv` and read the warnings that are displayed onscreen. This is a special script run on your local machine to help you diagnose any problems with your installation. The messages should be specific to your installation, and any warning should be accompanied by a suggestion about how to fix the problem.

The TWiki installation directions suggest setting permissions and changing ownership. For Fedora, the permissions are set correctly, but the ownerships are wrong. To change the ownerships, implement the following steps (after each step, you should reload the `http://localhost/twiki/bin/testenv` page to check your progress):

+   1. Change the group ownership of everything to `apache`, but change the group ownership of `/httpd/twiki/templates` back to `root`:
+      ```
+      # chgrp -r apache /home/httpd
+      # chgrp -r root /home/httpd/twiki/templates
+      ```
+   2. Remember to edit `/home/httpd/twiki/lib/TWiki.cfg` to reflect your own domain name instead of `http://your.domain.com`.
+   3. Change the ownership of the RCS repository files to the user `apache`:
+      ```
+      # cd /home/httpd/twiki/data
+      # perl -pi -o 's/nobody/apache:/' *.v
+      ```

After you complete the installation, you should have a “virgin” TWiki installation that you can view at `http://localhost/twiki/bin/view`. As with any application, you need to further configure this file so that it suits your needs. The TWiki documentation explains the many configuration options and processes available to you. This documentation is included in the TWiki installation you just completed.