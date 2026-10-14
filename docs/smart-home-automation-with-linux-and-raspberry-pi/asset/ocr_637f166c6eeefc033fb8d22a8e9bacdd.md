# ## Media Access

One common piece of functionality is to provide access to your music collection from outside home, such as from the office. Several Apache modules are available to handle this; one of them is mod_musicindex (http://freshmeat.net/projects/musicindex/, also available in the libapache2-mod-musicindex package). Although capable of being used to list general-purpose directories (as it does for its own online documentation), it is capable of rendering music-specific icons to let you download and/or stream this music anywhere in the world and create playlists interactively for the current folder and all the subdirectories underneath it.

To prepare an online portal for your music, first create a directory inside your web directory:

```
```bash
mkdir music
```
```

Then create an .htaccess file inside, granting permissions to whichever users you see fit. These permissions apply to this directory and every one underneath it, unless superseded by another .htaccess file. Because your music collection is likely to be stored outside of the web root, you must add a symlink to it.

```
```bash
ln -s /net/media/mp3 mp3
```
```

This also highlights the reason you created a separate media directory in the root—it eliminates the need for web-specific files polluting the directory structure of our nonweb media file hierarchy. You can then add the appropriate configuration lines to your virtual site configuration file, such as 001-homecontrol:

```
```apache
<Directory /var/www/sites/homecontrol/media>
    Options Indexes FollowSymLinks MultiViews
    MusicIndex On +Stream +Download +Search -Rss -Tarball
    MusicSortOrder filename album disc track artist title filetype filename
    MusicFields title artist album length bitrate
    MusicPageTitle Media Jukebox
    MusicDefaultCss musicindex.css
</Directory>
```
```

Then reload the Apache configuration in the usual way. This provides a functional but less than beautiful page, such as that shown in Figure 5-2.

![](bbox=[0.066, 0.638, 0.902, 0.855])

*Figure 5-2. An example of music index and your music being available anywhere*