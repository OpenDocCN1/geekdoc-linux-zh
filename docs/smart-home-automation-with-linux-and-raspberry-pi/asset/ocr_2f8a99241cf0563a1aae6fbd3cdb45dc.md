On Debian, for example, an extra repository is added by placing a single line in the `/etc/apt/sources.list` file:

```
deb http://www.debian-multimedia.org lenny main
```

This is followed by the following traditional process:

```
apt-get update
apt-get install libdvdcss2
```

Sometimes you have to download and install the package manually. That command line invocation would be as follows:

```
dpkg -i libdvdcss2_1.2.10-1_i386.deb
```

Alternatively, the source installation would be as per the INSTALL file, probably something like the trinity of this:

```
./configure
make
make install # as root
```

Once you can use VLC to play DVDs, you know the library is successfully installed and is consequently available to all the main media player applications, such as mplayer, totem, xine, and so on.
When ripping DVDs, you have to consider the amount of hard disk space that you want to devote to your collection, whether you want (or need) the DVD menus, and on what devices they are being played. Ultimately, there are two choices.

# Rip As ISO

Rip As ISO makes a raw copy of the entire disc and stores it as a file. This is the easiest process to initiate, because you simply invoke the following:

```
dd if=/dev/dvd of=TheOffice-series1.iso bs=1024
```

This will generally require between 4GB and 8GB of space and includes all of the DVD menus, titles, chapters, and subtitles. Movie players such as VLC will be able to handle interactive components such as menus, but others won’t. This is especially true of units that don’t support the DVD logo because they won’t have the CSS code as well as of smaller low-power devices such as MediaMVP. In the case of the latter, you can partially solve the problem by using VLC to remotely transcode the movies, but it still won’t be able to handle the processing of the DVD menus.

As with all disk images, Linux is able to mount them to a directory so that they can be read and so that their files can be queried normally. This can be done automatically through the desktop or with the following:

```
mount -t udf -o loop TheOffice-series1.iso dvdimage
```

Note that you cannot mount the image to your usual DVD location (such as `/dev/dvd`) because that is a block device, and you can only mount images to a directory.