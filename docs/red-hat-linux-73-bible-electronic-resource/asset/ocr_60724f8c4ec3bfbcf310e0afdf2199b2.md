![](bbox=[0.15, 0.07, 0.75, 0.3])

![](bbox=[0.15, 0.31, 0.42, 0.38])

**Figure 8-2**: Play CDs and store artist, title, and track information with `gtcd`.

# ## Using the CD Database

By default, the player contacts the freedb.freedb.org server to get CD artist and track information from the CD Database. However, you can add the address of a different CDDB server if you choose.

To get information about the CD you are playing from the CD Database, do the following from your `gtcd` window:

+   1. Click the **Open Track Editor** button.
+   2. From the **Track Editor** window that appears, click the **CDDb Status** button.
+   3. From the **CDDb Status** window that appears, click the **Get CDDb Now** button. The CDDb Status window opens a connection to the CD Database on the Internet and tries to download artist, title, and track information for the current CD.

If the procedure is successful, information about the CD should appear in the **Track Editor** window. You will see the name of the artist, the title of the CD, and the title of each track.

> **NOTE**: You need a connection to the Internet from your Red Hat Linux system to take advantage of Internet CD databases.

# ### Playing CDs with cdp

If you are working from a dumb terminal or just don’t have your **X** desktop running, you can run the `cdp` utility (which comes with Red Hat Linux) to play CDs. I don’t suggest running