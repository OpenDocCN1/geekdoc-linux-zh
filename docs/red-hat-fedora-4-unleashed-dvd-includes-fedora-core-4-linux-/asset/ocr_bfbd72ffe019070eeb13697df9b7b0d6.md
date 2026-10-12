An excellent Internet site for CD-related information is http://www.cdmediaworld.com/.

Also, the Gracenote CDBB Music Recognition Service licenses a database service to software developers so that they can include additional functionality in their application by accessing the database and having their application display information about the music CD, including the artist and song title, the CD's track list, and so on. The database server at cddb.cddb.org will, when contacted by the appropriate software, identify the appropriate CD and send the information to be displayed locally. Many CD player applications provide this functionality. The service is interactive: If you have a CD that is not in the CDBB database, the website tells you how you can add the information to the database.

Each GUI application for burning CDs has different strengths and weaknesses. You should experiment with all the different graphical tools as well as try your hand at command-line burning and you will have a significantly richer multimedia experience with Fedora.

# **X-CD-Roast**

X-CD-Roast, shown in Figure 10.2, is the default standalone CD creator provided with Fedora Core Linux. It can be found in the System Tools menu as the CD Writer menu item, or it can be launched from the command line, like this:

```
$ xcdroast &
```

When you first start it, X-CD-Roast is deceptively plain, giving little indication of the true power of this application. The very first time it is run, it begins with a dialog warning you to enter the Setup dialog, which will be the only button presented to you in the next screen other than Exit. The application autodetects your CD drive, but you must tell it which drive (if you have more than one) is the CD-RW drive and select the users who are allowed to use the application. The dialogs for setting this information are straightforward and easy to follow. Make certain that you choose a default directory for temporary image storage that offers enough room to store several images.

The main X-CD-Roast menu offers you the choice to duplicate or create CDs. The latter operation is shown in Figure 10.3.

# **Other Graphical CD Clients**

Fedora provides the GNOME Grip client to advance ripping to a fine art. Working as both a player and a ripper, it uses cdparanoia and cdcd2wav to rip music tracks and access Internet databases for retrieving track information from disc database servers. To launch Grip, click on its icon in the Sound & Video menu found in the More Sound & Video Applications menu. Use the options in the Grip dialog box tabs to choose, configure, and rip tracks. Also provided is the similar Sound Juicer application.