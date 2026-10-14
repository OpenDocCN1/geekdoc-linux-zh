Configuring the server requires you to edit the basic configuration file, to indicate the port, the appropriate locations of your media files, and the log files. This file is **minidlna.conf** and should be amended to begin:

```
```conf
# port for HTTP (descriptions, SOAP, media transfer) traffic
port=8200

# set this to the directory you want scanned.
media_dir=A,/net/media/mp3
media_dir=/net/media/movies

# set this if you would like to specify the directory where you want MiniDLNA to store its log file
log_dir=/var/log
```
```

Multiple media_dir lines are perfectly acceptable, and the “A” designation ensures that only Audio files are included. This is handy because some newer albums include digital tracks and music videos alongside their audio counterparts.

From here you can start the server as a daemon from a user account with:

```
```bash
minidnla -f minidlna.conf
```
```

At this point, it will scan the specified media directories for all your files, although the server will begin before scanning has completed. Consequently, some media players will need to be refreshed (or, in the worst case, restarted) to pick up files as the scanning procedure continues. It will also install an inode notifier into the kernel to automatically look for new files in the media directories, although any changes to the configuration file to introduce new media will require you to restart the daemon. There is a command to force such a refresh:

```
```bash
minidnla -R
```
```

although success with this option has been widely variable.

If you intend to include minidlna (or any other UPnP server) in your startup scripts in /etc/init.d, then include it at the end of the sequence, to ensure that filesystem services such as RAID are fully started.

The cache of media files is stored, by default, in /tmp. If you wish this to be more permanent, for example, between reboots, then add a line to the configuration file to this effect:

```
```conf
db_dir=/var/cache/minidlna
```
```

Although there is no web administration tool, you can retrieve basic stats by pointing your web browser to port 8200, or install webmin. In reality, however, little administration is needed as it is intended to be operated headless, with a controller such as VLC.

# Rygel

As a media server, Rygel (https://live.gnome.org/Rygel) builds on the conceptual functionality of minidlna by incorporating its main omission—transcoding. Naturally, this requires a machine with higher performance than minidlna, but the software still retains its focus on being used on a headless box.

Like minidlna, Rygel can be run by a local user and is configured by specifying the URLs of your media:

```
```conf
# In ~/.config/rygel.conf
uris=/net/media/movies,/net/media/mp3
```
```