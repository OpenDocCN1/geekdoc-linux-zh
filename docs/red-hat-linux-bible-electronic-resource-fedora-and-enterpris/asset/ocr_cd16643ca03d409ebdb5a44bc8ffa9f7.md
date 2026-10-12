+   - Access to WineX support forums.
+   - Ability to vote on which games you want TransGaming to support next.
+   - Subscription to the WineX newsletter.

Source code for WineX is should be available in the near future if you want to build your own WineX package. To check availability, try the SourceForge.net project site for WineX (sourceforge.net/projects/winex).

# Loki Software game demos

To encourage people to get to know their games, Loki offered a demo program that let you choose from among more than a dozen of its games to download and try. Although Loki Software, Inc. is no longer in business, you can still find some of its games for sale. For example, a recent search for “Loki” at Amazon.com turned up 16 different Loki games (including the ones described here), with many selling for $9.99.

> **WARNING:** If you try to download any of the demos described in the next sections, make sure you have plenty of disk space available. It is common for one of these demos to require several hundred megabytes of disk space.

The Loki Demo Launcher for downloading demos is still available from the Demo Launcher page (www.lokigames.com/products/demos.php3). From that page, there are links to FTP sites from which you can download the Demo Launcher. (If that page is gone, try ftp://david.hedbor.org/loki/demos.) The file that you want to save is loki_demos-full-1.0e-x86.run. Save it to a directory (such as /tmp/loki) and do the following:

+   1. Change to the directory where you downloaded the demo. For example:
+   ```bash
+   # cd /tmp/loki
+   ```

> **NOTE:** You may not need to be root user to install these games. However, the default paths where the Demo Launcher tries to write by default are only accessible to the root user.

+   2. As root user, run the following command (the program may have a different name if it has been updated):
+   ```bash
+   # sh loki_demos-full-1.0e-x86.run
+   ```
+   
+   If you have not used the Demo Launcher before, a screen appears asking you to identify the paths used to place the Install Tool.

+   3. If the default locations shown are okay with you, click Begin Install.
+   
+   Assuming that there was no problem writing to the install directories, you should see an Install Complete message.