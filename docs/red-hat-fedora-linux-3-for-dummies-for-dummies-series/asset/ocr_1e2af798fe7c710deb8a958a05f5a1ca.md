These steps describe how to configure your Icecast2 server to broadcast over your private network:

+   1.  **Log in as root** and open the Gedit text editor by clicking the GNOME Menu and choosing **Accessories**: Text Editor.
+   2.  In the Gedit window, choose **File**: Open.
+   3.  Select /usr/local/etc/icecast.xml and click **OK**.
+   4.  Change the loopback address, 127.0.0.1, to the IP address of your Icecast2 server.
+   
+   For example, if your server's IP address is 192.168.1.1, modify the file as shown here; change the host name as appropriate too:

```
<hostname>cancun</hostname>
<!-- You can use these two if you only want a
single listener -->
<port>8000</port>
<bind-address>127.0.0.1</bind-address>

<!-- You may have multiple <listener> elements -->
<listen-socket>
  <port>8000</port>
  <bind-address>192.168.1.1
  </bind-address>
</listen-socket>
```

Note that the port number doesn't change.

+   5.  Change the source password from its default value. Otherwise, anyone who downloads the Icecast2 package can determine your password:

```
<source-password>
  givememusic
</source-password>
```

+   6.  **Modify the e-mail and location information to match your network.**
+   This step gives any listeners an idea of who you are and where you're coming from.

```
<location>Hi-Fi Paunchy</location>
<admin>olgoz@paunchy.net</admin>
```

+   7.  **Save your changes** by clicking the Save button.
+   8.  Open the **Icecast2 configuration file** — /usr/local/etc/ices-playlist.xml — in Gedit.