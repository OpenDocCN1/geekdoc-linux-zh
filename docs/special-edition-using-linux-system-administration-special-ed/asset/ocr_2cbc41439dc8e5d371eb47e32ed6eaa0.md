+   3. Unpack the INN distribution archive:
+      ```
+      # tar xzvf inn-2.2.1.tar.gz
+      ```
+   4. Change your current directory to the directory created during extraction of the archive:
+      ```
+      # cd inn-2.2.1
+      ```
+   5. Create the group news:
+      ```
+      # groupadd news
+      ```
+   6. Create the user news and set the account’s home directory to `/usr/local/news/`:
+      ```
+      # useradd -g news -d /usr/local/news/ news
+      ```
+   7. Configure the INN source code for compiling with the command:
+      ```
+      # ./configure-with-perl
+      ```
+   8. The configure script will build a Makefile suited to your system to be used during compilation.
+   9. Compile the INN software:
+      ```
+      # make
+      ```
+   10. The INN source code will be compiled into binary files.
+   11. Install the compiled INN software:
+      ```
+      # make install
+      ```
+   12. The compiled binary files along with the INN man pages and other documentation will be installed in its default locations.

# GENERAL OVERVIEW OF INN

The operations performed by INN can be divided into five main areas:

+   - Receiving incoming news feeds
+   - Processing outgoing news feeds
+   - Servicing news readers and facilitating the reading and posting of articles
+   - Expiring old articles
+   - Logging all activity

When a system which runs INN boots, it starts the script `/etc/rc.d/rc.news`. This script runs as the root user and launches innnd, the INN daemon, which runs as the news user for security reasons. `rc.news` actually starts innd using the `innstart` script which opens the NNTP port, sets the port’s user ID and group ID to the news user and group, and then launches innd with the `-p` flag.