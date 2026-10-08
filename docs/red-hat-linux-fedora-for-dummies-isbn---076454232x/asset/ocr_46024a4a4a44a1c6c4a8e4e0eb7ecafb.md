+   6.  **Modify the e-mail and location information to match your network.**

That gives any listeners an idea of who you are and where you’re
coming from.

```
<location>Hi-Fi Paunchy</location>
<admin>oldgomez@paunchy.net</admin>
```

+   7.  **Save your changes by clicking the Save button and open the /usr/
local/etc/ices-playlist.xml file in Gedit.**

+   8.  **Modify the file so that Ices2 contacts the Icecast2 server:**

```
<hostname>veracruz</hostname>
<port>8000</port>
<password>givememusic</password>
<mount>/track1.ogg</mount>
```

+   9.  **Save your changes and close the Gedit window.**

+   10. **Open a GNOME Terminal window and start the server:**

```
killall -9 icecast ices
icecast -c /usr/local/etc/icecast.xml &
ices /usr/local/etc/ices-playlist.xml &
```

+   11. **Enter this command to start XMMS and connect to the newly configured
Icecast2 stream:**

```
xmms http://192.168.1.1:8000/track1.ogg
```

You can also use MPlayer to listen to the stream, if you want:

```
mplayer http://192.168.1.1:8000/track1.ogg
```