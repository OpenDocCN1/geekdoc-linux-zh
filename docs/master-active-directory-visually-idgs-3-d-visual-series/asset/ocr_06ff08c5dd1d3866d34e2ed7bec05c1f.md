![](bbox=[0.0, 0.13, 0.08, 0.22])

# Should I change the statistic update time?

The default time is ten minutes, which gives you accurate information about the WINS server’s performance. You can lower the time if desired, but this causes the server to do more update checks. If you increase the time, you may not receive as accurate statistical information as desired. The default setting is best, so make sure that you have a specific reason to change it before doing so.

# Should I have the server back up the database each time it shuts down?

Using the General tab in the Properties dialog box, you can tell the WINS server to back up the database every time the server shuts down. This option is not enabled by default, but it is a good safety measure. This action, however, may slow the time it takes to shut down the server.

![](bbox=[0.0, 0.5, 0.48, 0.8])

![](bbox=[0.5, 0.5, 0.98, 0.8])

# CHANGING THE STATISTIC UPDATE TIME

+   1. Choose **Action**➔**Properties**.

+   2. On the **General** tab, use these boxes to change the statistic update time.
+   3. Enter a location for the backup path.
+   4. Or use the **Browse** button to browse for the location.
+   5. Click here to back up the database every time the server shuts down.