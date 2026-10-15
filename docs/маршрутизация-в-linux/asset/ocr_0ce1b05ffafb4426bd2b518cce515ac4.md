Parts of MRTG are written in Perl, so Perl also must be installed on the system. Version 5.05 or later is recommended. Several graphics libraries also are required for MRTG to function correctly, but their installation is beyond the scope of this chapter. Refer to the doc/unix-guide.txt document (in the MRTG source directory covered shortly) for the exact requirements.

# MRTG Installation

MRTG should be downloaded from http://people.ee.ethz.ch/~oetiker/webtools/mrtg/pub/ and placed in the appropriate directory. For this example, /usr/src is used. The current version of MRTG at the time of publication is 2.9.12, which is used here.

After downloading the MRTG package, follow these steps.

+   1. Log in as root and move into the directory where the package was downloaded:
+      `[root@lefty /root]# cd /usr/src`

+   2. Unzip the distribution:
+      `[root@lefty src]# gunzip mrtg-2.9.12.tar.gz`

+   4. Untar the tarball:
+      `tar xvf mrtg-2.9.12.tar`

+   5. This will create the MRTG source tree. Move into the source tree:
+      `[root@lefty src]# cd mrtg-2.9.12`

+   6. Execute the configure script:
+      `[root@lefty mrtg-2.9.12]# ./configure`

+   7. Execute the make command:
+      `[root@lefty mrtg-2.9.12]# make`

+   8. Finally, execute the make install:
+      `[root@lefty mrtg-2.9.12]# make install`

This will create the installation directory structure, /usr/local/mrtg-2/, and move all the binaries and appropriate files into the directory. Move into the directory structure:
   `[root@lefty mrtg-2.9.12]# cd /usr/local/mrtg-2/`

MRTG needs a directory that is accessible by the web server. A common directory location for HTML documents for the Apache Web Server on Linux is /home/httpd/html/, so the MRTG files can be placed in a subdirectory:
   `[root@lefty mrtg-2]# mkdir /home/httpd/html/mrtg`

Be sure to use an appropriate directory based upon the web server's configuration. A configuration directory for MRTG also should be created:
   `[root@lefty mrtg-2]# mkdir cfg`