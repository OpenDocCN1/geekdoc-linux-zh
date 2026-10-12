psql books

Then I type SQL commands at the psql prompt to look up items from the database. When done, I type \q to exit the psql program. Here’s an example (the bold text is what I typed in a terminal window):

```
books> select isbn, title from books where pubkeyr > 2002 \g
isbn | title
-----------------------------------
0764542583 | Red Hat Linux Fedora All-in-One Desk Reference For Dummies
0764541331 | Red Hat Linux 9 Professional Secrets
(2 rows)
books> \q
```

To find out more about administering and using PostgreSQL, visit www.postgresql.org/docs/ and look for links to the latest version of online PostgreSQL documentation.

# Multimedia Applications

Fedora Core includes quite a few multimedia applications — mostly multimedia audio players and CD players, but also applications for using digital cameras and burning CD-ROMs. To play some other multimedia files (such as MPEG video), you have to download and install additional software in your Fedora Core system. Here’s a quick sketch of a few typical multimedia tasks and the applications you can use to perform these tasks:

+   - Using digital cameras: Use the Digital Camera tool to download photos from your digital camera in Fedora Core.

+   - Playing audio CDs: Use one of many audio CD players that come with Fedora Core.

+   - Playing sound files: Use Rhythmbox or XMMS, multimedia audio players (you have to download some additional software to use MP3 files with Rhythmbox or XMMS). You can also download other players from the Internet.

+   - Burning a CD: Use X-CD-Roast to burn CDs.

# Using a digital camera

Fedora Core comes with gtkam — a digital-camera application you can use to download pictures from digital cameras. gtkam is a GUI front end to the gPhoto2 command-line application that works with many different makes and models of digital cameras. Depending on the model, the cameras can connect to the serial port or the Universal Serial Bus (USB) port. Visit the