![](media/bookcover.jpg)

![cover image](media/bookcover.jpg)

1.  [Cover](text/cover.xhtml)
2.  [Table of contents](#nav.xhtml_toc)

# Colophon

Copyright © Dmitri Popov 2020

This work is licensed under the Creative Commons [Attribution-NonCommercial-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-nc-sa/4.0/) license.

Cover photo: Ikebukuro, Tokyo, Japan, May 2016\. SONY NEX-3N, SONY E 18-55mm f/3.5-5.6 OSS SEL1855\. Processed in digiKam.

# About the author

![](media/file0.png)

Dmitri Popov has been writing exclusively about Linux and open source software for many years, and his articles have appeared in Danish, British, US, German, and Russian magazines and websites. He regularly contributes to [PIXLS.US](https://pixls.us/), and you can find more about his work on his [Coffee, Code, Camera](https://coffeecode.camera/) website.

# About this book

This book provides practical examples of automating the key stages of a Linux-based photographic workflow using minimalist and specialized tools to manage, process, publish, and back up photos. The book demonstrates how to harness the power of Bash shell scripting to automate the process of transferring, renaming, and organizing photos. You’ll also learn how to use gThumb to manage and edit images, process RAW files in Darktable, implement an automatic cloud backup system, build a mobile backup device, and host your own photo gallery. Understanding the book’s material requires a working knowledge of Bash and Linux. The book assumes that you are using Debian or openSUSE Linux distribution with *sudo* enabled and configured.

# Import photos and RAW files with Photo Funnel

When it comes to transferring photos and RAW files from a camera to a regular Linux machine, you have plenty of tools at your disposal: from [digiKam](https://www.digikam.org/) to [Rapid Photo Dowloader](https://www.damonlynch.net/rapid/index.html). But in case you are looking for something more simple and straightforward in use, [Photo Funnel](https://github.com/dmpop/photo-funnel) might be right up your alley.

![](media/file1.png)

Photo Funnel is a simple graphical tool that allows you to import, geotag, and organize photos and RAW files. When running, Photo Funnel displays a drag-and-drop panel. Drop the photos and RAW files you want to import on to the panel, press **Import**, and the utility takes care of the rest.

During the import operation, Photo Funnel writes useful information (copyright, camera model and lens) into the appropriate EXIF fields.

Installing Photo Funnel is a matter of running the `curl -sSL https://is.gd/photofunnel | bash` command. On the first run, it prompts you to specify copyright notice and a target directory for storing the transferred files.

The configuration procedure is done only once, and the provided values are stored in the *~/.pf* file. If you need to change the saved values later, edit the *.pf* file in a text editor.

Using Photo Funnel couldn’t be easier. First, insert and mount a storage card on your machine. Launch then Photo Funnel either by using the Desktop launcher or by running the `pf` command. Select the photos and RAW files on the storage card, drop them on to the designated area of the Photo Funnel panel, and press **Continue**. Enter the city where the photos were taken, press **OK**, and wait till the transfer operation is finished. You’ll then find the transferred photos in the specified destination directory renamed, geotagged, and neatly organized into folders by date.

# Import and organize photos with Otto

Moving files from a storage card or an external storage device to a NAS is usually a rather straightforward affair. But if you want to teach your NAS a few clever tricks, [Otto](https://gitlab.com/dmpop/otto) is just the tool for the job. Install it on your NAS, and you can use the appliance to transfer photos and RAW files as well as rename and organize the transferred files, and even write useful information into EXIF metadata.

Before you deploy Otto, you need to install several tools on your Linux-based NAS. Most NAS models don’t allow you to install third-party packages out of the box. Fortunately, the [Entware](https://github.com/Entware/Entware) project provides a solution to the problem. Install the Entware app on your NAS, and you’ll instantly get access to a wide range of popular Linux tools and utilities. The Entware project offers a compiled app for several mainstream NAS models, including ASUSTOR, Synology, and QNAP. If you happen to use the latter, grab the appropriate *.qpkg* package from the [Install on QNAP NAS](https://github.com/Entware/Entware/wiki/Install-on-QNAP-NAS) page. On the NAS open **App Center**, click the **Install Manually** button in the upper-right corner of the main window, select the downloaded *.qpkg* package, and press **Install**.

Next, establish an SSH connection from your regular machine to the NAS. Run the `opkg update` command to update the list of available packages. Install then the required packages using the following command:

```
opkg install getopt bc jq curl perl-image-exiftool git git-http
```

If you want to be notified when Otto has finished importing and organizing photos, install the [Simple Push](https://www.simplepush.io/) app on your Android device, run the app, and note the unique token.

Deploying Otto on the NAS is a matter of switching to the desired directory (e.g., */share/homes/admin*) and cloning the project’s Git repository:

```
git clone https://gitlab.com/dmpop/otto.git
```

The QNAP NAS can handle practically any other mainstream file system, including NTFS, Ext2, Ext4, etc. So when you connect a supported external storage device, the appliance automatically detects and mounts it. To find the directory where the device is mounted, run the `mount` command and note the path to the directory (it may look something like this: */share/external/DEV3301_1*).

Unfortunately, QNAP NAS appliances don’t support the exFAT file system out of the box. And if you want to use an exFAT-formatted external storage device with your QNAP NAS you need to purchase a license. However, if you don’t mind manually mounting external storage devices and you don’t want to waste money on something that should have been included with the NAS by default, Entware got you covered. Run the `opkg install exfat-fuse lsblk` command to install the required packages. Connect then an exFAT-formatted device to your NAS, run the `lsblk` command, and note the device name and path of the connected storage device (e.g., */dev/sdc1/*). Use the command below to mount the device in the */root/media/* directory (you need to create the mount directory if it doesn’t exist):

```
mount.exfat-fuse /dev/sdc1 /root/media/
```

By default, Otto works with photos and RAW files that have the *JPG* and *ARW* extensions. To change that, open the *otto.sh* script for editing and modify the values of the `EXT` and `RAW` variables.

With all the pieces in place, you are ready to run the script. Plug in a storage card into your NAS, and make sure that the card has been mounted. The Otto command has the following format `otto.sh -d <directory> -g <city>`, where `directory` is the absolute path to the root directory of the storage card and `city` is the name the of the city where the photos where taken. If your photos are already geotagged, you can omit this parameter. For example:

```
/share/homes/admin/otto/otto.sh -d /share/external/DEV3301_1/DCIM/ -g Tokyo
/share/homes/admin/otto/otto.sh -d /root/media/DCIM/
```

During the first run, the script prompts you to specify the required info, such as the desired target directory, and a copyright notice. These values are stored in the *otto.cfg* configuration file. If you need to change any of the values later, you can do this by editing the configuration file in a text editor.

Wait then for the script to finish. You’ll find the transferred photos and RAW files geotagged, renamed, and neatly organized in folders by date in the target directory.

To update Otto, switch to the *otto* directory, and run the `git pull` command.

Since Otto is just a regular Bash shell script, it will happily run on any NAS device that supports Entware as well as any Linux-based machine. For example, installing Otto on openSUSE is a matter of running the following commands:

```
sudo zypper in bc jq curl ImageMagick gpsbabel
git clone https://gitlab.com/dmpop/otto.git
cd otto
sudo cp otto.sh /usr/local/bin/otto
sudo chown root:root /usr/local/bin/otto
sudo chmod 755 /usr/local/bin/otto
```

## Geotag and geocorrelate photos with Otto

If the photos are geotagged, Otto writes useful information, such as camera model and lens into the **Comment** field of the EXIF metadata. Better still, if your camera doesn’t support geotagging, the script offers two ways to geotag photos and RAW files on the fly. Add the `-g` switch followed by the city where the photos were taken, and the script automatically obtains the city’s coordinates and uses them for geotagging:

```
otto.sh -d /path/to/photo/dir -g Tokyo
```

Otto also makes it possible to geocorrelate photos and RAW files using a GPX file. This can come in handy when you use an app like [GPS Logger for Android](https://github.com/mendhak/gpslogger) to track your movements and save them as GPX files.

To geocorrelate photos and RAW files when transferring them, put one or several GPX files into a directory and use the `-c` switch followed by the path to the directory:

```
otto.sh -d /path/to/photo/dir -c /path/to/gpx/dir
```

# Geotag photos with Geophotobash

Once photos and RAW files have been imported, you might want to geotag them. And the [Geophotobash](https://gitlab.com/dmpop/geophotobash) Bash shell script can help you with that.

## Deploy Geophotobash

To install Geophotobash on Debian and Ubuntu, run the following commands:

```
sudo apt install git-core curl bc jq libimage-exiftool-perl
git clone https://gitlab.com/dmpop/geophotobash.git
cd geophotobash
sudo cp geophotobash.sh /usr/local/bin/geophotobash
sudo chown root:root /usr/local/bin/geophotobash
sudo chmod 755 /usr/local/bin/geophotobash
```

To do the same on openSUSE, replace the `sudo apt install git-core curl bc jq libimage-exiftool-perl` command with `sudo zypper in git-core curl bc jq exiftool`.

To make sure that the script has been installed, run the `geophotobash -h` command, and you should see brief usage info.

## How Geophotobash works

The *geophotobash.sh* script performs the following actions:

*   Obtains the latitude and longitude for the specified city using the [Photon](http://photon.komoot.de/) service
*   Geotags photos in the current directory using the retrieved geographical coordinates
*   Renames photos using their date and time from EXIF metadata
*   Organizes the photos in folders by city, and date
*   Assigns the specified city as a keyword to each photo

Here is how this works. Say, you have a folder with photos taken in Berlin with file names like *DSC00895.ARW*, *DSC00895.JPG*, *DSC00896.ARW*, *DSC00896.JPG*, *DSC00897.ARW*, *DSC00897.JPG*, etc. Run the `geophotobash -g Berlin` command. The result will be the following directory tree containing renamed and geotagged photos organized into folders by date:

```
Berlin
  2016-05-01
    20160501-135557.ARW
    20160501-135557.JPG
  2016-05-02
    20160502-190510.ARW
    20160502-190510\. JPG
  2016-05-03
    20160503-151535.ARW
    20160503-151535\. JPG
```

# Organize and manage photos with ExifTool

If you need to process hundreds, or even thousands, of photos on a regular basis, using ExifTool for the job can save you a lot of time and effort. Even if you need to modify a handful of photos, doing this with ExifTool can be more efficient than resorting to your preferred photo management application.

## Install ExifTool

Installing ExifTool is a matter of running the `sudo apt install libimage-exiftool-perl` command on Debian and Ubuntu or `sudo zypper in exiftool` on openSUSE. ExifTool in the official software repositories is often several versions behind the current release. And if you want to use the most recent version of ExifTool, you have to compile it from the source code. Fortunately, this is a rather straightforward thing to do. Grab the latest ExifTool source code from the project’s website, and use the `tar xzvf Image-ExifTool-#.##.tar.gz` command to extract the downloaded archive. Switch to the resulting directory, and run the `perl Makefile.PL` command. To test whether ExifTool can work properly on your system, issue the `make test` command. If everything works as it is supposed to, you should see the *PASS* message at the end of the test output. Run then the `make install` command as root to perform the installation.

By default, ExifTool is installed in the */usr/local/bin/* directory. If this path is not in the PATH environment variable, you need to add it manually. To do this, open the terminal and run the `echo "PATH=\$PATH:/usr/local/bin" >> ~/.bashrc` command.

Once ExifTool has been compiled and installed, run the `exiftool -ver` command to verify that the you have the latest version of the tool on your system.

## Simple ExifTool commands

To get started with ExifTool, run the `exiftool /path/to/foo.jpg` command which generates a long list of metadata tags and their values pulled from the source photo. Besides JPEG, ExifTool can handle a wide range of other formats as well as RAW and video files (the full list of supported formats is available on the project’s website).

Metadata included in a digital photo actually comes from several different groups, including EXIF (Exchangeable image file format maintained by the Japanese Electronics and Information Technology Industries Association), IPTC (standard developed by the International Press Telecommunications Council for the purpose of data exchange between newspapers and news agencies), MakerNote data (tags that allow camera manufacturers to add custom metadata), XMP (metadata stored in the XMP format originally created by Adobe Systems Inc.), and Composite (composite tags derived from the values of other tags).

Despite its name, ExifTool can handle metadata stored in all these formats. When you need to read or modify a specific tag in metadata, you occasionally need to know the actual name of the tag (as opposed to the human-friendly format used by default) and the group it belongs to. The easiest way to find that out is to use the `exiftool` command with the `-s` and `-G` switches. The former shows the actual tag names, while the latter lists all tags organized by groups. Run the `exiftool -s -G /path/to/foo.jpg` command, and you should see a list of tags neatly organized into groups.

## Rename and organize photos using metadata

Besides merely reading metadata, ExifTool can perform other useful actions. For example, the tool can read the photo’s creation date and time and then use the obtained values to rename the file. The following command renames the *foo.NEF* RAW file in the current directory using the *YYYYMMDD-HHMMSS.NEF* format (e.g., *19730915-153500.NEF*):

```
exiftool -d %Y%m%d-%H%M%S.%%e '-FileName<DateTimeOriginal' /path/to/foo.NEF
```

The command consists of three parts. The *-d* switch sets the format for date and time values, and the rule right after the switch defines the format itself (`%%e` keeps the original file extension). The `'-FileName<DateTimeOriginal'` part instructs ExifTool to obtain the creation date and time and use these values as file name. The last part of the command specifies the path to the file.

You can use the path to a folder instead of a single file to run the command on all files in the target directory (replace *DIR* with the actual path to the target directory):

```
exiftool -d %Y%m%d-%H%M%S.%%e '-FileName<DateTimeOriginal' DIR
```

ExifTool supports a wide range of parameters and switches. The `-ext` parameter, for example, can be useful when you need to process photos in a specific format. For example, if the target directory contains both JPG and NEF RAW files, and you want to rename RAW files only, use the `-ext NEF` parameter as follows (`.` denotes the current working directory):

```
exiftool -ext NEF -d %Y%m%d-%H%M%S.%%e '-FileName<DateTimeOriginal' .
```

The `-r` switch can be used to run ExifTool commands on a directory and all its subdirectories:

```
exiftool -ext NEF -r -d %Y%m%d-%H%M%S.%%e '-FileName<DateTimeOriginal' .
```

Renaming photos is only one of ExifTool’s many capabilities. Need to organize photos into folders by year? The command below provides a solution to the problem:

```
exiftool -r -d %Y '-directory<$DateTimeOriginal/%d' .
```

This command pulls the year from each photo’s creation date and moves the photo into the appropriate folder (the folder is automatically created if it doesn’t already exist).

Photographers who shoot in both RAW and JPEG will also appreciate the following command that sorts photos into directories named by the original file extensions:

```
exiftool -directory=%e DIR
```

So if the current working directory contains both *.nef* and *.jpg* files, the command above moves them into the *nef* and *jpg* directories respectively.

Speaking of RAW files, ExifTool also makes it possible to extract JPEG images embedded into RAW files using the `-JpgFromRaw` switch:

```
exiftool -b -r -JpgFromRaw -ext NEF -w foo/%f.jpg .
```

The command above extracts JPEG images from NEF RAW files in the current working directory and saves the extracted files in the *foo* folder. The `-b` switch outputs data in the binary format, while the `-w` switch writes the binary data as files.

## ExifTool-based multi-purpose shell script

[ExifTool](http://www.sno.phy.queensu.ca/~phil/exiftool/) is an immensely powerful and flexible tool for working with photographic metadata. But you don’t need to learn all its intricacies in order to put it to some practical uses. The following Bash shell script makes use of ExitTool to automate several tasks:

```
#!/usr/bin/env bash
while getopts "h?sdyar" opt; do
case $opt in
  s) exiftool -directory=%e .
  ;;
  d) exiftool -d %Y%m%d-%H%M%S.%%e '-FileName<DateTimeOriginal' -r .
  ;;
  y) exiftool '-Directory<CreateDate' -d %Y-%m-%d -r .
  ;;
  a) exiftool -T -r -filename -make -model -fnumber -exposuretime -iso -r . > results.txt
  ;;
  r) exiftool -overwrite_original -all= -r .
  ;;
  h|\?)
  cat <<EOF
USAGE:
  $0 [OPTIONS]
  $0 -s sort photos into folders by file extension
  $0 -d rename photos by date
  $0 -y sort photos into folders by year, month, and date
  $0 -a save key EXIF data in the results.txt file
  $0 -r remove all EXIF metadata from photos
EOF
  exit 2
;;
esac
done
```

Paste the script into a new text file and save it under the *exiftool-helper.sh* name. Use then the following commands to install the script globally:

```
sudo cp exiftool-helper /usr/local/bin/
sudo chown root:root /usr/local/bin/exiftool-helper
sudo chmod 755 /usr/local/bin/exiftool-helper
```

Since the script relies on the ExifTool, you need to install this tool using the `sudo apt install libimage-exiftool-perl` command.

The script uses various switches to run the available commands. Used with the `-s` switch, the script sorts photos in the current directory by file extension. This can be useful when you have RAW and JPEG files in the same directory and you want to move them into separate folders. The `-r` switch runs the command that removes metadata from all photos in the current directory, while the `-a` switch can be useful for exporting key EXIF data (aperture, shutter speed, ISO, etc.) to a tab-separated text file. You can then use a spreadsheet application to analyze these data.

Naturally, you can customize the existing commands in the script as well as add new ones. For example, if you want to add focal length data to the list of exported values, modify the command launched by the `-a` script as follows:

```
exiftool -T -r -filename -make -model -fnumber -exposuretime -iso -focallength -r . > results.txt
```

To add a new command to the script you need to specify a switch for it first. For example, if you want to use the `-w` switch, add it to the `"h?sdyar"` string: `"h?sdyarw"`. Add then the desired command at the end of the `case ... in` block above the `h|\?)` line using the following format:

```
w) command goes here
  ;;
```

# Add useful functions to the Bash shell

Add a few relatively simple functions to the *~/.bashrc* configuration file, and you can perform a wide range of photo-related tasks directly from the command line.

## Find and remove duplicates

To keep your photo library in good shape, you should regularly check it for duplicates. And [fdupes](https://github.com/adrianlopezroche/fdupes) is just the tool for the job. Install it using the `sudo apt install fdupes` command, open the *~/.bashrc* file in a text editor, add the code below, and save the changes:

```
if [ -x "$(command -v fdupes)" ] ; then
  function prune() {
  dir=$(pwd)
  fdupes -rd $dir
  }
fi
```

The `if...then` statement checks whether the *fdupes* tool is installed, while the *prune()* function obtains the path of the current directory and runs the `fdupes -rd` command that finds duplicate files and lets you remove them interactively.

## Resize photos

Before you share photos on social media or publish them on your blog, you might want to reduce their size and quality to save storage space and cut down upload time. And the *mogrify* tool, which is part of the ImageMagick package, can help you with that. To install ImageMagick on Debian and Ubuntu, run the `sudo apt install imagemagick` command. On openSUSE, run the `sudo zypper in ImageMagick` command. To process all JPEG images in a directory, you can use the following command:

```
mogrify -resize '1600x1600>' -quality 95% *.JPG
```

This command finds all *.JPG* files and runs the `mogrify -resize '1600x1600>' -quality 95%` action on them. The latter reduces the size to 1600px on the longest side and reduces quality to 95%. Of course, you can modify the defaults, if needed.

Instead of typing the command every time you need to resize photos, you can add a dedicated function to the *~/.bashrc* file. Open the file in a text editor and add the following code:

```
if [ -x "$(command -v mogrify)" ] ; then
  function resize() {
    ext=${1:-JPG}
    dimension=${2:-1600}
    quality=${2:-95}
    mogrify -resize "$dimension"x"$dimension"\> -quality "$quality"% *."$ext"
  }
fi
```

Switch then to the directory containing the photos you want to process, and run the `resize` command. Keep in mind that this overwrites the original files in the directory. If that’s not what you want, use the *convert* tool instead of *mogrify*:

```
if [ -x "$(command -v convert)" ] ; then
  function resize() {
    ext=${1:-JPG}
    dimension=${2:-1600}
    quality=${3:-95}
    for file in *".$ext"; do echo "$file"; convert "$file" \
    -resize "$dimension"x"$dimension"\> \
    -quality "$quality"% "resized_$dimension_$file"; done
  }
fi
```

When you run the `resize` command without any parameters, the function uses the default values of the *ext*, *dimension*, and *quality* variables. In this case, the defaults are *jpg*, *1600*, and *95* respectively. You can override the default values by specifying the desired values as follows:

```
resize png 800 75
```

## Convert RAW files

There is no need to fire up a heavyweight RAW processing application when you need to quickly convert RAW files to the JPEG format. Instead you can use the combination of the *dcraw* and *cjpeg* tools to process RAW files and save them as JPEG images. Start with installing the required packages using the `sudo apt install dcraw libjpeg-turbo-progs` command on Debian and Ubuntu, or `sudo zypper in dcraw libjpeg-turbo` on openSUSE. Run then the `dcraw -c foo.raw | cjpeg > foo.JPG` command to convert a single RAW file, or use a more advanced command with the `for...do` loop to convert all RAW files in the current directory:

```
for file in *.RAW; do dcraw -c -g 2.4 12.92 $file | cjpeg > "${file%%.*}".jpeg; done
```

And of course, you can add a dedicated function to the *~/.bashrc* file:

```
if [ -x "$(command -v dcraw)" ] && [ -x "$(command -v cjpeg)" ] ; then
  function rawtojpeg() {
    ext=${1:-RAW}
    for file in *.$ext; do echo "Processing $file"; \
    dcraw -v -c -g 2.4 12.92 $file | cjpeg > "${file%%.*}".jpeg; done
  }
fi
```

By default, this function processes all files with the *.RAW* extension in the current directory, but you can specify a different file extension, for example: `rawtojpeg NEF`.

## Rename photos and edit EXIF metadata with jhead

[ExifTool](http://www.sno.phy.queensu.ca/~phil/exiftool/) is by far the most powerful and versatile tool for working with photographic metadata, but it’s not the only tool that allows you to do that. Although [jhead](http://www.sentex.net/~mwandel/jhead/) offers only a fraction of ExifTool’s functionality, this lightweight utility is easy to master and it can handle many common EXIF-related tasks. To install jhead, run the `sudo apt install jhead` command.

Similar to ExifTool, jhead can rename photos using date and time data from EXIF headers, so you can add the following function that does this to the *~/.bashrc* file.

```
if [ -x "$(command -v jhead)" ] ; then
  function jrename() {
    ext=${1:-jpeg}
    jhead -n%Y%m%d-%H%M%S *.$ext
  }
fi
```

By default, the function renames all *.jpeg* files in the current directory, but you can also explicitly specify the desired extension as a command parameter:

```
jrename JPG
```

The function renames photos using the *YYYYMMDD-HHMMSS* format, but you can easily modify the `%Y%m%d-%H%M%S` formatting string. Here are a few useful arguments you can use to construct a custom string.

```
%d  Day of month as decimal number (01 – 31)
%H  Hour in 24-hour format (00 – 23)
%j  Day of year as decimal number (001 – 366)
%m  Month as decimal number (01 – 12)
%M  Minute as decimal number (00 – 59)
%S  Second as decimal number (00 – 59)
%U  Week of year as decimal number, with Sunday as first day of week (00 – 53)
%w  Weekday as decimal number (0 – 6; Sunday is 0)
%y  Year without century, as decimal number (00 – 99)
%Y  Year with century, as decimal number
```

Need to add a description to a photo? The function below allows you to do just that.

```
if [ -x "$(command -v jhead)" ] ; then
  function jcomment() {
    jhead -ce $1
  }
fi
```

Run the `jcomment` command followed by the filename of the desired photo (e.g., `jcomment foo.jpg`), and it opens the default text editor, where you can enter the text. When you save the changes, jhead writes the text into the Comment field in the EXIF header.

## Geotag photos with reference snapshots

If your camera lacks geotagging capabilities, you can add geographical information to photos using a smartphone and a Bash one-liner.

When you take photos at a specific spot, remember to take a snapshot using your mobile device (make sure that the geotagging feature in the camera app on the device is enabled). This snapshot can be used as a reference file for geotagging the photos with the [ExifTool](http://www.sno.phy.queensu.ca/~phil/exiftool/). To install it, run the `sudo apt-install libimage-exiftool-perl` command. The simple command below reads geographical tags from the reference snapshot and writes them to all photos in the current directory:

```
exiftool -overwrite_original -r -tagsFromFile path/to/reference.jpg -gps:all.
```

Replace *path/to/reference.jpg* with the actual path to the reference snapshot. To make geotagging photos more straightforward, add the following function to the *~/.bashrc* file:

```
if [ -x "$(command -v exiftool)" ] ; then
  function geotag() {
    refphoto=${1:?Missing file}
    dir=${2:?Missing directory}
    exiftool -overwrite_original -r -tagsFromFile $1 -gps:all $2
  }
fi
```

You can then geotag photos using the `geotag path/to/reference.jpg path/to/dir` command.

## Geocorrelate photos with GPS Logger for Android and ExifTool

Even if your camera doesn’t have a GPS module and geotagging capabilities, there are still plenty of ways to add geographical coordinates to photos. If you happen to use an Android device, you can install a GPS logging app that records tracks in the GPX format. These tracks can then be used to geocorrelate photos (i.e., obtain geographical coordinates from the GPX track and write them into the photos). While there are several GPS trackers available at Google Play Store, the [GPS Logger](https://play.google.com/store/apps/details?id=com.mendhak.gpslogger) is probably the best of the bunch: it’s lightweight, user-friendly, and released under an open source license. More importantly, GPS Logger doesn’t affect the battery life and can export recorded tracks in a number of formats, including GPX. Before launching the app and start logging, it’s important that the time on your Android device and camera is in sync. When you are heading out to shoot, launch the app and start logging. Stop recording when you are done, export the track into the GPX format, and transfer the resulting file to your Linux machine.

To geocorrelate photos, add the following function to the *~/.bashrc* file:

```
if [ -x "$(command -v exiftool)" ] ; then
  function geocorrelate() {
    gpx_file=${1:?Missing GPX file}
    dir=${2:?Missing directory}
    exiftool -overwrite_original -geotag "$gpx_file" "$dir"
  }
fi
```

This function uses the ExifTool to perform geocorrelation, so you need to install the tool using the `sudo apt-get install libimage-exiftool-perl` command first. To run a geocorrelation operation, issue the `geocorrelate` command followed by the paths to the GPX file and the directory containing photos, for example:

```
geocorrelate ~/gpx/20160707.gpx ~/photos
```

## Assemble photos into a GIF animation or a slideshow with ImageMagick

Animated GIFs are not only good for sharing funny cat videos. They can also come in rather handy when you want to whip up a quick-and-dirty slideshow that can be viewed on any platform or create a timelapse animation from a sequence of images with a minimum of effort.

Generating animated GIFs can be done using *ImageMagick* and *jhead*. To install these tools on Debian and Ubuntu, run the `sudo install imagemagick jhead` command. If you happen to use openSUSE, run the `sudo zypper in ImageMagick jhead` command.

In the terminal, switch to the directory containing the photos you want to assemble into an animated GIF, and run the following command:

```
jhead -n%Y%m%d-%H%M%S *.JPG
```

This renames the photos using their date and time data to ensure the correct image sequence. Since there is little point in turning full-resolution photos into an animated GIF, resize the source images:

```
mogrify -resize 800x *.JPG
```

Generating an animated GIF then is a matter of running the following command:

```
convert -delay 120 -loop 0 *.JPG foo.gif
```

The *delay* parameter specifies the delay between frames in milliseconds, while the *loop* parameter determines how many times the animation runs (the *0* value will run the loop infinitely).

To automate the process of generating an animated GIF, add the following function to the *~/.bashrc* file:

```
if [ -x "$(command -v mogrify)" ] ; then
  function makegif() {
    ext=${1:-JPG}
    dimension=${2:-800}
    quality=${3:-95}
    output=${4:-"foo.gif"}
    delay=${5:-120}
    mogrify -resize "$dimension"x *."$ext"
    convert -delay "$delay" -loop 0 *"$ext" "$output"
  }
fi
```

Next time you want to transform a set of photos into an animated GIF, switch to the directory with the photos, and run the `makegif` command. To overrride the default settings, specify the required parameters, for example:

```
makegif jpeg 1600 90 foo-big.gif 180
```

## Add captions with basic EXIF data to photos

Adding a caption containing basic EXIF info such as aperture, shutter speed, and ISO to a photo can come in useful in many situations. And a simple Bash shell function automates this action. The function uses the *ExifTool* and *ImageMagick* tools to extract EXIF data from a specified image. It then adds a caption containing the extracted aperture, shutter speed, and ISO values to the image.

```
if [ -x "$(command -v exiftool)" ] && [ -x "$(command -v convert)" ]; then
  function annotate(){
  fnumber=$(exiftool -aperture $1 | cut -d':' -f2)
  exposure=$(exiftool -shutterspeed $1 | cut -d':' -f2)
  iso=$(exiftool -iso $1 | cut -d':' -f2)
  convert $1 -gravity South -background Black \
  -font mononoki-Regular -pointsize 50 -fill White \
  -splice 0x54 -annotate 0x0 "Aperture:$fnumber Shutter speed:$exposure ISO:$iso"  exif_$1
  xdg-open exif_$1
  }
fi
```

In this case, the function uses the [Mononoki](https://madmalik.github.io/mononoki/) font for the caption, but you can replace it with any other font installed on your system. To list all fonts that you can use, run the `convert -list fonts` command. To add a caption to a photo, run the `annotate /path/to/foo.JPG` command (replace */path/to/foo.JPG* with the actual path and filename of the photo).

Of course, you can tweak the script to fit your specific needs. For example, you can replace the EXIF info with a copyright notice, or modify the function to add an arbitrary text on-the-fly.

## Show geotagged photos on OpenStreetMap

Want to show on the map the place where you took a specific photo? Provided that the photo is geotagged, the simple function below will do the job:

```
if [ -x "$(command -v exiftool)" ] ; then
  function show-on-osm(){
    lat=`exiftool -n -p '$GPSlatitude' $1`
    lon=`exiftool -n -p '$GPSlongitude' $1`
    osm="http://www.openstreetmap.org/?mlat=$lat&mlon=$lon&zoom=18"
    xdg-open $osm
  }
fi
```

The function extracts latitude and longitude values from the photo’s EXIF metadata, creates an OpenStreetMap URL, and opens it in the default browser.

For the function to work, you need to install the *ExifTool* on your system. Add the function to the *~/.bashrc* file, and use the `show-on-osm foo.JPG` command to show the photo you want on OpenStreetMap (replace *foo.JPG* with the actual name of the desired photo).

# Faster access to image processing actions via context menus

Using the service menus feature in KDE, you can add useful commands to the **Actions** entry context menu in Dolphin. For example, you might want to resize photos before sharing them. But instead of switching to the terminal and running a command like `convert photo.jpg -resize 1600x1600> resized-photo.jpg` every time you need to optimize a photo, you can create a service menu that allows you to quickly resize images from the convenience of the Dolphin file manager. Create a text file and paste the following service menu definition in it:

```
[Desktop Entry]
Type=Service
ServiceTypes=KonqPopupMenu/Plugin
MimeType=image/png;image/jpeg;image/png;image/JPG;image/png;image/jpg;
Actions=ResizeLarge
[Desktop Action ResizeLarge]
Name= Resize to 1600px
Exec=mogrify -resize "1600x1600>" %f
Icon=image-x-applix-graphics
```

To limit the menu to certain image formats, you can specify them in the *MimeType* part. In the example above, the action will work only with JPEG and PNG images.

Save the file under the *resize.desktop* name and move it to */usr/share/kservices5/ServiceMenus* (create *ServiceMenus* directory manually if it doesn’t exist):

```
sudo cp resize.desktop /usr/share/kservices5/ServiceMenus/
```

Open Dolphin, right-click on a JPG or PNG image file, and select the **Actions → Resize to 1600px** action to resize the image.

Using this simple technique, you can add all sorts of context commands. For example, you can define an action that recompresses JPEG photos using the [jpeg-recompress](https://github.com/danielgtaylor/jpeg-archive) tool:

```
[Desktop Entry]
Type=Service
ServiceTypes=KonqPopupMenu/Plugin
MimeType=image/jpeg;image/JPG;image/jpg;
Actions=JPEGRecompress
[Desktop Action JPEGRecompress]
Name= Recompress
Exec=jpeg-recompress %f %f
Icon=image-x-applix-graphics
```

![](media/file2.jpg)

Dolphin is not the only file browser that supports user-defined actions. If you happen to use Nautilus as your preferred file browser, you can add commands by placing executable scripts in the *~/.local/share/nautilus/scripts* directory. In addition to popular languages like Python and Perl, you can use good old Bash to write scripts. When a script is called, Nautilus automatically sets a handful of variables that can be used in the script. Here is a simple Bash script that uses the *mogrify* tool to resize the currently selected image files:

```
#!/bin/bash
FILE=`echo $NAUTILUS_SCRIPT_SELECTED_URIS | sed 's@file://@@g'`
mogrify -resize "1600x1600>" $FILE
```

The script obtains full file paths via the `$NAUTILUS_SCRIPT_SELECTED_URIS` variable and uses the sed tool to remove the leading *file://* string from them. Save the script under a descriptive name like *Resize*, make it executable using the `chmod +x Resize` command, and place the script into the *~/.local/share/nautilus/scripts* directory. You can then run the script by right-clicking on selected files in Nautilus and choosing the **Scripts → Resize** item in the context menu.

## Compare photos with ImageMagick and a KDE service menu action

Need to compare two photos side-by-side? Using the convert tool, you can quickly stitch two or more photos together and compare the result in any image viewer:

```
convert photo1.jpg photo2.jpg +append compare.jpg
```

The command above stitches *photo1.jpg* and *photo2.jpg* from left to right (i.e. *photo1.jpg* + *photo2.jpg*), but you can use `-append` instead of `+append` to reverse the order (i.e. *photo2.jpg* + *photo1.jpg*). In both cases, the stitched image is saved as the *compare.jpg* file in the JPEG format.

If you use KDE as your preferred graphical desktop environment, you can create a context action to stitch file pairs in the Dolphin file manager. Create a text file and paste the following code into it:

```
[Desktop Entry]
Type=Service
ServiceTypes=KonqPopupMenu/Plugin
MimeType=image/JPG;image/JPEG;image/jpeg;image/JPG;image/jpg;
Actions=Compare
[Desktop Action Compare]
Name=Compare Photos
Exec=convert %F +append compare.jpg
Icon=image-x-applix-graphics
```

Save the file under the *compare.desktop* name and move it to */usr/share/kservices5/ServiceMenus*:

```
sudo cp compare.desktop /usr/share/kservices5/ServiceMenu/
```

Open Dolphin, select a pair of JPEG files you want to compare, right-click on the selection, and choose the **Actions → Compare Photos** action to resize the image. You can then use your preferred image viewer to open the resulting *compare.jpg* file and examine the photos.

# Efficient JPEG compression with jpeg-recompress

Compressing JPEG images is something most photographers try to avoid. After all, JPEG is a lossy format, and reducing the size of a JPEG file inevitably leads to loss of quality. But there are situations where compressing images is the only option. For example, some photo sharing and printing services don’t accept images that exceed a specific file size. And when embedding photos into a blog article, you might want to compress them to save storage space.

Whenever you need to optimize JPEG files, [jpeg-recompress](https://github.com/danielgtaylor/jpeg-archive) is just the tool for the job. jpeg-recompress can reduce the size of the target file by 30-70% while keeping the perceived visual quality. To install jpeg-recompress, download the latest release from [github.com/danielgtaylor/jpeg-archive/releases](https://github.com/danielgtaylor/jpeg-archive/releases). Unpack the downloaded archive and make the *jpeg-recompress* binary executable using the `chmod +x jpeg-recompress` command. Move then the binary file to the *~/bin* directory.

jpeg-recompress is rather straightforward in use. To recompress a JPEG file using the default settings (the SSIM comparison method and medium quality), run the `jpeg-recompress photo.jpg recompressed.jpg` command. It’s also possible to specify various parameters, and you can list them along with their brief descriptions using the `jpeg-recompress -h` command.

If you plan to use the jpeg-recompress tool on a regular basis, add the following function to the *~/.bashrc* file:

```
if [ -x "$(command -v jpeg-recompress)" ] ; then
  function recompress() {
  jpeg-recompress --quality very high $1 re-$1
  }
fi
```

You can then recompress a JPEG file using the `recompress photo.jpg` command.

Want to automatically recompress images as soon as they are added to a specific directory? A simple Bash script below can help you with that:

```
#!/usr/bin/env bash

help(){
cat <<EOF
$0 [OPTIONS]

$0 recompresses JPEG files as soon as they are moved into the monitored directory

Usage:
  $0 [IN] [OUT]

Options:
 IN    Directory to monitor
OUT    Directory to save the recompressed files
EOF
  exit 1
}

if [ -z "$1" ] || [ -z "$2" ]; then
  echo help
  exit 1
fi

while true
do
inotifywait -m --format '%f' -e MOVED_TO $1 |
while read FILE
  do
    jpeg-recompress $1/$FILE $2/$FILE
    notify-send "$FILE has been recompressed"
  done
done
```

The script uses inotify-tools to monitor a directory and trigger the `jpeg-recompress` command to process images as soon as they appear in the directory. To install inotify-tools on openSUSE, run the `sudo zypper in inotify-tools` command. The script requires two parameters: the path to the monitored directory and the path the target directory. Note that the latter must not reside in the monitored directory.

Paste the code above into a new text file and save it under the *monitor-recompress* name. Install then the script using the following commands:

```
sudo cp monitor-recompress /usr/local/bin/
sudo chown root:root /usr/local/bin/monitor-recompress
sudo chmod 755 /usr/local/bin/monitor-recompress
```

Run then the script using the `monitor-recompress /path/to/source/dir /path/to/target/dir` command.

# Squeeze JPEG files with jpegoptim

Need to reduce the size of a JPEG file with a minimum of effort? Use [jpegoptim](https://github.com/tjko/jpegoptim). Feed jpegoptim a JPEG file, and this unassuming tool will reduce its size, no questions asked.

To install the latest version of jpegoptim, you need to compile it from source. Before you can do that, you need to install the libjpeg library on your system. On openSUSE, this can be done using the `sudo zypper in libjpeg8-devel` command. Once you’ve done that, run the following commands to clone the project’s Git repository and install jpegoptim:

```
[](#cb53-1)git clone https://github.com/tjko/jpegoptim.git
[](#cb53-2)cd jpegoptim
[](#cb53-3)./configure
[](#cb53-4)make
[](#cb53-5)make strip
[](#cb53-6)sudo make install
```

That’s all there is to it. To compress a JPEG file, run the `jpegoptim foo.jpg` command (replace *foo.jp* with the actual path and name of the JPEG file).

By default, jpegoptim uses the lossless compression algorithm, but you can override this by specifying the maximum image quality using the `--max` parameter. In addition to compressing the file, jpegoptim can also remove metadata. The `--strip-exif` parameter, for example, removes all EXIF data, while the `--strip-iptc` parameter removes IPTC data.

jpegoptim offers several other useful options, and you can view them all, along with their explanations, using the `man jpegoptim` command.

# Color management on Linux

The purpose of color management is to produce consistent color output across different devices. This definition might sound simple enough, but understanding the mechanics of color management and implementing a color-managed workflow can be a rather complex and at times confusing affair. The following description can help you to get an understanding of color management fundamentals and set up a color-managed environment using open source Linux tools.

## Color management in a nutshell

The need for color management arises from the fundamental problem of color reproduction: a formal representation of a given color (e.g., numeric value of the color in a specific color model) doesn’t necessarily produce the same color on different devices due to a wide variety of factors. Thus the primary goal of color management is to achieve a consistent color reproduction across devices. So, for example, a photo taken by a color-managed camera should look the same on a color-managed computer screen.

In a color-managed workflow, each device such as a digital camera and LCD display has its own color profile which characterizes the color response of that particular device. Each color profile describes these colors relative to a standardized set of reference colors. Color-managed software then uses these standardized profiles to translate color from one device to another. This is usually performed by a color management module ([Overview of color management by Cambridge in Colour](http://www.cambridgeincolour.com/tutorials/color-management1.htm))

Color profiles are closely related to the concept of color space. A color space is a defined range of colors, or as Thom Hogan puts it, “a Color Space defines what is possible.” ([Thom’s Quick & Dirty Guide to Color Management](http://www.bythom.com/qadcolor.htm)). Put it in another way, a color space determines the color capabilities of a specific device or application. While a color space contains color definitions, a color profile describes the color input or output of a device.

Since there are several established color spaces, the question is which one you should choose. A detailed answer to that question deserves a separate discussion, but the simple truth is that the sRGB color space is adequate for general use. Developed specifically for the Internet, sRGB is smaller compared to other color spaces (most notably Adobe RGB), but it’s widely supported by manufacturers and developers, and it’s a default color space on virtually any device and application that supports color management. digiKam, for example, uses sRGB as its default working color space (i.e., the color space in which color data is meant to be manipulated). When choosing a color space, consider the following: 1) sRGB can’t be converted to a larger color space like Adobe RGB (although the opposite is true: Adobe RGB can be downsampled to sRGB), 2) there is no color space assigned to RAW files, so if you expect to use different color spaces in your workflow, you can use RAW originals to process photos in the desired color space.

Precise and consistent color management requires ICC-compliant profiles for all devices in your workflow (e.g., digital camera and LCD display). A color profile is “a set of data that characterizes a color input or output device” ([Wikipedia color profile definition](http://en.wikipedia.org/wiki/ICC_profile)). Again, Thom Hogan explains this best: “A Color Profile specifies how a device deviates from a Color Space. When we profile a monitor, printer, or sometimes a camera, we are essentially creating a map of how it differs from a Color Space definition. Savvy software can then use that map to”fix" the color when rendered on or by that device so that it matches the Color Space definitions." ([Thom’s Quick & Dirty Guide to Color Management](http://www.bythom.com/qadcolor.htm))

## Setting up a color-managed workflow with Darktable

To illustrate how the color management theory works in practice, here is a real-world scenario: You use a digital camera to take photos as RAW files which you then process on a Linux machine using Darktable and view on an LCD display connected to the machine.

The first step is to create color profiles for the camera and the display. To calibrate a monitor and generate a color profile for it on Linux, you need two things: a colorimeter and color profiling software. High-quality professional colorimeters tend to be rather expensive, but you can use the excellent low-cost [ColorHug](http://www.hughski.com) open source colorimeter instead.

When it comes to calibration and profiling, [DisplayCAL](http://displaycal.net/) is the perfect tool for the job. It provides a graphical user interface to the display calibration and profiling tools of the ArgyllCMS open source color management system. The latter is available in the software repositories of most mainstream Linux distributions, so you can install it using your distro’s package manager. On Debian and Ubuntu-based distributions, this can be done by running the `sudo apt install argyll` command. Next, you need to install the ColorHug library and client software. This software is also available in Debian and Ubuntu repositories, so it can be installed using the `sudo apt libcolorhug2 colorhug-client` command. Download then the packaged version of DisplayCAL from the project’s website and install it on your system. Connect ColorHug, and it should blink briefly, indicating that it has been detected by the system. Before you start using ColorHug, make sure that it has the latest version of firmware. Run the `colorhug-flash` command to launch the Firmware Updater utility and use it to check and upgrade ColorHug’s firmware.

![](media/file3.jpg)

Now everything is ready to calibrate and profile the display. Launch DisplayCAL and press the **Detect** button to make DisplayCAL detect the connected colorimeter (it should appear in the **Instrument/Port** section). If you are using a multi-display setup, make sure that the correct monitor is selected in the **Display device** section. Select then *Photo (D50, Gamma 2.2)* from the **Settings** drop-down list. Press the **Calibrate & Profile** button and follow the instructions to calibrate the monitor and generate its color profile. Once the color profile has been generated, DisplayCAL prompts you to install the profile and enable it during boot. By the way, you can use DisplayCAL to install an existing ICC display profile, too. To do this, press the **Load Settings** button next to the **Settings** drop-down list, and select the existing *.icc* file. Use then the **Install Profile** button to install the selected profile either globally or for the current user only.

The process of calibrating a digital camera consists of several steps:

1.  Take a RAW shot of a color calibration target
2.  Process the RAW file in digiKam without any color adjustments and save the result as a 16-bit TIFF image
3.  Generate a color matrix with ArgyllCMS and use it to create an ICC profile

First, you need to obtain a color calibration target. Like colorimeters, professional color targets are rather expensive. Fortunately, Wolfgang Faust offers low-cost [IT8-compliant color targets](http://www.targets.coloraid.de) for calibrating various devices, including digital cameras (you need the C1 target). Each target production run is unique, so each batch of color targets is identified by its charge number (e.g., *R131007*), and every calibration target is supplied with its own reference file (e.g., *R131007.txt*).

The first step is to take a RAW shot of the color target using the camera you want to profile. This is actually trickier than it sounds, and the [How to Make a Camera Input Profile Target Shot](http://ninedegreesbelow.com/photography/camera-profile-make-target-shot.html) article offers valuable information on the subject. Once you have the shot, launch Darktable and import the RAW file. Disable the **base curve** module, crop the photo to remove the background, and save the result as a 16-bit TIFF file.

![](media/file4.jpg)

To read the color patch values of the created TIFF file, use the following command (replace *DSC00001.tif* with the actual name of the TIFF file and *131007.txt* with the reference file):

```
scanin -v -p -a -dipn DSC00001.tif /usr/share/color/argyll/ref/it8.cht R131007.txt
```

Open the generated *diag.tif* file and make sure that all color patches have been indexed. Finally, generate a color profile, using the actual values instead of the default ones:

```
colprof -v -A "SONY" -M "SONY NEX-3N" -D "sony nex-3n" -C "Copyright (c) 2016 Dmitri Popov. Some rights reserved." -q l -a m -u DSC00001
```

The final step is to add the created camera color profile to Darktable. To do this, move the generated *.icc* file to the *~/.config/darktable/color/in/* folder (create the missing directories if they don’t exist). Launch the application and open a RAW file for editing. Enable then the **input color profile** module, and select the created camera profile in the **profile** drop-down list in the module’s pane.

# Manage and edit photos with gThumb

Managing and editing photos and RAW files is a key step in a photographic workflow. While there are plenty of excellent and powerful tools available at your disposal, [gThumb](https://live.gnome.org/gthumb) can handle most management and editing tasks with a minimal overhead. It may look like a regular image viewer, but behind its unassuming appearance hides a rather capable application for retouching photos and keeping tabs on them. Since gThumb is available in the official software repository, you can install using the `sudo apt install gthumb` command.

![](media/file5.jpg)

gThumb features a lightweight interface that puts all essential tools right at your fingertips. The directory tree in the left panel lets you easily traverse the file system and open folders containing photos. And the application features a couple of creature comforts that make directory navigation more efficient. When you launch gThumb, it automatically switches to the last-used directory. The application also keeps track of visited directories, and you can jump to any previously opened directory using the **History** button. You can also bookmark a specific directory using the **Add Bookmark** command under the **Bookmarks** button.

gThumb offers basic import functionality that makes it possible to offload files from external storage devices and pull photos from popular services like Flickr and Facebook. To do the latter, press on the hamburger menu in the upper-right corner of gThumb’s window and select the desired service from the **Import From** menu. Authenticate gThumb with the service, pick the photos you want, and the application imports them into the currently opened directory. You can use the **Removable Device** and **Folder** commands in the **Import From** menu to import photos from external storage devices (SD cards, USB keys, etc.) and local directories.

The application supports most popular graphics formats, including JPEG, PNG, TIFF, and many others. Better still, gThumb features a dedicated command for converting photos between different formats. To convert a photo to a different format, press the **Tools** button in the upper-right corner of gThumb’s window and choose the **Convert Format** command. Other commands under the **Tools** button can be used to rotate and resize images as well as change their dates.

When you select a directory in the left panel, gThumb displays photos from it as thumbnails in the main area. Select a photo, and you should see information about it in the **File properties** section of the left panel. The **Details** button below this section lets you view the photo’s metadata, while the **Histogram** button displays the photo’s histogram.

![](media/file6.jpg)

Clicking on a thumbnail switches gThumb into the full-view mode, with a main pane displaying a large version of the photo and a thumbnail bar at the bottom. The button group on the left side of the main toolbar can be used to switch between different views (*Set to actual size*, *Fit to window*, *Fit to width*, and *Fit to height*), while the buttons in the group on the right side toggle the **Properties** and **Edit file** panels as well as evoke **Comment** and **Tags** dialog windows.

gThumb’s filtering functionality can be useful for narrowing the displayed photos to items that match certain criteria. For example, you can define a filter that shows photos taken on a specific date or having a matching text in their descriptions. To configure and enable a filter, select **Personalize** from the **Show** drop-down list in the bottom bar, and select the desired items from the list of default filters. Alternatively, you can define custom filters by pressing the **New** button and defining one or multiple filtering rules.

## Organize photos in gThumb

If you use tags to keep tabs on your photos, you’ll appreciate gThumb’s tagging functionality. To quickly assign one of the existing tags to a specific photo, right-click on it and choose the desired tag from the **Tags** menu (or use the **C** keyboard shortcut). You can then select the tags you want. To create a new tag, enter its name into the **Tags** field, and select the **Create tag** command from the appeared drop-down list. To add a description to the photo, choose the **Comment** command from the right-click context menu (or press the **C** keyboard shortcut). This opens the **Metadata** dialog window, where you can enter a description and specify other metadata properties, such as title, place the photo was taken, tags, and rating.

![](media/file7.jpg)

Flags, or selections in gThumb’s terminology, is another useful feature for organizing photos. Using the **Alt+1…3** keyboard shortcuts, you can assign green, red, and blue flags to the currently selected photos. This feature can be put to a variety of uses. For example, you can flag your best photos you want to share immediately using the green flag, and add the red flag to photos that need further retouching. The **Selections** entry at the bottom of the directory tree in the left panel lets you view photos grouped by flag (e.g., the **Selection 1** section shows photos with the red flag). To quickly view the selection you need, use the **Ctrl+1…3** keyboard shortcuts.

To make it easier to keep tabs on photos, gThumb allows you to group photos into catalogs and libraries. Catalogs are basically virtual folders: adding a photo to a catalog simply creates a reference to the original file, without physically moving the photo. Multiple catalogs can be grouped into libraries. This relatively simple functionality offers a flexible mechanism for organizing photos. For example, you can create separate catalogs for different countries (e.g., *Japan*, *Germany*, *France*, etc.), and then group the catalogs into the *Travel* library.

The **Organize** button in the upper-right corner can be used to automatically generate catalogs based on several criteria, such as dates and tags. It’s also possible to create custom catalogs and libraries and populate them with photos manually. To create a new catalog or library, right-click on the **Catalogs** entry at the bottom of the directory tree in the left panel, choose the **Create Catalog** or **Create Library** command, give the new item a descriptive name and press **Create**. To add a photo to the catalog or library, right-click on the photo and choose the **Add to Catalog** command. Pick then the target catalog or library and press **Add**. You can also use the appropriate buttons in the **Add to Catalog** dialog window to create catalogs and libraries on the fly.

## Edit photos in gThumb

When in the full-view mode, pressing the **Edit file** button opens the right panel that gives you access to editing tools. While gThumb won’t replace a dedicated image editing application, the available tools can come in handy for quickly tweaking basic settings like brightness, saturation, and contrast as well as sharpening photos and converting images to black-and-white. The dedicated **Special Effects** button in the **Color** group gives you access to several ready-made filters you can apply to your photos.

![](media/file8.jpg)

In addition to these simple features, gThumb offers a curves tool that in skillful hands can work magic on your photos. gThumb allows you to save curve adjustments as presets, so you can maintain your own library of effects. To save the current curve adjustments, press the **Add to presets** button in the main toolbar, give the preset a name, and hit **Save**. You can access the saved presets using the **Presets** button.

### Understanding curves tool

The key element in the Curves tool is the histogram that shows the input distribution of tones (X axis), and the output tones (Y axis). The left part of the X axis represents the darker tones, while the right part represents the highlights. The diagonal line (the tonal curve) indicates the ratio between input and output. Initially, the line is straight which means that the output is exactly the same as the input. Adjusting the tone curve alters the original ratio, thus changing the tonality of the image. And this is exactly what the Curve tool is designed to do. Click on the diagonal line to add a control point, then adjust the shape of the tonal curve by dragging the control point with the mouse. For more fine curve adjustment, create additional control points.

To better understand how curves work, start with a few basic curve adjustments. To boost highlights, adjust the top-right part of the tonal curve upwards. As noted above, the right part of the histogram represents the highlights, so pushing the curve in the Luminosity channel upwards increases the brightness of the image. Among other things, this technique can be used to produce a high-key lighting effect. Another common adjustment is giving the tonal curve the S shape by raising the upper half of the curve and lowering the lower half of it. This effectively brightens the lighter areas of the image and darkens the darker areas. This, in turn, increases the overall contrast of the image without affecting exposure.

While the Luminosity channel allows you to adjust the tonal curve, the Red, Green, and Blue channels can be used to control the contribution of each color in specific tonal regions of the image. For example, pushing the lower part of the curve in the Red channel downwards decreases the contribution of red in the dark tones, thus making shadows cooler.

![](media/file9.jpg)

But what if you want to make highlights look warmer by increasing the amount of yellow? There is no Yellow channel in the Curves Adjust tool, so instead you need to consult the HSV color circle to determine which color you have to subtract to get yellow. To do this, look at the color opposite to yellow, which is blue. So to warm the highlights, you need to decrease the amount of blue by pushing the upper part of the curve in the Blue channel downwards.

## gThumb and RAW files

Although gThumb is not designed to replace a dedicated RAW processing tool, the application does make it possible to preview RAW files, perform basic editing, and save the resulting photo in one of the supported formats. And in many cases, that’s all what many users will ever need. Working with RAW files in gThumb is no different from dealing with regular photos. The only thing you need to keep in mind is that after you’ve applied adjustments to a RAW file, you need to use the **Save as** command to save the edited photo in a supported format.

## Share photos with gThumb

Want to share your photographic masterpieces with the world? The **Export** button on the main toolbar lets you upload photos to several popular photo sharing services like Flickr and Facebook. In addition to that, the application can also generate a static web album you can publish on your own website. And if you want to create collages to amuse your friends and family, the **Imagewall** export tool is just what you need.

# Process RAW files with Darktable

Photo management software like gThumb and digiKam can help you to process, organize, and manage your photos, but if your photographic workflow is built around RAW files, then you might consider a more specialized application like [Darktable](http://darktable.sourceforge.net/). This software darkroom offers a wide range of powerful tools for sorting and processing your digital negatives.

Although Darktable is designed for serious amateurs and professional photographers alike, the application features an elegant and user-friendly interface that puts all the essential tools at your fingertips and makes it easy to get to grips with this powerful application. More importantly, Darktable relies on the RawSpeed decoder library which supports virtually any RAW variant out there, including CRW/CR2, NEF, RAF, DNG, and many others. Moreover, Darktable comes with custom-enhanced color matrices that provide better color rendition. And to reproduce the behavior of some camera sensors, the Darktable developers have reverse-engineered base curves (visit the [Camera Support](http://www.darktable.org/resources/camera-support/) page for a list of supported cameras).

## Install Darktable

The first order of business is, of course, to install Darktable on your machine. Binary packages of Darktable are available for popular LInux distributions like Ubuntu, openSUSE, and Fedora, so installing the application on these distros is not particularly complicated. For Ubuntu users, the project provides two PPAs: the [Darktable Release PPA](https://launchpad.net/~pmjdebruijn/+archive/ubuntu/darktable-release) contains the current stable version of Darktable and the [Darktable Unstable PPA](https://launchpad.net/~pmjdebruijn/+archive/ubuntu/darktable-unstable) offers development versions of Darktable. Adding the desired PPA and installing Darktable from it is a matter of executing three simple commands in the terminal:

```
sudo add-apt-repository ppa:pmjdebruijn/darktable-release-plus
sudo apt update
sudo apt install darktable
```

## Manage RAW files in the Light Table mode

When you launch Darktable for the first time, you are automatically dropped into the **lighttable** interface designed for importing, sorting, and organizing RAW files. The **lighttable** interface offers several ways to import RAW files into the application. Use the **image** button in the **import** palette to grab a single photo, or press the **folder** button to import a directory containing RAW files as a film roll.

![](media/file10.jpg)

The **collect images** palette provides tools for keeping tabs on the imported RAW files. By default, all RAW files are displayed as film rolls, but there are other options for you to choose from. For example, you can display RAW files by camera model. To do this, select the **camera** item from the drop-down list in the **collect images** palette. This can come in handy when you use several digital cameras with Darktable. Want to display photos taken on a given date? Select the **date** item from the drop-down list, and pick the desired item from a list of dates.

Although the **lighttable** interface is geared towards sorting and filtering RAW files, it hides a rather nifty feature in the **selected images** palette. Press the **create hdr** button, and Darktable combines multiple images of the same subject with different exposures into a single file with an improved dynamic range.

Darktable offers two handy features for triaging and sorting the imported RAW files: color labels and stars. Used in combination, they provides a flexible mechanism for organizing RAW files. How you use both features is completely up to you. For example, you can use stars to assign ratings to photos, and then use color labels to specify processing priority.

No photo management application is complete without metadata editing and tagging capabilities, and Darktable is no exception. The **metadata editor** palette in the **lighttable** interface allows you to add and modify key information about the currently selected photo or a set of photos, including title, description, author, and rights. The **tagging** palette makes it possible to create, manage, and assign tags to the currently selected photos. This palette has two sections: the lower section is used to create and delete tags, while the upper section lets you attach or detach existing tags to the currently selected photos. The **collect images** palette mentioned earlier can also filter photos by metadata. Select, for example, the **tag** item from the drop-down list in the palette, and you should see a list of all available tags. Pick then the desired tag from the list to view the matching photos. In a similar manner, you can filter photos by title (the **title** item) and description (the **description** item).

![](media/file11.jpg)

## Process RAW files in the Darkroom mode

Once you’ve added and organized RAW files, it’s time to process them. To open a RAW file for processing, double-click on it. This opens the file in the **darkroom** interface where you process your digital negatives. Similar to **lighttable**, all tools in the **darkroom** interface are grouped into palettes. The interface itself consists of two sidebars and a viewing area. The left sidebar holds palettes like **thumbnail** (displays the thumbnail of the currently processed photo), **snapshots** (lets you save the current version of the processed photo), **history** (contains a list of editing steps), and **image information** (displays key info about the photo).

Darktable uses non-destructive editing, meaning that no editing actions are applied directly to the photo. Instead all editing information is saved in an *.xmp* file, leaving the original photo untouched. The editing operations are displayed as a list in the **history** palette, and you can revert to any previous step by selecting it in the list. The clever part is that you can turn a history stack into a style, so you can apply the exact same actions to other photos in just one step. To convert the current history stack to a style, press the **create a style** button which sits next to the **compress history stack** button. Give the new style a name and description. Save the style, and you can then apply it to any photo when you are in the **lighttable** interface. Darktable also lets you save the current state of the edited photo as a snapshot. But keep in mind that these snapshots are not persistent, so they disappear when you close the application.

The viewing area in the middle provides a large preview of the currently processed photo. The thumbnail strip at the bottom of the pane lets you quickly select a photo from the current film roll and open the photo for editing. You can also use the thumbnail strip to assign star ratings to the photos, and the toolbar at the top of the main pane lets you apply color labels to the photos and filter the photos by different criteria.

The right sidebar acts as a toolbox that holds tool palettes. Palettes in Darktable are treated as modules, and you can enable and disable them at will. This allows you to customize your workspace to fit your specific photographic needs. Darktable comes with only a few key modules enabled by default, but you can easily enable other modules by picking the ones you like in the **more modules** palette. To make it easier to keep tabs on the multitude of tools Darktable has to offer, all palettes are organized into several groups like **basic**, **color**, **correction**, and **effect**.

Each module contains a number of parameters you can tweak. The **sharpen** module, for example, lets you adjust three key parameters: radius, amount, and threshold. If you are not happy with the result, you can reset all the parameters by pressing the **reset parameters** button in the top-right corner of the palette. You can also save the current parameter values as a preset which you can then easily apply to other photos. To save a preset, press the **presets** button, choose the **store new preset** command, and give the new preset a name. Darktable can apply the created preset to photos that match specific criteria. For example, you can configure the sharpen preset to be applied to all photos with a specific ISO (e.g., ISO 1600 and higher). To do this, tick the **auto apply this preset to matching images** check box and specify the desired value in the **ISO** section.

## Darktable modules

Darktable comes with a large collection modules that let you perform a wide range of processing operations: from simple crop and rotate to more advanced actions like tone mapping and color zone adjustments. Most modules are pretty straightforward in use, and you can get to grips with them by experimenting with the available parameters. Better yet, some modules like **equalizer** and **graduated density** come with several default presets, so you can use these tools without fiddling with different parameters.

In addition to essential modules like **base curve**, **exposure**, **white balance**, and **crop and rotate**, Darktable offers a few nifty tools that can help you to improve photos with a minimum of effort. The **velvia** module, for example, boosts colors by increasing saturation in low-saturated areas of the photo, while the **bloom** tool adds or emphasizes halos in bright areas (this effect works best on photos with sharp highlights like a street light at night). As the name suggests, the **zone system** module is based on the zone system technique developed by Ansel Adams and Fred Archer. Using this module, you can adjust the contrast of specific parts of the photo. The **monochrome** module can come in handy when you need to convert color photos to black and white, and the **graduated density** module lets you emulate different GND filters.

![](media/file12.jpg)

**Color zones** is another clever module which can help you to adjust the saturation and brightness of a specific color without affecting other colors in the photo. Despite the advanced behind-the-scenes processing, the module is rather straightforward in use. First, you have to pick the color you want to adjust. To do this, switch to the **hue** section, press the **eye dropper** button, and use the mouse to select the desired color area on the photo. You should see a black vertical line in the color table in the **color zones** palette. This line marks the selected color in the color table. To increase saturation, click on the **saturation** tab, and use the mouse to drag the horizontal line up to the point where it crosses the black line. In a similar manner, you can adjust the brightness of the selected color in the **lightness** section.

![](media/file13.jpg)

## Export processed photos

Once the RAW files have been processed, switch back to the **lighttable** interface to export the resulting photos. The **export selected** palette lets you configure export settings, including destination, file format, size, and color profile. Besides the ability to export photos to the hard disk, Darktable can upload the selected photos to your Flickr or Picasa Web Albums account as well as send them via email. The application supports a wide range of graphic formats, including 8-bit JPG, 8/16-bit PNG, and 8/16-bit TIFF. In the **target storage** section you can also define a rule for automatically generating a destination path using variables like `$(FILE_NAME)`, `$(PICTURES_FOLDER)`, `$(HOUR)`, `$(DAY)`, `$(MONTH)`, and others (hover the mouse over the destination path field to view a list of all available variables). The `$(HOME_FOLDER)/$(FILE_NAME)` rule, for example, saves the exported photos under their original names in the user home directory.

# Manage and process photos with digiKam

In a way, digiKam is an underappreciated application. Many Linux users may have heard that it’s a decent tool for managing photo collections, but they might not be aware of digiKam’s more advanced features and the fact that this application offers functionality that covers the entire photographic workflow. This article introduces some of digiKam’s key features and shows how they can be used to set up a complete workflow, including importing, organizing, and editing photos and RAW files.

## digiKam AppImage package

If you want to try the very latest version of digiKam, you either need to install it from a third-party repository or compile the application from source. There is also a third option: using the digiKam AppImage package. It is a single file that contains all the required files and libraries. This means that you don’t need to install anything: grab the latest AppImage package from the project’s website, make the downloaded file executable using the `chmod +x digikam-x.x.x.appimage`, then double-click on the file to launch digiKam. This convenient option does have a couple of drawbacks, though. It’s slower to launch and offers no system integration. Also, it’s not possible to modify the application’s files, so you can’t replace the default splash screen and add custom presets.

## Importing photos and RAW files

digiKam features a rather capable import module that makes it possible to transfer photos and RAW files from your camera into the application as well as process and organize them on the fly. In fact, the **Import** interface box offers a few clever features that allow you to configure the import operation. In the **File Renaming Options** section in the **Settings** right sidebar, you can define a custom rule which renames all incoming photos. Say, you want to rename imported photos using their date and time info pulled from EXIF metadata. Enable the **Customize** option and select the *Date & Time* item from the **Options** drop-down list. From the drop-down list next to the **Format** field, select the desired date and time format. The available options include Standard, ISO, Text, UnixTimeStamp, and Custom. The latter allows you to specify your own data and time format. For example, enter the *yyyyMMdd-hhmmss* rule in the **Format** field to rename photos as follows: *19730917-175735*.

![](media/file14.jpg)

The options available in the **Auto-creation of Albums** section can come in handy in several situations. If you are downloading photos taken on different dates, enable the **Date-based sub-albums** option and choose the desired date format. This will organize imported photos in albums by date. The **Extension-based sub-albums** option can be useful for importing photos in different formats into separate albums. For example, if you shoot in both RAW and JPG, you can enable the **Extension-based sub-albums** option, so photos will be imported into appropriate folders based on their file extensions. Finally, the **On the Fly Operations** section allows you to configure several actions to be performed on the photos during the import process. Among other things, you can let digiKam auto-rotate photos and convert them to another format like PNG or TIFF.

## Sort photos with Image Quality Sorter

Here’s a problem that may sound familiar. You return from a trip with hundreds and even thousands of photos, and some of them are underexposed, out of focus, or too noisy. Weeding them out manually is like catching fish with a spoon. This is where the Image Quality Sorter tool in digiKam can prove its worth. To enable it, choose **Settings → Configure digiKam**, switch to the **Image Quality Sorter** section, and tick the **Enable Image Quality Sorting** check box. While you can modify the available settings, you might want to try the default values first. Create a separate album containing both good and low-quality photos, then run the image quality sorter with the default values on it. Adjust then specific parameters, if necessary. The Image Quality Sorter feature is part of the Maintenance tool. To process existing photos in all or selected albums, choose **Tools → Maintenance**, enable the **Image Quality Sorter** option and run the maintenance operation. The Image Quality Sorter then goes through the photos and flags them according to their quality.

![](media/file15.jpg)

## Color labels and picks

Like any other decent photo management application, digiKam allows you to assign tags to photos and RAW files. But in addition to tags, digiKam also offers the Color Labels and Picks features that can be useful for keeping tabs on your photos. To add a color label to an individual photo, right-click on it, choose **Assign Labels → Color**, and pick the desired color. Each color label has its own shortcut, so you can quickly label photos using the keyboard. For example, to assign the Magenta label, press **Ctrl+Alt+6**. To quickly remove a color label from a photo, press **Ctrl+Alt+0**. The Picks feature works in a similar manner: you can assign one of three picks (Pending, Accepted, or Rejected) to any photo in digiKam via the **Assign Labels → Pick** context menu, or using the default shortcuts. Keep in mind that the Image Quality Sorter tool uses the picks to flag photos, so to avoid confusion, you might want to avoid using picks when this tool is enabled.

digiKam provides two ways to find photos with specific color labels or picks. The **Labels Filter** section in the **Filters** sidebar lets you filter photos in the currently viewed album by color labels and picks. Using filtering capabilities can be useful when you need to specify multiple filtering criteria (e.g., show all photos with green and orange color labels as well as the Pending pick), but you can only view one album at a time.

![](media/file16.jpg)

If you need to quickly filter photos by one or two criteria, the **Labels** left sidebar is the way to go. The sidebar contains a list of all labels supported by digiKam grouped by their type: rating, pick, and color. Select the desired label to view all matching photos. You can select several labels by clicking on them with the mouse while holding down the **Ctrl** key. It’s worth noting that quick filters in the **Labels** left sidebar are applied to the entire digiKam photo collection (as opposed to filters defined in the **Filters** right sidebar that are applied to the currently selected album).

## Geotag photos in digiKam

If your camera doesn’t support geotagging, you can easily add geographical coordinates to your photos using digiKam. In digiKam, select the photos you want to geotag and choose **Item → Edit Geolocation**. This opens the **Geolocation Editor** interface consisting of three parts: the map pane contains a map and a toolbar with several navigation tools; below the map pane, there is a list of selected photos; the sidebar on the right displays the currently active section.

To geotag photos, you need to obtain the geographical coordinates of the place, where the photos were taken, and the geolocation editor offers several ways to do this. You can use the mouse to move around the map to locate the desired spot. If you know the full or partial address of the location, you can use the built-in search feature to find it on the map. Switch to the **Search** section and enter the address in the search field. Hit the **Search** button, and you should see a list of matching results with corresponding markers on the map.

![](media/file17.jpg)

The easiest way to add geographical coordinates to the photos is to drag them from the list onto the desired spot on the map. Alternatively, you can assign the geographical coordinates of a specific search result to the photos. To do this, select the photos in the list, right-click on the desired search result, and select *Move selected images to this position* from the context menu. Once you’ve assigned the geographical coordinates to the photos, press the **Apply** button to write geotags to the photos.

digiKam also makes it easy to find geotagged photos. Need to find all the photos you took in Japan? You can use the **Map** sidebar to do just that, provided your photos have been geotagged. Expand the **Map** sidebar, and you should see thumbnails representing groups of geotagged photos on the map. Each thumbnail contains a counter indicating the number of photos found in the specific area. Click on the **Pan Mode** button in the map toolbar to control the map using the mouse.

![](media/file18.jpg)

To view all photos represented by a thumbnail, press the button which creates a region selection from a thumbnail (middle button in the **Search by area** section). Using the area selection button in the **Search by area** section, you can view all photos in the manually selected area on the map. To do this, press the button, then click somewhere on the map and draw a rectangle around the desired area.

digiKam also lets you save map searches. This way, you don’t have to perform the same map search every time you need to find photos in a specific region. Enter a name for your search in the field below the map and hit the **Save** button. This adds the search to the **Map Searches** section, and you can activate the saved search at any time by clicking on it.

## Search and filter photos

Designed to manage hundreds and even thousands of photos, digiKam provides powerful searching capabilities that can help you to find the photos you want in several different ways.

If you need to quickly locate or filter photos, your first stop should be the **Filters** right sidebar. Here, you can use a list of all available tags in the **Tags Filter** section to quickly locate photos containing specific tags. Select one or several tags, and digiKam returns all matching photos in the current album. To use the rating filter, specify the desired number of stars, and digiKam narrows the view to the matching photos. By default, the rating filter uses the Greater Than or Equals condition, but you can choose between two other options by selecting them from the **Rating Filter Options** drop-down list.

![](media/file19.jpg)

While the quick search and filtering features can help you to find the photos you want with a minimum of fuss, keep in mind that the results they return largely depend on the quality and completeness of the metadata of each photo. This is also true for digiKam’s more advanced search features, so to be able to use them to their full potential, you should tag and rate your photos and add as much information as possible.

Besides the quick search and filtering tools in the **Filters** right sidebar, digiKam offers more advanced search features accessible via the left sidebar. Here, you’ll find a variety of search options, including the Calendar, Tags, Timeline, Searches, Fuzzy Searches, Map Searches and People.

The **Dates** section lets you quickly find photos for a specific year, month, and date. Using the tree in the main pane you can easily locate the year and month you want. Select the desired month and digiKam promptly displays related photos. Want to view photos taken on a specific date? You can do this using the calendar at the bottom, where dates containing photos are marked in bold. Click on the date you want to view the related photos.

![](media/file20.jpg)

The **Timeline** section offers another way to locate and view photos for a specific period of time. All photos here are presented as a bar chart, and you can view photos for a specific period by clicking on the related bar. The **Time Unit** drop-down list lets you specify the desired time scale for the chart: Year, Month, Week, and Day. The **Timeline** section has another clever trick up its sleeve: you can save searches as virtual albums. To save the current search, give it a name in the field right below the timeline and press the **Save** button. This adds the virtual album to the **My Date Searches** list.

![](media/file21.jpg)

The **Search** section lets you perform searches in a more traditional way. Type the search term in the **Search** field and digiKam automatically displays the matching photos in the main pane. To make your search more precise, press the **Advanced Search** button. This opens the **Advanced Search** interface that allows you to search photos using a wide range of criteria: from tags and image properties, to specific text and metadata values. When configuring an advanced search query, you can at any time press the **Try** button to see whether it returns the photos you are looking for. Once you’re satisfied with the result, you can save the search for later use. Give the search a name in the **Save Current Search** section and press the **Save** button. You can then run the search by selecting it in the **My Searches** list.

## Process RAW files in digiKam

digiKam usually does a decent job of decoding RAW files using the default settings. But if you prefer to have complete control of how the application processes RAW files, choose **Settings → Configure digiKam**, switch to the **Image Editor → RAW Behavior** section, and enable the **Always open the Raw Import Tool to customize settings** option. Next time you open a ra file for editing, digiKam drops you into the **RAW Import** module, where you can tweak the RAW import and post-processing settings.

The **RAW Import** sidebar contains three tabs: **RAW Decoding**, **Post Processing**, and **Info**. The **RAW Decoding** section gives you access to settings that let you tweak demosaicing, white balance, noise reduction and chromatic aberration correction, and color management settings.

![](media/file22.jpg)

Demosaicing is a process of reconstructing a full color image from the RAW output of an image sensor. The LibRaw library that digiKam uses for processing RAW files supports several demosaicing algorithms, including Bilinear, VNG, AHD, LMMSE, and others. You can use the **Shift+F1** keyboard shortcut to view a brief, and rather technical, description of each algorithm. But the best way to see the differences between various algorithms is to try to apply them to the currently opened RAW file. Select the algorithm you want, and press the **Update** button to preview the result. The preview pane displays an image that will be imported in the editor, and you can use the zoom slider at the bottom of the window to zoom in on the image for closer examination.

By default, digiKam converts RAW files into 8-bit color images, but you can choose the 16-bit mode instead by enabling the **16 bits color depth** option. The 8-bit mode is faster, but the 16-bit conversion is by far the best way to go, as it provides better tonal range. If you choose to work in the 16-bit mode, it’s recommended that you enable and configure color management options in the **Color Management** section to prevent dark rendering of the image in the editor. Due to the way certain algorithms process green pixels, the resulting image can contain undesirable patterns and artifacts. Enabling the **Interpolate RGB as four colors** option can fix that. The **Do not stretch or rotate pixels** option is there specifically for Fujifilm’s cameras with the Super CCD sensors and cameras using sensors with non-square pixels. When this option is enabled, the image is titled 45 degrees, so that each output pixel corresponds to one RAW pixel. This option also prevents the image from stretching to its correct aspect ratio.

In the **White Balance** section, you can adjust white balance settings and specify how the system should handle highlight clippings (overexposed areas in the photo). LibRaw offers several algorithms for restoring highlight clippings (Solid White, Unclip, Bend, and Rebuild) and you can view their brief description by using the **Shift+F1** keyboard shortcut. To process highlights more accurately, enable the **Correct false colors in highlights** option. And if you want LibRaw to automatically adjust brightness, tick the **Auto Brightness** check box. Besides white balance, you can also enable and adjust the **Exposure Correction** option and manually tweak exposure compensation settings. The under- and overexposure buttons at the bottom can identify under- and overexposed areas of the photo in the preview pane, which can help you to adjust exposure settings.

Using the options in the **Corrections** section, you can choose to apply one of the supported noise reduction algorithms to the image as well as enable the chromatic aberration correction option and adjust its settings. And in the **Color Management** section, you can specify a color profile and a color space.

Under the **Post Processing** tab, you can adjust several exposure settings (e.g., brightness, contrast, gamma, and exposure) as well as adjust the luminosity curve. While these adjustments can be performed later when editing the converted image, you can do this during the RAW import to streamline the editing process. digiKam applies all adjustments to the preview image, so you can immediately see the result of your tweaking without performing the actual conversion.

Once you’re satisfied with the settings and adjustments you made, press the **Import** button to import and process the RAW file. And remember: when in doubt, use the **Use Default** button to let digiKam import the RAW file using the default settings.

## Edit photos with the Levels and Curves Adjustment tools

When it comes to improving photos, Levels is an important weapon in digiKam’s arsenal. This tool lets you adjust brightness and contrast by specifying the location of complete black, complete white, and midtones in a histogram, which makes it a perfect tool for fixing under- and overexposed photos as well as improving the overall tonal range of a photo.

![](media/file23.jpg)

You can access the Levels tool in the image editor by choosing **Color → Levels Adjust**. Select **Luminosity** from the **Channel** drop-down list, and press the **Linear** button. The key element in the **Levels Adjust** pane is the histogram with the black point and white point sliders. Simply put, the black point slider controls shadows, while the white point slider controls highlights. So to darken shadow areas in the photo, move the black point slider to the right. Need to boost highlights? Move the white point slider to the left. Instead of using sliders, you can let digiKam adjust levels automatically by pressing the **Auto** button. Using this feature is often hit and miss, but you can easily revert all changes using the **Defaults** button.

Three color pickers next to the **Auto** button provide yet another way to tweak levels. To adjust shadows, press the shadow tone color picker button and click on an area in the photos that should be black. In a similar manner, you can adjust midtones and highlights using the appropriate color pickers. Adjusting levels in the Luminosity channel can help to increase contrast without affecting color saturation. To change the color balance, you can adjust levels in the Red, Green, and Blue channels (select the appropriate channel in the **Channel** drop-down list). This can be useful for boosting colors and fixing photos which suffer from unnatural color casts.

![](media/file24.jpg)

Similar to Levels, the Curves tool (**Color → Curves Adjust**) can selectively remap input tones. But unlike Levels, which has only black and white point sliders, the Curves tool can be used to control a tonal curve using any number of points.

The key element in the Curves tool is the histogram that shows the input distribution of tones (X axis), and the output tones (Y axis). The left part of the X axis represents the darker tones, while the right part represents the highlights. The diagonal line (the tonal curve) indicates the ratio between input and output. Initially, the line is straight which means that the output is exactly the same as the input. Adjusting the tone curve alters the original ratio, thus changing the tonality of the image. And this is exactly what the Curve tool is designed to do. Click on the diagonal line to add a control point, then adjust the shape of the tonal curve by dragging the control point with the mouse. For more fine curve adjustment, create additional control points.

To better understand how curves work, start with a few basic curve adjustments. To boost highlights, adjust the top-right part of the tonal curve upwards. As noted above, the right part of the histogram represents the highlights, so pushing the curve in the Luminosity channel upwards increases the brightness of the image. Among other things, this technique can be used to produce a high-key lighting effect. Another common adjustment is giving the tonal curve the S shape by raising the upper half of the curve and lowering the lower half of it. This effectively brightens the lighter areas of the image and darkens the darker areas. This, in turn, increases the overall contrast of the image without affecting exposure.

While the Luminosity channel allows you to adjust the tonal curve, the Red, Green, and Blue channels can be used to control the contribution of each color in specific tonal regions of the image. For example, pushing the lower part of the curve in the Red channel downwards decreases the contribution of red in the dark tones, thus making shadows cooler.

digiKam provides the ability to save the current curve profile as a preset as well as load existing curve presets using the **Save as** and **Load** buttons in the right sidebar. The curves are stored in the GIMP-compatible format, so you can use curves created with GIMP in digiKam and vice versa.

# Color transformations with Hald CLUT

The ability to save color adjustments as a preset provides a convenient way to create presets that can be easily applied to one of several photos. But this functionality has its limitations. Firstly, presets are usually application-specific, so presets created with one photo editing tool don’t work with other applications. Secondly, some applications provide only limited support for presets. digiKam, for example, lets you create curve presets only. And lastly, presets can normally be used from within the application itself, which makes it impossible to automate actions involving presets using scripts.

The [Hald CLUT](http://www.quelsolaar.com/technology/clut.html) technology overcomes these and other shortcomings. The author of Hald CLUT explains it best:

> Any color correction can be expressed as a Color LookUp Table or CLUT (some times written as “Color LUT”). This is a 3D dimensional table where all colors are represented in color space. For each color in the color lookup table there is a destination color value that corresponds to what the particular color becomes when it is corrected using the CLUT. These tables are by nature 3-dimensional (Red Green and Blue) and therefore special file formats are used to store them. Hald CLUTs however have been converted to a 2D space and since tables store colors the CLUT can be be saved as an image, in any non destructive image format.

Simply put, Hald CLUT is a two-dimensional color table that is used as a reference for applying color corrections to an image. Thanks to the fact that the [ImageMagick](http://www.imagemagick.org/script/index.php) image manipulation tool supports Hald CLUT, using the technology to create color adjustment presets and photo filters is not all that complicated. To install ImageMagick, run the `sudo apt install imagemagick` command (on openSUSE use the `sudo zypper in ImageMagick` command). The first thing you need to do is to create a Hald CLUT table using the following command:

```
convert hald:9 hald-9.png
```

Open then the generated *hald-9.png* file in your preferred photo editing application, apply the desired color corrections (curves, levels, saturation, brightness, etc.), and save the changes. Now you have a reference Hald CLUT table that can be used as a preset. To apply color adjustments in the table to a photo, use the command below:

```
convert foo.JPG hald-9.png -hald-clut foo-modified.jpeg
```

This applies color adjustments from the *hald-9.png* table to the *foo.JPG* image and saves the modified file as *foo-modified.jpeg*

You’ll find more info about ImageMagick and Hald CLUT at [www.imagemagick.org/Usage/color_mods/#hald-clut](http://www.imagemagick.org/Usage/color_mods/#hald-clut)

## Practical example

digiKam makes it possible to create photographic effects using a combination of curves, hue, and saturation adjustments. But here is the problem: digiKam can’t save all these adjustments as a single preset (you can save curve presets only). Normally, this would mean that you have to make the same adjustments manually every time you want to apply a certain photographic effect to a photo, which is not very practical. This is where the Hald CLUT technology can help.

Create a Hald CLUT table, open it in digiKam and apply the desired curves, hue, and saturation adjustments. Save the modified table in the PNG format, and you are done. Next time you want to apply the created photographic effect to a photo, use the *convert* tool to perform image transformation based on the created Hald CLUT table. Better still, this technique makes it possible to apply the same effect to multiple photos. The following command uses a Hald CLUT table to transform multiple photos in the JPEG format:

```
for file in *.jpg; do echo "$file"; convert "$file" hald-9.png -hald-clut "$file"; done
```

## Shell script to apply multiple Hald CLUT presets

Hald CLUT files offer a straightforward way to apply color corrections to an image with a single command:

```
convert foo.JPG hald-9.png -hald-clut foo-modified.jpeg
```

But what if you have a handful of Hald CLUT files and you want to apply them all to a specific photo? A relatively simple Bash shell script can automate this otherwise tedious task:

```
#!/usr/bin/env bash
if [ -z "$1" ]; then
  echo "Specify the required parameter."
  exit 1
fi
dir="hald-clut"
if [ ! -d "$dir" ]; then
  mkdir -p "$dir"
fi
for file in *.png; do
  prefix="${file%.*}"
  bname=$(basename "$1")
  echo "Applying $file Hald-CLUT ..."
  convert "$1" "$file" -hald-clut "$dir/$prefix-$bname"
done
```

The script picks *.png* Hald CLUT files in the current working directory one-by-one and applies them to the specified image file. The modified files are saved in the separate *hald-clut* directory, and each file is prefixed with the name of the applied Hald CLUT file.

Here is how this works in practice. First of all, paste the code above into a text file and save it under the *hald-clut* name. Use then the following commands to copy the created file to the */usr/local/bin* directory and make the script executable:

```
sudo cp hald-clut /usr/local/bin/
sudo chown root:root /usr/local/bin/hald-clut
sudo chmod 755 /usr/local/bin/hald-clut
```

Now, let’s say you want to apply all Hald-CLUT presets in the *hald-clut-files* directory to the *foo.JPG* file. In the terminal, switch to the directory, and run the `hald-clut path/to/foo.JPG` command (replace *path/to/foo.JPG* with the actual path to the desired file). This apply all presets to the *foo.JPG* image and saves the resulting files in the *hald-clut-files/hald-clut* directory.

## Use Hald CLUT presets with Lilut

If you happen to use digiKam, RAWTherapee, or any other photo editing application that supports Hald CLUT, you might already have a handful of favorite presets. But what if you want to use these presets even when you don’t have access to your photo editing application? [Lilut](https://gitlab.com/dmpop/lilut) to the rescue. This simple PHP-based tool makes it possible to upload a photo from any device and apply any of the available Hald CLUT presets.

![](media/file25.jpg)

Lilut can run on any web server with PHP. The only additional requirement is the *php-imagick* package that must be installed on the server. If your server runs a Debian-based Linux distribution, you can install the package using the `sudo apt-get install php-imagick` command. On openSUSE, the command is `sudo zypper in php7-imagick`. The default PHP configuration limits the size of uploaded files to a mere 2MB. To change that, open the *php.ini* file for editing (e.g., `sudo nano /etc/php7/cli/php.ini`) and adjust the value of the `upload_max_filesize` parameter.

To deploy Lilut, clone the project’s Git repository using the following command:

```
git clone https://gitlab.com/dmpop/lilut.git
```

Alternatively, grab the last source code as a ZIP file and extract the downloaded archive. Put your Hald CLUT files into the *luts* folder, and move the entire *lilut* directory to the document root of the web server. Point then the browser to *127.0.0.1/lilut* (replace *127.0.0.1* with the actual IP address or domain name of the server), and you should see Lilut’s main page.

# Backup and recovery

There is more to backup than having a copy of your photo library on an external hard disk. You should also consider implementing a cloud backup system and a solution for keeping your photos safe when you are on the move.

## Cloud backup with rclone

Cloud storage is cheap nowadays, and there are plenty of storage providers to choose from. So there is no excuse for not having an off-site backup system for keeping your files safe. There is a fly in the ointment, though. Many cloud storage services want you to use their own proprietary graphical client applications. Worse still, some services don’t provide Linux clients at all. Fortunately, there is [rclone](http://rclone.org/), a small open source utility that can talk to many popular cloud storage services. rclone can also handle local file systems, so you can use it for local backup, too. The utility is straightforward in use, so there is no learning curve to speak of.

### Install rclone

Written in Go, rclone is distributed as a self-contained binary file with no dependencies, and it will happily run on the x86, AMD64, and ARM platforms. Installing rclone is not difficult, but it does require a bit of manual work. Grab the latest release of the tool for the appropriate Linux platform from the project’s website. Unpack then the downloaded archive, and switch to the resulting directory in the terminal. Copy then the binary executable to the */usr/local/bin/* directory and change the file’s permissions:

```
sudo cp rclone /usr/local/bin/
sudo chown root:root /usr/local/bin/rclone
sudo chmod 755 /usr/local/bin/rclone
```

To install rclone’s man pages, run the following commands:

```
sudo mkdir -p /usr/local/share/man/man1
sudo cp rclone.1 /usr/local/share/man/man1/
sudo mandb
```

### Install rclone on Android

It’s also possible to install and run rclone on an Android device. This can be useful if you want to back up photos stored on your device, or use the device to transfer photos from a camera and then back them up. Deploying rclone on Android requires the [Termux](https://termux.com/) app, so the first order of business is to install it on your device either via Google Play Store or F-Droid. Launch then Termux an run the following commands to install rclone:

```
pkg update
pkg install golang git
export GOPATH=`pwd`/go
mkdir go
go get -u -v github.com/ncw/rclone
```

Use the `./go/bin/rclone version` command to confirm that the rclone has been installed. Enable then access to Android’s storage:

```
pkg install termux-api
pkg termux-storage-setup
```

You can then use rclone as described below, but remember to replace `rclone` command with `./go/bin/rclone`.

### Configure rclone

To make rclone work with your preferred cloud storage service, you need to create a configuration file. And the utility has the special `config` subcommand that allows you to do just that. Say, you want to use rclone with the [Amazon Drive](https://www.amazon.com/clouddrive/) service. Run the `rclone config` command, press **n** when prompted to set a configuration password, and name the configuration profile *remote*. Enter then the number corresponding to the Amazon Drive option in the list of supported services. Leave the *Amazon Application Client Id* and *Amazon Application Client Secret* options empty, and select the auto configuration option. This will open the default browser and obtain an access token. Check and confirm the generated settings, and you are done.

Once rclone has been configured, run the `rclone lsd remote:` command that returns all containers.

### Use rclone

rclone supports a few simple subcommands and options that allow you to access, manage, and use the remote storage. And the `copy` and `sync` subcommands are probably the most important among them. As the name suggests, the `copy` subcommand copies the contents of the source directory to the remote destination. This subcommand doesn’t transfer unchanged files (it checks them by size, modification time, and md5sum hashes), and it doesn’t delete files from the destination directory. If the destination directory doesn’t exist, rclone automatically creates it. Most rclone commands have the simple `rclone [OPTION] [SUBCOMMAND] <source> <destination>` syntax, and here is what the command that copies the contents of a specified directory to the remote destination looks like:

```
rclone copy /path/to/source remote:destination
```

Similar to `copy`, the `sync` subcommand transfers files from the source directory to the destination, skipping unchanged files. But when `sync` encounters files that don’t exist in the source directory, the subcommand deletes them from the destination. In other words, `sync` keeps both source and destination directories in sync by modifying the destination. Since this operation (and other rclone actions for that matter) is irreversible, it makes sense to test it first, and rclone provides the handy `--dry-run` option for that. Add this option to the `rclone sync` command to check what files will be copied and deleted:

```
rclone --dry-run sync /path/to/source remote:destination
```

The `check` subcommand can come in handy when you need to ensure that the files in the source and destination directories match:

```
rclone check /path/to/source remote:destination
```

This command compares files by their sizes and md5sum hashes, and then shows a list of files that don’t match.

Besides `copy` and `sync`, rclone supports several subcommands that let you view and manage remote storage. The `lsd` subcommand, for example, can be used to list all directories (also called containers and buckets) in the remote destination, while the `ls` subcommand shows all files in a specified remote directory:

```
rclone lsd remote:
rclone ls remote:dir
```

Need to create or delete a remote directory? Use the `mkdir and rmdir` subcommands for that:

```
rclone mkdir remote:new_dir
rclone rmdir remote:old_dir
```

The last command can remove a directory only if it’s empty. If you want to delete a directory and its contents, use the `purge` subcommand:

```
rclone purge remote:old_dir
```

Being a command-line tool, rclone supports a number of options that control its behavior. The `--bwlimit` option, for example, lets you limit the bandwidth available to rclone. This can be useful when the machine running rclone shares the Internet connections with other clients. Limiting the bandwidth ensures that other machines can access the Internet at a reasonable speed during the copy or sync operations. The bandwidth limit can be specified in kilobytes, megabytes, or gigabytes using the k, M, and G suffixes:

```
rclone --bwlimit=15M sync /path/to/source remote:destination
```

The command above limits the bandwidth to 15MBytes/s.

The `--dry-run` option has been mentioned earlier, and it allows you to test rclone operations without applying any changes. Finally, if you run rclone unattended, you might want to use the `--log-file` option to save rclone’s output to a file for later reference:

```
rclone --log-file=rclone.log sync /path/to/source remote:destination
```

### Use filters in rclone

Filtering options and patterns in rclone can be used to configure rclone to skip certain files and directories. Filtering rules in rclone work with most commands, including `copy` and `sync`. A filtering rule in rclone consists of two parts: an exclude or include subcommand and a filtering pattern. rclone features four filtering subcommands: `--exclude`, `--exclude-from`, `--include`, and `--include-from`. The first two commands can be used to exclude files, while the other two let you limit the current operation only to the specified files. The `--exclude` subcommand allows you to specify the filtering pattern in-line, for example:

```
rclone --exclude *.NEF sync /path/to/source remote:destination
```

This command syncs everything except the RAW files with the *.NEF* extension. Instead of specifying a filtering rule on the fly, you can save a list of filtering patterns in a text file and use the `--exclude-from` subcommand with it:

```
rclone --exclude-from=filters.txt copy /path/to/source remote:destination
```

The `--include` command can come in useful when you need to limit rclone to a specific subset of files. For example, if you want to sync TIFF and JPEG files in a directory and skip the rest, the following filtering rule does the job:

```
rclone --include *.{tif,jpg} copy /path/to/source remote:destination
```

Similar to `--exclude-from`, the `--include-from` command can read filtering patterns from a text file.

Using the exclude and include subcommands, you can create filtering rules that either skip or include matching files. But what if you need to create a set of filters that combines both? Then the `--filter-from` subcommand is what you need. This subcommand reads a text file containing include and exclude filtering rules and applies them to the current rclone operation:

```
rclone --filter-from=filters.txt sync /path/to/source remote:destination
```

Each line in the specified text files contains a filtering rule that starts with either the + (include) or - (exclude) prefix, for example:

```
+ *.jpeg
+ *.tiff
- *.MP4
- *.xmp
```

As you may have noticed, filtering patterns in rclone are based on wild cards. While they are not as powerful as regular expressions, wild cards are significantly easier to master. And if you used wild cards when working from the command line, you won’t have problems composing filtering rules for rclone.

## Detect data rot in photos and RAW files

Backup will help you to keep your photos safe, but it won’t solve another issue — data rot (also known as data decay and [data degradation](https://www.wikiwand.com/en/Data_degradation)). Data rot can occur for a number of reasons, but the result is always the same: data corruption due to one or more changed bits in the file. Usually data decay happens silently, so you probably won’t realize it happened before it’s too late. One way to combat data rot is to make sure that your have a healthy backup which you can use to restore the corrupted files and ensure that the damaged file doesn’t propagates to all your back up copies. This means that you need to check your photos and RAW files for data rot and detect corrupted files before you perform backup, and a simple Bash shell script can help you with that.

```
#!/usr/bin/env bash
shopt -s nullglob
for file in *.JPG *.jpeg *.ARW; do
    if [ ! -f "$file.sha1" ]; then
       sha1sum "$file" > "$file.sha1"
    fi
    sha1sum -c "$file.sha1" | grep "FAILED"
done
```

During the initial run, the script generates hash files using the SHA1 hash algorithm for each photo and RAW file in the current directory. The example above handles files with the *.JPG*, *.jpeg*, and *.ARW* extensions, but you can add any other file extension you need. When you run the script again, it compares the current checksum with the saved one. If they don’t match, then the file in question is either modified or damaged. If the former case (e.g., you’ve edited a photo or RAW file), just delete the related *.sha1* file. But if you haven’t modified the photo or RAW file in any way, the checksum mismatch indicates that the file might be corrupted. In this case, replace it with a healthy copy from a backup.

## Recover photos with PhotoRec

Choosing storage cards from respectable manufacturers like Transcend, SanDisk, and Lexar is the best way to ensure that you don’t lose RAW files and photos. But if disaster strikes, [Photorec](http://www.cgsecurity.org/wiki/PhotoRec) can save the day. This simple tool can recover files from damaged storage cards and bring back accidentally deleted files. PhotoRec is a part of the TestDisk package, and you can install it using the `sudo apt install testdisk` command. Although PhotoRec is a command-line tool, it’s supremely easy to use, and it gently guides you through the entire process of recovering data, providing easy-to-follow instructions along the way.

To start a recovery operation, plug the storage card into your machine and run the `sudo photorec` command. Choose the storage card from the list of detected volumes and press **Proceed**. Select then the partition you want to recover and choose its format. Specify whether you want to recover data from the entire partition or from the unallocated space on it (this is the default option, and it’s a sensible first choice). Choose a path for storing recovered files, press **C**, and wait till the recovery process is finished. You will then find the recovered data in the *recup_dir.x* (where *x* is a number) directory in the specified path. This is pretty much all you need to know to successfully recover data with PhotoRec, but you’ll find additional info about the tool’s options on the [PhotoRec Step By Step](http://www.cgsecurity.org/wiki/PhotoRec_Step_By_Step) page.

Despite its apparent simplicity, PhotoRec usually does a great job recovering data, so it makes an indispensable addition to your photographic toolbox.

# Publish and share photos with Mejiro

If you are looking for an uncomplicated and lightweight application for hosting photos on your own server, [Mejiro](http://dmpop.github.io/mejiro/) is right up your alley. Consisting of a single PHP file, Mejiro will happily run on any machine with a web server (e.g., Apache or lighttpd) and PHP, and the application is supremely easy to deploy and use.

![](media/file26.jpg)

Although Mejiro is a rather minimalist application, it does offer useful functionality and creature comforts. The application features a responsive design, so it works well on mobile devices. Mejiro automatically extracts and displays basic EXIF info for each photo, including aperture, shutter speed, and ISO. In addition to that, the application parses IPTC metadata and displays keywords assigned to photos. For geotagged photos, Mejiro shows their exact locations on OpenStreetMap or Google Maps. You can add a description to each photo in an accompanying text file, and the application can also read and show descriptions from the photo’s *UserComment* EXIF field. Better still, Mejiro automatically detects the browser language and picks the description text file with the appropriate language prefix. Mejiro uses the [is.gd](http://is.gd/) service to generate short URLs for easy sharing. For each photo in the JPEG format, you can upload the accompanying RAW file, and Mejiro automatically adds a link to it.

## Install Mejiro

To host Mejiro, you need a Linux-based machine with the Apache service, PHP, and the GD library. You also need to install the cURL tool and Git. Mejiro should work with other servers like [nginx](http://nginx.org/), but it has only been tested with Apache and lighthttpd.

### Installation with the Apache server

1.  Install the required packages using the `sudo apt install apache2 php5 php5-gd git curl` command.
2.  In the terminal, switch to the root directory of the server (e.g., */var/www*) and use the `sudo git clone https://github.com/dmpop/mejiro.git` command to fetch the latest source code. Alternatively, you can download the ZIP archive and extract it into the document root of the server.
3.  Open the *index.php* file in a text editor and edit the settings. This step is optional.
4.  Make the *mejiro* directory writable by the server using the `sudo chown www-data -R mejiro` command.
5.  Put photos into the *photos* directory.
6.  Point the browser to *http://127.0.0.1/mejiro/*, and you should see the Mejiro page.

### Install Mejiro on Raspberry Pi

Installing Mejiro on Raspberry Pi is a matter of executing the following commands in the terminal:

```
wget https://raw.githubusercontent.com/dmpop/mejiro/master/install.sh
chmod +x install.sh
sudo ./install.sh
```

These commands fetch the *install.sh* script, make the script executable, and then run the script.

## Update Mejiro

To update an existing Mejiro installation, replace the current *index.php* file with the latest one.

If you installed Mejiro directly from the project’s GitHub repository using Git, switch to the Mejiro directory and run the following command:

```
git pull origin master
```

This command pulls the latest source code from the project’s GitHub repository.

## Add photos to Mejiro

To populate Mejiro with photos, you need to upload them into the *photos* directory. You can do this by pushing photos from a local machine via SSH or FTP, or by uploading photos from an Android device via a dedicated app.

### Upload photos via SSH

The most straightforward way to upload photos from a Linux machine is to use the scp tool. To be able to use it, though, the server hosting Mejiro must run an SSH server (you can easily find instructions on installing and enabling SSH on many popular platforms). To copy a photo from a local machine to the server use the following command:

```
scp /path/to/foo.jpg user@127.0.0.1:/var/www/mejiro/photos
```

Replace *user* and *127.0.0.1* with the actual user name and IP address or domain name of the server running Mejiro.

### Use rsync to upload photos

Instead of the scp tool, you can use the good old rsync utility to upload the contents of the entire directory to Mejiro. This allows you to push multiple photos and accompanying description files with a minimum of effort. For this solution to work, you need to install the rsync software on both the server running Mejiro and your machine using the `sudo apt install rsync` command. Use then the following command to upload photos and files from a directory to Mejiro (replace */path/to/dir* with the path to the source folder):

```
rsync -avhe ssh --progress /path/to/dir user@127.0.0.1:/var/www/mejiro/photos/
```

### Upload from Android with Ghost Commander

Android-toting users can upload photos from their devices using the excellent [Ghost Commander](https://play.google.com/store/apps/details?id=com.ghostsq.commander) file manager. The app supports the FTP protocol out of the box. This means that if the machine that hosts Mejiro runs an FTP server, you can use the app to upload photos straight away. To do this, launch Ghost Commander and tap the **Home** button at the bottom toolbar. Tap then the **FTP site** entry, provide the required connection info, and press **OK**. Once a connection has been established, you can upload photos.

In case you want to upload files via SSH or SFTP, you need to install the [SFTP plugin to Ghost Commander](https://play.google.com/store/apps/details?id=com.ghostsq.commander.sftp). After you’ve done that, you can establish an SSH connection to the server using the **SFTP site** entry in the **Home** section.

## Map photos with uMap and PHP

If you happen to use a photo publishing application like [Mejiro](http://dmpop.github.io/mejiro/) that stores photos and their thumbnails in regular directories, you can automatically map your photos with [uMap](http://umap.openstreetmap.fr/) and a dash of PHP scripting. Better still, there is no need to write PHP code from scratch: you can use the script below as a starting point.

```
[](#cb86-1)<?php
[](#cb86-2)$url = "http://127.0.0.1/mejiro";
[](#cb86-3)$photos = "photos";
[](#cb86-4)$thumbnails = "thumbnails";
[](#cb86-5)function gps($coordinate, $hemisphere) {
[](#cb86-6)    for ($i = 0; $i < 3; $i++) {
[](#cb86-7)        $part = explode('/', $coordinate[$i]);
[](#cb86-8)        if (count($part) == 1) {
[](#cb86-9)        $coordinate[$i] = $part[0];
[](#cb86-10)        } else if (count($part) == 2) {
[](#cb86-11)        $coordinate[$i] = floatval($part[0])/floatval($part[1]);
[](#cb86-12)        } else {
[](#cb86-13)        $coordinate[$i] = 0;
[](#cb86-14)        }
[](#cb86-15)    }
[](#cb86-16)    list($degrees, $minutes, $seconds) = $coordinate;
[](#cb86-17)    $sign = ($hemisphere == 'W' || $hemisphere == 'S') ? -1 : 1;
[](#cb86-18)    return $sign * ($degrees + $minutes/60 + $seconds/3600);
[](#cb86-19)}
[](#cb86-20)$files = glob($photos.DIRECTORY_SEPARATOR.'*.{jpg,jpeg,JPG,JPEG}', GLOB_BRACE);
[](#cb86-21)$fileCount = count($files);
[](#cb86-22)echo "lat,lon,thumbnail,photo\n";
[](#cb86-23)for ($i=($fileCount-1); $i>=0; $i--) {
[](#cb86-24)    $file = $files[$i];
[](#cb86-25)    $photo_url = $url.DIRECTORY_SEPARATOR.$photos.DIRECTORY_SEPARATOR.basename($file);
[](#cb86-26)    $photo_url = preg_replace('/\s+/', '%20', $photo_url);
[](#cb86-27)    $thumbnail_url = $url.DIRECTORY_SEPARATOR.$photos.DIRECTORY_SEPARATOR.$thumbnails.DIRECTORY_SEPARATOR.basename($file);
[](#cb86-28)    $filepath = pathinfo($file);
[](#cb86-29)    $exif = exif_read_data($file);
[](#cb86-30)    $lat = gps($exif["GPSLatitude"], $exif['GPSLatitudeRef']);
[](#cb86-31)    $lon = gps($exif["GPSLongitude"], $exif['GPSLongitudeRef']);
[](#cb86-32)    $exif = exif_read_data($file, 0, true);
[](#cb86-33)    echo $lat.",".$lon.",".$thumbnail_url.",".$photo_url."\n";
[](#cb86-34)}
[](#cb86-35)?>
```

The script goes through each photo in the specified directory and pulls the photo’s geographical coordinates, its full path, and the path to the related thumbnail. The script then outputs the obtained data in the comma-separated format.

![](media/file27.jpg)

Copy the code, and paste it into a new text file. Specify the correct values for the **u**r**l**, *photos* and *$thumbnails* variables, and save the script under the *csv.php* name. Move the resulting file to the root of your photo sharing app installation. To see whether the script works properly, point your browser to *http://127.0.0.1/photos/csv.php* (replace *127.0.0.1* and *photos* with the actual server IP address or domain name and directory containing photos). You should see output that looks something like this:

```
lat,lon,thumbnail,photo 49.477116899982,10.988667,http://dmpop.dhcp.io/mejiro/photos/tims/20170506-155800.jpeg,http://dmpop.dhcp.io/mejiro/photos/20170506-155800.jpeg
```

Next, sign in to uMap and click the **Create a map** button to create a new map. In the right panel, click **Manage layers**. Click the **Edit** button next to the default layer, and give it a descriptive name. Expand the **Remote data** section, enter the URL to the PHP script in the **Url** field, and choose *csv* from the **Format** drop-down list. Enable the **Dynamic** and **Proxy request** options. Expand then the **Interaction options** section, and enter the following into the **Popup content template** field:

```
{{{thumbnail}}}
Source: {photo}
```

Save and reload the map, and you should see markers for each photo. Click on the marker to open its popup containing a thumbnail and the link to the source photo.

# Build static photo essays with Expose

There are plenty of reasons to use a static web site generator for web publishing instead of a traditional content management system. Serving static pages requires only a web server, which dramatically simplifies the required setup. This, in turn, improves security and reduces maintenance overhead, as the minimal stack has fewer potential vulnerabilities and is easier to troubleshoot and keep up to date. Moreover, since publishing static content can be done using a lightweight web server, you can host your site on modest hardware or an inexpensive virtual private server.

That’s all fine and dandy, but most static generators are designed to work with text-centric content like blog posts and long-form articles. But what if you want to publish a photo essay or a photo gallery? Enter [Expose](https://github.com/Jack000/Expose), a Bash shell script for generating static photo and video galleries. The script is less than a thousand lines long, but it’s capable of generating rather impressive galleries and photo essays, and offers a wide range of configurable options to boot.

![](media/file28.jpg)

## Get started with Expose

Expose has only two dependencies: ImageMagick and FFmpeg. The latter is required only if you plan to publish videos. Better still, being just a regular Bash shell script, Expose requires no installation. Start with installing the required packages. To do this on Debian or Ubuntu, run the `sudo apt install imagemagick ffmpeg` command. Installing the packages on openSUSE is also a matter of running the `sudo zypper in ImageMagick ffmeg` command. To deploy the script on your machine, clone the project’s Git repository using the following command (make sure that Git is installed on your system first):

```
git clone https://github.com/Jack000/Expose.git
```

Open then the *~/bashrc* file in a text editor and specify an alias that points to the *expose.sh* script:

```
alias expose=/script/location/expose.sh
```

Before you start using the script, you might want to edit some basic settings. You can do this either by modifying the defaults directly in the *expose.sh* script or creating a separate *_config.sh* file in the directory containing the photos you want to publish. In the latter case, configuration may look something like this:

```
site_title="Title Goes Here"
theme_dir="theme1"
social_button=false
backgroundcolor="#ffffff"
```

Expose comes with two themes: the default theme presents photos as a gallery, while the second theme is more suitable for photo essays featuring a mixture of text and images. Choosing the theme you want is a matter of specifying its name using the **theme_dir** configuration option. The **social_button** option lets you enable or disable sharing buttons, while the **backgroundcolor** option specifies the background color of the gallery.

The tool supports plenty of other options, too. If you want to allow visitors to download the published photos, use the **download_button=true** option. In this case, you also need to install the zip package using the `sudo apt install zip` command on Debian and Ubuntu or `sudo zypper in zip` on openSUSE. With the download option enabled, Expose conveniently bundles a readme file with the default copyright notice, but you can change it using the **download_readme** option, for example: `download_readme="CC BY-SA-NC 4.0"`. By default, Expose reduces image quality to 92%, but you can override this using the **jpeg_quality** option as follows: `jpeg_quality=99`. Want to give your visitor the option to add comments? Expose also provides a range of video-related options, and you can find them along with their brief descriptions in the *expose.sh* script.

:Before you run the script, you need to do some preparatory work. Expose sorts images in alphabetical order, so to arrange photos, you might want to rename them. One way to do this is to use numeric prefixes (e.g., *001_foo.jpeg*, *002_bar.jpeg*>, etc.). You can group photos in folders, and Expose generates a navigation menu based on the folder structure. To organize the folders, add numeric prefixes to them. The script strips these prefixes when generating a gallery, so they don’t appear in the navigation menu. If you want to skip a certain folder, prefix it with *_* (e.g., *_private-photos*), and Expose will ignore the folder when generating a gallery.

Using Expose couldn’t be easier. In the terminal, switch to the directory containing the photos and videos you want to publish, and run the `expose` command. This generates a complete static gallery in the *_site* directory. If you want to generate a preview, run the `expose -d` command to create a gallery with low-resolution images. Keep in mind, though, that Expose doesn’t overwrite existing images when you run the script again, so you need to delete the *_site* directory to re-generate the gallery with high-resolution photos.

## Add descriptions and settings

Adding a text description to a photo is as easy as creating a *.txt* file with the same file name as the photo. For example, to add a description to the *001_foo.jpeg* photo, create the *001_foo.txt* file with the desired text in it.

![](media/file29.jpg)

In the default theme, the specified description appears as a text overlay in the lower part of the photo. But this might not always be the most optimal text placement. Fortunately, Expose makes it possible to define text position and flow by specifying YAML configuration settings in the description file. You can specify the exact text position as well as the width and height of the text box by adding the following configuration at the beginning of the description file (all values are expressed in percent):

```
---
top: 15
left: 5
width: 25
height: 20
---
```

In this example, the `top: 15` and `left: 5` options instruct the script to place the text 15% from the top edge and 5% from the left edge of the photo. In addition to position, you can also specify text color using the **textcolor** settings:

```
---
top: 15
left: 5
width: 25
height: 20
textcolor: #ffffff
---
```

By default, the text is placed in a rectangular text box of specified width and height, but it’s also possible to make the text flow around shapes using the **polygon** option. Using it, you can specify multiple points using the X and Y values, thus turning the rectangular box into a polygon. Here is how this work in practice. Use the **width** option to specify the width of the text box, for example:

```
---
width: 50
---
```

The X and Y coordinates of each corner of the box are as follows:

```
x:0,y:0-------x100,y:0
   |             |
   |             |
   |             |
x:100,y:100-----x:0,y:100
```

The rectangular can be defined using the **polygon** option with a JSON-formatted list of coordinates:

```
polygon:[{"x":0, "y":0},{"x":100, "y":0},{"x":100, "y":100},{"x":0, "y":100}]
```

Knowing this, you can adjust the coordinates of each corner as well as introduce additional points with specific coordinates. For example, to add a left-to-right slope to the right side of the text box, adjust the X value of the top-right corner as follows:

```
polygon:[{"x":0, "y":0},{"x":25, "y":0},{"x":100, "y":100},{"x":0, "y":100}]
```

Expose uses ImageMagick for all image manipulation tasks, and you can add processing instructions to the description file for on-the-fly image adjustments. For example, if you want to watermark a specific image add the following processing instruction to its description file:

```
---
image-options: /path/to/watermark.png -gravity SouthWest -geometry +10+10 -composite
---
```

This uses the *watermark.png* image file to apply a watermark at the lower-right corner of the image, with a 10-pixel margin from the edge. Need to sharpen a photo? The following option does the trick:

```
---
image-options: -sharpen 0x1.5
---
```

You can use practically any option supported by ImageMagick, so you might want to peruse the [Command-Line Options page](http://www.imagemagick.org/script/command-line-options.php) if you want to make the most out of this functionality.

Instead of specifying options for individual photos, you can apply them globally to all published images. To do this, create the *metadata.txt* file and specify the desired options in it.

If you shoot time-lapses, you’ll be pleased to learn that Exposure can automatically encode them as videos, no manual work required. Add the **imagesequence** keyword to the folder containing time-lapse images (e.g., *001 tokyo nightscape imagesequence*) and put in the directory with the photos you want to publish. Run then the `expose` command, and the script transforms the image sequence into a video.

## In conclusion

Despite its simplicity, Exposure is a rather capable and flexible tool for generating static photo and video galleries. It gives you full control of the publishing process and allows you to configure a wide range of options. More importantly, Exposure produces galleries and essays that look exceptionally good and are easy to navigate.

# Simple PHP script for showcasing photos

A simple PHP script, the [Parsedown](https://github.com/erusev/parsedown) PHP library, and the [Sakura](https://github.com/oxalorg/sakura) minimal CSS framework are all you need to create a simple stylish page for showcasing your photos on the web. The script randomly picks a photo from a specified directory and extracts the content of the *Comment* field in the photo’s EXIF metadata. It then generates a regular HTML page containing an introductory text, the photo, and the extracted text along with a reload button, while Google Fonts and Sakura CSS framework make the resulting page look presentable.

![](media/file30.jpg)

```
<?php
$title = "Title Goes Here";
$dir = "path/to/dir";
$md = "foo.md";
$ext = "jpg";
$font = "Lato";

include('parsedown.php');

echo <<< EOT
    <!doctype html>
    <html lang="en">
        <head>
            <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <title>$title</title>
            <link href="https://unpkg.com/sakura.css/css/sakura-dark.css" rel="stylesheet" type="text/css" />
            <link href="https://fonts.googleapis.com/css?family=$font" rel="stylesheet">
            <link rel="shortcut icon" href="favicon.png" />
            <style>
                h1 { font-family:$font;font-size:2em;letter-spacing:5px; }
                p { font-family:$font;font-size:0.9em;letter-spacing:2px; }
            </style>
        </head>
        <body style="text-align: center";>
            <h1>$title</h1>
EOT;

$html = file_get_contents($md);
$Parsedown = new Parsedown();
echo $Parsedown->text($html);

$files = glob($dir.'/*.'.$ext);
$file = array_rand($files);
$img = $files[$file];

$exif = exif_read_data($img, 0, true);
$caption = $exif['COMMENT']['0'];

echo <<< EOT
            <img style="border-radius: 9px;"; src="$img" />
            <p style="">$caption</p>
            <input type="button" value="Reload" onClick="window.location.reload()">
EOT;
?>
```

Despite its simplicity, the script has several configurable parameters that give you some degree of control. You can specify the desired title by editing the `$title` variable, while the `$dir` variable lets you point the script to the source directory containing photos. If you don’t like the default Lato font, you can use the `$font` variable to specify any other font available through [Google Fonts](https://fonts.google.com/). The `$md` variable points to a Markdown-formatted file that is included in the resulting page as an introductory text, while the `$ext` variable lets you specify the file extension of the photos. The latter can come in handy when the source directory contains other files besides photos.

The script and all the required components are available in the [Boketto](https://gitlab.com/dmpop/boketto) GitLab repository. You can either clone it using the `git clone https://gitlab.com/dmpop/hanabi.git` command or downloading the source code as a ZIP package. Replace the *favicon.png* file, add an *.md* file if desired, and change the default values in the *index.php* file. Upload then the *index.php*, *parsedown.php*, *favicon.png*, and the *.md* files to the desired location in the document root of your web server.

Next, create a directory on the server for storing photos. Before you add photos to this directory, it’s a good idea to reduce their size. This will make your app run faster and reduce the amount of data that needs to be transferred. You can use the [jpeg-recompress](https://github.com/danielgtaylor/jpeg-archive) and mogrify tools to do this. With these two tools installed on your system, use the following command to recompress or resize all *.jpg* files in the current directory:

```
for file in *.jpg; do jpeg-recompress --quality high $file $file; done
mogrify -resize "1600>" *.jpg
```

While this simple solution won’t replace a proper gallery or portfolio, it can come in handy when you want to set up a no-frills page featuring your photos. Better still, you can easily put the script to other uses. For example, if you already have a website, you can embed the script into pages to display random photos.

```
<?php
$dir = "path/to/dir";
$ext = "jpg";

$files = glob($dir.'/*.'.$ext);
$file = array_rand($files);
$img = $files[$file];

$exif = exif_read_data($img, 0, true);
$caption = $exif['COMMENT']['0'];

echo <<< EOT
            <img src="$img" />
            <p>$caption</p>
EOT;
?>
```

Insert the code above in a page where you want the image to appear, and make sure that the page itself has the *.php* file extension. That’s all there is to it.

# Show your photos in a new browser tab

The new tab area in your browser can be put to a variety of practical uses: from displaying time zone to taking notes and managing daily tasks. It’s also possible to configure the new tab to showcase your photos. To do this, you need three things: 1) a folder with photos on a web server, 2) a simple PHP script, 3) the New Tab Override extension for Firefox or the Change New Tab extension for Chrome and Chromium.

Before you upload the desired photos to a folder on your web server, it’s a good idea to resize them to make them load quickly. If you have ImageMagick installed on your system, switch to the local directory containing the photos and run the command below (if needed, adjust the file extension, resize, and quality values):

```
for file in *.jpg; do mogrify -resize "1200>" -quality 95% $file; done
```

Keep in mind that this command replaces the original images with the processed ones. If you don’t want that, use the following command which saves the resized images with the *.JPG* file extension:

```
for file in *.jpg; do convert -resize "1200>" -quality 95% $file "`basename $file .jpg`.JPG"; done
```

Upload the resized images to a folder on the web server. Fetch then the PHP script using the `wget -O newtab.php https://gitlab.com/snippets/1832587/raw` command. Open the downloaded *netab.php* file for editing, and make sure that the value of the `$ext` variable matches the file extension of the photos. Move the script to the folder on the web server containing the resized photos.

Install the [New Tab Override](https://addons.mozilla.org/firefox/addon/new-tab-override/) extension, open the extension’s preferences page and specify the URL of the PHP script in the corresponding field. If you happen to use Chrome or Chromium, install the [Change New Tab](https://chrome.google.com/webstore/detail/change-new-tab/mocklpfdimiadpbgamlgehpgpodggahe/) extension, and specify the URL when prompted.

When you’re done, open a new tab, and you should see a random photo.

# WIRC: Wi-Fi infrared remote control for Sony Alpha cameras

The IR port is probably not the most exciting feature of a Sony Alpha camera. In fact, you’ll be forgiven for wondering why Sony keeps this seemingly obsolete piece of technology around. Because it’s cheap, simple and reliable. It’s also surprisingly versatile, as it allows you to control practically every physical button of your camera. Unfortunately, the inexpensive IR remote controls you find on the web don’t do the IR port any justice. Most of them allow you to trigger the camera’s shutter, trigger a timer, lock it in the bulb mode. Some advanced models also feature intervalometers, but that’s about it.

![](media/file31.jpg)

So if you want to unleash the true potential of the IR port, you should go the DIY route. It’s both educational and fun. And it’s probably cheaper too. Not to mention that the final result beats any commercially available IR remote control. The DIY IR remote control described below features its own web-based interface and it can be controlled via a wireless connection using any device with a web browser. This may seem like a bad case of over-engineering, but this solution does have some redeeming qualities:

*   It doesn’t require any proprietary apps installed on your camera or mobile device
*   You can use any device with a browser to control the camera
*   It is possible to adapt the IR remote control for use with camera models from other manufacturers

To build the IR remote control, you need the following components:

*   ESP8266 NodeMCU board or Wemos D1 mini
*   Breadboard
*   1x 150Ohm resistor
*   IR LED (940nm)
*   Wires

While you can use practically any ESP8266-based board, a Wemos D1 mini module makes an ideal candidate for the project thanks to its diminutive size. You also need a regular Linux machine to write and compile code and upload it to the board.

The first order of business is to install the required tools on your Linux machine and connect the board to it. While you can use the popular Arduino IDE to work with code and push it to the board, [Arduino CLI](https://github.com/arduino/arduino-cli) is a perfectly adequate command-line tool for this project. Grab the latest release for your platform from the project’s GitHub page, and extract the downloaded archive. In the terminal, switch to the resulting directory and install the executable binary using the following commands:

```
[](#cb105-1)sudo cp arduino-cli* /usr/local/bin/arduino-cli
[](#cb105-2)sudo chown root:root /usr/local/bin/arduino-cli
[](#cb105-3)sudo chmod 755 /usr/local/bin/arduino-cli
```

Next, connect the board to the machine, and run the `sudo chmod 666 /dev/ttyUSB0` command to enable access to it. To make the access permanent, use the following command:

```
sudo usermod -a -G dialout $USER
```

To detect the connected board, run the `arduino-cli board list` command. If the board has been detected, you should see the following output.

```
FQBN    Port            ID              Board Name 
        /dev/ttyUSB0    1a86:7523       unknown 
```

Disconnect the board and wire all the components as shown on the diagram below.

![](media/file32.png)

Now clone the [WIRC](https://gitlab.com/dmpop/wirc) project that contains the code using the `git clone git@gitlab.com:dmpop/wirc.git` command. Alternatively, download the latest archive from the project’s GitLab page. In the terminal, switch to the resulting directory and run the following command to compile the code:

```
arduino-cli compile --fqbn esp8266:esp8266:d1
```

This creates two files in the directory: *wirc.esp8266.esp8266.d1.elf* and *wirc.esp8266.esp8266.d1.bin*. To install and upload the compiled code to the board, connect the board to the machine and run the following command:

```
arduino-cli upload -p /dev/ttyUSB0 --fqbn esp8266:esp8266:d1
```

As soon as the code has been uploaded to the board, the device becomes operational. The final step is to connect the created Wi-Fi IR remote control to an existing Wi-Fi network. To do this, connect either your Linux machine or a mobile device to the access point created by the board. This automatically redirects to the captive portal that allows you to connect the board to an existing wireless network. Once you’ve done this, make sure that the device you want to use to operate the remote control is connected to the same wireless network as the board. Point then the browser on your device to the IP address of the remote control, and you should see its web interface.

On your Sony Alpha camera, enable the remote control feature. To do this on Sony α6300 (ILCE-6300), press the **MENU** button, go to **Settings → 3 → Remote Ctrl**, and choose *On*. Make sure that there is a line of sight between the remote control and the camera’s IR port, and press the **SHUTTER** button in the web interface. If everything works, this should trigger the camera’s shutter.

# Control Sony Alpha camera from Linux with Sony Camera Remote API

Controlling a digital camera from a Linux machine via a USB connection is nothing new, and applications like gPhoto, Entangle, and Darktable allow you to do this with consummate ease. But tethered shooting is both old-fashioned and somewhat impractical, as it requires a physical connection between the machine and the camera. Conveniently, the latest camera models support remote control via Wi-Fi, which offers a more flexible way of remote shooting. In most cases, though, you use a dedicated app on an Android or iOS device to take advantage of this functionality. Fortunately, some manufacturers like Sony support a camera remote API that can be used to build third-party applications and tools for remote control via Wi-Fi on practically any platform.

In the case of Sony Alpha models, the Smart Remote Control app transforms the camera into an ad-hoc wireless hotspot and a server that accepts and parses incoming HTTP calls with payloads in the JSON format. These payloads contain instructions for controlling the camera and its settings. In practical terms this means that you can control the Sony camera from any device via a direct wireless connection by sending HTTP calls containing JSON-formatted data. The technical term for this technology is [JSON-RPC over HTTP](https://en.wikipedia.org/wiki/JSON-RPC), and it’s supported by many popular scripting and programming languages.

On Linux, you only need the Bash shell script and the [cURL](https://curl.haxx.se/) tool to build simple and more advanced scripts for controlling your Sony Alpha camera remotely. But before you proceed, make sure that your specific camera model is supported by consulting the [camera compatibility](https://developer.sony.com/develop/cameras/) page.

## Preparatory work

The first step is to establish a direct wireless connection between your Linux machine and the camera. On the camera, press the **Menu** button, switch to the **Application List** section, and start the Smart Remote Control app. Switch to the **Connect with password** page, and use the provided connection info to connect the Linux machine to the camera’s hotspot. To communicate and control the camera, you need to know its endpoint URL, or URL to send JSON-RPC HTTP requests to. Usually, the endpoint URL of Sony cameras is *http://192.168.122.1:8080/sony/camera*. However, it may happen that your particular camera model uses a different endpoint URL. To find it, you can use a quick-and-dirty Python script:

```
[](#cb110-1)#!/usr/bin/env python
[](#cb110-2)import sys
[](#cb110-3)import socket
[](#cb110-4)import re
[](#cb110-5)import urllib2
[](#cb110-6)SSDP_ADDR = "239.255.255.250";
[](#cb110-7)SSDP_PORT = 1900;
[](#cb110-8)SSDP_MX = 1;
[](#cb110-9)SSDP_ST = "urn:schemas-sony-com:service:ScalarWebAPI:1";
[](#cb110-10)ssdpRequest = "M-SEARCH * HTTP/1.1\r\n" + \
[](#cb110-11)                "HOST: %s:%d\r\n" % (SSDP_ADDR, SSDP_PORT) + \
[](#cb110-12)                "MAN: \"ssdp:discover\"\r\n" + \
[](#cb110-13)                "MX: %d\r\n" % (SSDP_MX, ) + \
[](#cb110-14)                "ST: %s\r\n" % (SSDP_ST, ) + "\r\n";
[](#cb110-15)sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
[](#cb110-16)sock.sendto(ssdpRequest, (SSDP_ADDR, SSDP_PORT))
[](#cb110-17)RESULT = sock.recv(1000)
[](#cb110-18)URL=re.search("(?P<url>https?://[^\s]+)", RESULT).group("url")
[](#cb110-19)RESPONSE = urllib2.urlopen(URL)
[](#cb110-20)CONTENT = response.read()
[](#cb110-21)RESULT=str(re.findall("ScalarWebAPI_ActionList_URL.*$",CONTENT,re.MULTILINE))
[](#cb110-22)print (Endpoint URL:" + re.search("(?P<url>https?://[^\s]+)", RESULT).group("url").split("<", 1)[0] + "/camera")
```

Save the script under the *ssdp.py* name, make it executable using the `chmod +x ssdp.py` command, and run the script in the terminal to obtain the correct endpoint URL.

Grab the latest version of the [Sony Camera Remote API SDK](https://developer.sony.com/downloads/all/sony-camera-remote-api-beta-sdk/), and you are ready to get started.

## First Shell Script

A simple shell script that takes a single photo is a good starting point for mastering the Camera Remote API. Taking a photo remotely is a three-step action: put the camera into the recording mode, take photo, end the recording mode. Each step is accomplished by sending a JSON-PRC HTTP call. To enable the recording mode, you need to send an HTTP call with the following JSON-PRC payload:

```
{
  "method":"startRecMode",
  "params":[],
  "id":1,
  "version": "1.0"
}
```

When it comes to transferring data to and from a server via the HTTP protocol, cURL is the perfect tool for the job, and the command that puts the camera into the recording mode is as follows:

```
curl -s -X POST -d '{"method":"startRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
```

The `-s`flag mutes cURL, while the `-X POST -d` flags specify a custom request method that sends specified data via the HTTP POST request to the endpoint URL. Normally, the HTTP request triggers a response from the server, but since there is no need for it, the output is sent to */dev/null* and discarded. To switch to the recording mode, the camera needs a little bit of time, so you should add the `sleep 2` command right after the JSON-PRC request.

The commands that take a photo and stop the recording mode look very similar:

```
curl -s -X POST -d '{"method":"actTakePicture","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"stopRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
```

The only difference here is the actual *method* values. To turn individual commands into a script, create a text file and paste the following code into it:

```
#!/usr/bin/env bash
curl -s -X POST -d '{"method":"startRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
sleep 2
curl -s -X POST -d '{"method":"actTakePicture","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"stopRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
```

Save the file under the *take-photo.sh* name and make the script executable using the `chmod +x take-photo.sh` command. Make sure that your Linux machine is connected to the camera, then run the script with the `./take-photo.sh` command. If everything works properly, the camera should take a single photo.

The Camera Remote API also makes it possible to control practically all camera settings: from aperture and shutter speed, to white balance and shooting mode. All you need to do is to send a JSON-PRC HTTP request with `method` and `params` containing the appropriate values. For example, the command below sets the aperture value to 11:

```
curl -s -X POST -d '{"method":"setFNumber","params":["11"],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
```

To specify the desired aperture value on the fly, use the `read -p` command:

```
read -p "Specify F number: " fnumber
curl -s -X POST -d '{"method":"setFNumber","params":["'"$fnumber"'"],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
```

## Add GUI with YAD

To make the remote camera control script more comfortable in use, you might want to wrap it up into a graphical interface. While you can use [Zenity](https://help.gnome.org/users/zenity/stable/) or [Kdialog](https://techbase.kde.org/Development/Tutorials/Shell_Scripting_with_KDE_Dialogs) to create simple dialogs, [YAD](https://sourceforge.net/projects/yad-dialog/) is a much better tool for the job, as it allows you to build complex dialogs containing multiple fields and widgets. The following command, for example, generates a dialog window with three text input fields for specifying the aperture, shutter speed, and ISO values:

```
yad --width=400 --title="Sony Camera Remote" --form --separator="," --field="Shutter Speed" --field="ISO"
```

Here is the complete listing of the Bash shell script that checks the connection to the camera, displays a dialog window, processes the collected input, changes camera settings, and takes a photo:

```
#!/usr/bin/env bash
if [ -z "$(which yad)" ]; then
  echo "Please install YAD. To do this on Ubuntu, run the following command:"
  echo "sudo apt install yad"
  exit 1
fi
ping -W 1 -c 2 192.168.122.1 > /dev/null
if test $? -eq 1
then
    echo "Camera is not connected!" | yad --text-info
    exit 1
fi
result=$(yad --width=400 --title="Sony Camera Remote" --form --separator="," --field="Aperture" --field="Shutter Speed" --field="ISO")
exposuremode=$(echo "$result" | cut -d',' -f1)
fnumber=$(echo "$result" | cut -d',' -f2)
shutterspeed=$(echo "$result" | cut -d',' -f3)
iso=$(echo "$result" | cut -d',' -f4)
if [ -z $result ]; then
  exit 1
fi
curl -s -X POST -d '{"method":"startRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
sleep 5
curl -s -X POST -d '{"method":"setExposureMode","params":["$exposuremode"],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"setFNumber","params":["$fnumber"],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"setShutterSpeed","params":["$shutterspeed"],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"setIsoSpeedRate","params":["$iso"],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"actTakePicture","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
curl -s -X POST -d '{"method":"stopRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
echo "All done!" | yad --text-info
```

The ability to control the camera and trigger the shutter remotely as well as program the camera operations opens a whole new world of possibilities. For example, you can create a relatively simple Bash shell script for time-lapse photography:

```
#!/usr/bin/env bash
if [ $# -eq 0 ]
then
    echo "Error: missing arguments"
    echo "Syntax: [interval(seconds)] [number of Photos]"
    exit 1
fi
interval=$1
n=$2
ping -W 1 -c 2 192.168.122.1 > /dev/null
if test $? -eq 1
then
    echo "Error: camera is not connected!"
    exit
fi
begin(){
    curl -s -X POST -d '{"method":"startRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
    resposta=$?
    if test $resposta -ne 0
    then
        echo "Connection failed."
        curl -X POST -d '{"method":"stopRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
    else
        echo -e "\nConnection stablished."
    fi
}
end(){
    curl -s -X POST -d '{"method":"stopRecMode","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
}
takePhoto(){
    echo -e "Taking photo... \c"
    curl -s -X POST -d '{"method":"actTakePicture","params":[],"id":1,"version": "1.0"}' http://192.168.122.1:8080/sony/camera > /dev/null
    echo "Done."
}
begin
sleep 3;
time=`date +%s`
time=`expr $time + $interval \* $n + 10`
echo ""
echo "The timelapse will end at "`date --date=@$time +%H:%M:%S`""
echo ""
for (( i = 0; i < $n; i++ ))
do
    takePhoto
    sleep $interval
done
end
```

## Brief note on using Python

If you prefer to use Python instead of the Bash shell to control the camera, you’ll be pleased to learn that the *requests* Python module makes it supremely easy to send JSON-RPC HTTP calls. The easiest way to install the module is through the PIP package manager. On Ubuntu, this can be done using the following commands:

```
sudo apt install python-pip
sudo pip install requests
```

And here is an example Python script that takes a single photo:

```
[](#cb121-1)#!/usr/bin/env python
[](#cb121-2)import requests
[](#cb121-3)import time
[](#cb121-4)requests.post('http://192.168.122.1:8080/sony/camera', json={"method":"startRecMode","params":[],"id":1,"version": "1.0"})
[](#cb121-5)time.sleep(2)
[](#cb121-6)requests.post('http://192.168.122.1:8080/sony/camera', json={"method":"actTakePicture","params":[],"id":1,"version": "1.0"})
[](#cb121-7)requests.post('http://192.168.122.1:8080/sony/camera', json={"method":"stopRecMode","params":[],"id":1,"version": "1.0"})
```

# Extend Sony Alpha camera functionality with Sony-PMCA-RE

Updating firmware and installing additional apps on a Sony Alpha camera usually requires going through the Sony PlayMemories desktop software. In addition to being rather cumbersome in use, it only runs on Windows and macOS X. [Sony-PMCA-RE](https://github.com/ma1co/Sony-PMCA-RE) provides a nimble alternative that runs on Linux (as well as on Windows and mac OS X) and allows you to sideload apps, bypassing the official [PlayMemories](https://www.playmemoriescameraapps.com/) service. Although, the project doesn’t provide ready-to-use binaries for Linux, deploying Sony-PMCA-RE on a Linux system is not particularly difficult. You need to install the required packages, clone the project’s Git repository, create a Python virtual environment, and install the required Python packages. To do this on openSUSE, run the following commands:

```
sudo zypper in python3 python3-virtualenv python3-pip
git clone https://github.com/ma1co/Sony-PMCA-RE.git
cd Sony-PMCA-RE
python3 -m venv .env
source .env/bin/activate
pip install -r requirements.txt
```

Connect then your camera and turn it on. Run the `./pmca-gui.py` command to launch a graphical version of the tool. In the **Camera Info** section, press **Get camera info**. If the camera has been recognized, you should see basic info about the camera, including model, serial number, and firmware version.

![](media/file33.jpg)

Installing apps on the camera using the graphical tool is rather straightforward. Switch to the **Install app** section, select the desired app from the drop-down list of all available apps, and press **Install selected app**. Once the app has been installed, you’ll find it under the **Application List** section of your camera. You can uninstall any sideloaded app in a regular manner in the **App Management** section.

# Using FTP feature in Sony α7 Mark III

The FTP transfer feature in Sony α7 Mark III (and other newer Alpha models) doesn’t usually get a lot of attention. Sure, with all the modern technologies and apps, it’s easy to overlook this humble feature. But when it comes to transferring RAW and JPEG files, FTP can really hold its own. In fact, it has several important advantages.

*   FTP is a mature, reliable, and well-supported technology.
*   You can use FTP to transfer photos to a local machine as well as a remote server. And since Sony α7 Mark III supports multiple FTP profiles, you can transfer photos to multiple destinations.
*   FTP servers are available for practically any platform, including macOS, Linux, and Windows. There are also plenty of open-source FTP servers available free of charge.
*   The FTP transfer feature in Sony α7 Mark III supports transfer of both RAW and JPEG files.

## Installing FTP on Raspberry Pi

If you have a Raspberry Pi lying around, you can easily transform it into a dedicated FTP server for use with your camera. First, install the *vsftpd* server using the `sudo apt install vsftpd` command.

Run then the `sudo nano /etc/vsftpd.conf` command to open the *vsftpd.conf* file in the *nano* editor. Edit the configuration, so it includes the following parameters:

```
anonymous_enable=NO
local_enable=YES
write_enable=YES
```

This configuration disables anonymous access to the server, and gives the existing user access and upload rights. Save the changes, and restart the server using the `sudo service vsftpd restart` command.

## Configure FTP settings

Before you proceed, have the following connection info ready:

*   IP address or domain name of the FTP server
*   User name and password

In case the FTP server runs on the Raspberry Pi, use the `hostname -I | cut -d' ' -f1` command to obtain its IP address. The user name and the password required for logging into the FTP server are the same as the user account on the Raspberry Pi.

In your camera, press the **Menu** button and go to **Network → Network1 → [FTP Transfer Func.] → FTP Server 1**. Choose **Display Name** and give the profile a short descriptive name. Go one step back, and switch to the **Destination Settings** section. Configure the following settings: - **Host Name** The host name or IP address of the FTP server. - **Secure Protocol** Enable secure FTP transfers. Leave it disabled. - **Port** The port number of the FTP server. If the FTP server runs on the default port 21, skip this field. - **Directory** Set the destination folder on the FTP server. If you leave this field empty, RAW and JPEG files will be uploaded to a separate folder in the user home directory. The current date is used as the name of the upload folder.

Press **OK** to save the connection settings, switch to the **User Settings Info** screen, and enter the user name and the password in the appropriate fields. Press **OK**, and quit the menu mode.

To upload photos from the camera to the configured FTP server, switch to the viewing mode, press the **Menu** button and go to **Network → Network1 → FTP Transfer**. Once the camera has established a connection to the FTP server, select the photos you want to upload, press the **Menu** button, and choose **OK**.

# Add useful info to EXIF metadata

Unlike other fields in EXIF metadata, the *Comment* field is not reserved for any specific type of data, and it’s usually left for the user to decide what to put in there. A Bash shell script can automatically populate the *Comment* field with several pieces of useful and interesting information, including camera model, and lens, and weather conditions of the current date. And using a dedicated Dolphin action, you can view this info with a single mouse click.

Before you proceed, you need to sign up for [OpenWeatheMap API](https://openweathermap.org/api) and create a unique API key. You’ll need it to fetch weather data. Also, install the required packages on your system. To do this on openSUSE, use the `sudo zypper in exiftool jq kdialog` command. On Debian and Ubuntu, run the `sudo apt install libimage-exiftool-perl jq kdialog` command.

Next, open a text editor and paste the following code into a new text file:

```
#!/usr/bin/env bash

if [ -z "$1" ]; then
    echo "ERROR: Required parameter is missing."
    echo "Please specify file extension, e.g., $0 jpeg"
    exit 1
fi

CONFIG="$HOME/addinfo.cfg"

if [ ! -f "$CONFIG" ]; then
    api_key=$(kdialog --title "API" --inputbox "Enter your API key:")
    echo 'api_key="'$api_key'"' >> "$CONFIG"
    echo 'json="$HOME/weather.json"' >> "$CONFIG"
fi
source "$CONFIG"
check=$(wget -q --spider https://api.openweathermap.org)
if [ -z $check ]; then
    for photo in *."$1";
    do
    lat=$(exiftool "$photo" -gpslatitude -n | cut -d":" -f2 | tr -d " ")
    lon=$(exiftool "$photo" -gpslongitude -n | cut -d":" -f2 | tr -d " ")
    if [ ! -z "$lat" ] && [ ! -z "$lon" ]; then
            camera=$(exiftool -Model "$photo" | cut -d":" -f2 | tr -d " ")
            lens=$(exiftool -LensID "$photo" | cut -d":" -f2)
            curl "https://api.openweathermap.org/data/2.5/weather?lat="$lat"&lon="$lon"&appid="$api_key"&units=metric&cnt=7&lang=en&units=metric&cnt=7&lang=en" > $json
            w_sum=$(jq '.weather | .[0] | .main' $json | tr -d '"')
            w_temp=$(jq '.main | .temp' $json | tr -d '"')
            w_wind=$(jq '.wind | .speed' $json | tr -d '"')
            exiftool -overwrite_original -copyright="$copyright" -comment="$camera $lens "$w_temp"°C "$w_wind"m/s "$w_sum" "$1"
    else
        echo "$photo is not geotagged"
    fi
    done
    if [ -d "$json" ]; then
        rm "$json"
    fi
    kdialog --title "All done" --passivepopup "All done. Bye!" 10
else
    kdialog --title "Error" --passivepopup "API is not reachable." 10
    exit 1
fi
```

Save the script under the *add-exif-comment* name and move it to the */usr/local/bin/* directory. Set the correct owner and permissions for the script:

```
sudo chown root:root /usr/local/bin/add-exif-comment
sudo chmod 755 /usr/local/bin/add-exif-comment
```

Here’s how the script works. When you run the `add-exif-comment [EXTENSION]` command (e.g., `add-exif-comment JPG`) for the first time, it prompts you to specify your OpenWeatherMap API token and save it in a configuration file. The script then finds all JPG files in the current directory. To obtain the weather data, the script extracts the geographical coordinates from the photo’s EXIF metadata. This means that the script can only work with geotagged photos. If no latitude and longitude values were found in the currently processed file, the script displays an error message and skips the photo. ExifTool also pulls the camera model and lens values from the appropriate fields of EXIF metadata. The *curl* tool then fetches the weather data in the JSON format, and the *jq* utility extracts the temperature and weather summary information.

An image viewer like Gwenview allows you to view EXIF metadata, including the *Comment* field. And if you happen to use Dolphin as your default file manager, you can create a dedicated action for displaying the contents of the *Comment* field in a pop-up box. First, paste the following code into a new text file:

```
#!/usr/bin/env bash
comment=$(exiftool -Comment "@" | cut -d":" -f2 | sed -e 's/^[[:space:]]*//')
kdialog --msgbox "$comment"
```

Save the file under the *show-comment* name, and move it to the */usr/local/bin/* directory. Set the correct owner and permissions for the script:

```
sudo chown root:root /usr/local/bin/show-comment
sudo chmod 755 /usr/local/bin/show-comment
```

Paste the code below into a new text file:

```
[Desktop Entry]
Type=Service
X-KDE-Priority=TopLevel
ServiceTypes=KonqPopupMenu/Plugin
MimeType=image/JPEG;image/jpeg;image/JPG;image/jpg;
Actions=Comment
[Desktop Action Comment]
Name=Show EXIF Comment
Exec=/usr/local/bin/show-comment %F 
```

Save the file under the *show-comment.desktop* name, and move it to the */usr/share/kservices5/ServiceMenus/* directory. Launch Dolphin, right-click on a JPEG file, choose the **Show EXIF Comment* item, and you should see the contents in the *Comment* field in a pop-up box.

# Geotag JPEG files using reference photo

Sometime the easiest way to geotag JPEG files is to use geographical coordinates from an already geotagged photo. One way to do this is to use digiKam. While it’s not particularly difficult, this procedure requires a few separate steps. A can streamline the entire process.

```
[](#cb129-1)#!/usr/bin/env bash
[](#cb129-2)ref="$1"
[](#cb129-3)lat=$(exiftool -gpslatitude -n "$ref" | cut -d":" -f2 | tr -d " ")
[](#cb129-4)lon=$(exiftool -gpslongitude -n "$ref" | cut -d":" -f2 | tr -d " ")
[](#cb129-5)if [ -z "$lat" ] || [ -z "$lon" ]; then
[](#cb129-6)    notify-send "Geographical coordinates are missing."
[](#cb129-7)    exit 1
[](#cb129-8)else
[](#cb129-9)    notify-send $lat $lon
[](#cb129-10)fi
[](#cb129-11)if (( $(echo "$lat > 0" |bc -l) )); then
[](#cb129-12)    latref="N"
[](#cb129-13)else
[](#cb129-14)    latref="S"
[](#cb129-15)fi
[](#cb129-16)if (( $(echo "$lon > 0" |bc -l) )); then
[](#cb129-17)    lonref="E"
[](#cb129-18)else
[](#cb129-19)    lonref="W"
[](#cb129-20)fi
[](#cb129-21)f=$(yad --center --text-align=center --title="Photos to geotag" --button=gtk-cancel:0 \
[](#cb129-22)    --button="Geotag":0 --borders=15 --width=250 --height=150 \
[](#cb129-23)    --text='<big>\nDrop photos you want to geotag  here.\nPress the <b>Geotag</b> button.</big>' \
[](#cb129-24)    --dnd | sed 's/^.......//')
[](#cb129-25)array=("$f")
[](#cb129-26)for file in ${array[*]}
[](#cb129-27)do
[](#cb129-28)    exiftool -overwrite_original -GPSLatitude=$lat -GPSLatitudeRef=$latref -GPSLongitude=$lon -GPSLongitudeRef=$lonref "$file"
[](#cb129-29)done
[](#cb129-30)notify-send "All done. Bye!"
```

Here is how the script works. Using *ExifTool*, it obtains latitude and longitude values from the photo which file name was provided as a command parameter. If it fails to get geographical coordinates (i.e., the `$lat` and `$lon` values are empty), it show a notification and stops. If obtaining geographical coordinates was successful, the script uses the *bc* tool to calculate correct latitude and longitude references required for geotagging. The script then displays a drag-and-drop panel, when you drop photos you want to geotag. When you press the **Geotag** button, the script geotags the selected photos.

To make the described script work, you need to install the *ExifTool*, *bc*, *notify-send*, and *yad* tools on your system. To do this on Ubuntu, run the `sudo apt install libimage-exiftool-perl bc libnotify-bin yad`. On openSUSE, use the `sudo zypper in exiftool bc libnotify-bin yad` command.

Copy the script and paste it in a new text file. Save the file under the *geotagref.sh* name and make it executable using the `chmod +x geotagref.sh` command. Move then the script to the *~/bin* directory. To geotag photos run the script followed by the path and file name of the reference photo: `geotagref.sh /path/to/foo.jpg`

# Take a stroll down memory lane with Natsukashii

Services like Amazon Photos, Facebook, and Google Photos can help you rediscover your photos and relive your memories by showing photos taken on a specific day in the past. But there is no need to upload your photos to third-party services to enjoy this clever feature. [Natsukashii](https://gitlab.com/dmpop/natsukashii), a Bash shell script, can search photos on your machine and generate a simple HTML page with the found photos for your viewing pleasure. It can also send a notification to your Android device through the [Notify](https://github.com/mashlol/notify) app.

Deploying Natsukashii on the Linux machine that has all your photos is easy. First, make sure that you have the ExifTool, Git, sed, and seq tools installed on your system. Next, use the following command to clone the project’s repository, and create an alias, so you can run Natsukashii using the `natsukashii` command:

```
git clone https://gitlab.com/dmpop/natsukashii.git
echo -e "\nalias natsukashii=/share/homes/admin/natsukashii/natsukashii.sh" >> .bashrc
```

If the machine running Natsukashii also acts a web server, you can use Natsukashii to publish the photos it finds. To do this, move the *www* folder to the document root of your web server. You might want to give the *www* folder a different name, for example *natsukashii*.

If you want to receive notifications from Natsukashii on your Android device, install the [Notify](https://github.com/mashlol/notify) app, and note the generated unique token.

Now run the `natsukashii` command, and specify the required settings. After that, Natsukashii goes through the specified directory, and if it finds matching photos, it puts them into a separate directory. If you’ve specified the path to the web directory, Natsukashii moves the found photos there, and you can view them by pointing a browser to the correct URL.

![](media/file34.jpg)

When using Natsukashii, keep in mind that the script is not particularly fast. This is because the script needs to find all photos that match the specified file extension. It then goes through each photo, extracting its date and comparing the date with the given one. And this may take a while, depending on the number of photos you have.

While you can run Natsukashii manually, it makes sense to set up a cron job that executes the script daily. To do this, run the `crontab -e` command and add the following cron job:

```
@daily /absolute/path/to/natsukashii.sh
```

Save the changes, and you are done.

## Install Natsukashii on a QNAP NAS

Since Natsukashii is just a regular shell script that relies on standard Linux tools, it can be deployed on practically any machine running Linux. This includes network-attached storage (NAS) appliances like QNAP. To deploy Natsukashii on a QNAP appliance, install [Entware](https://github.com/Entware/Entware) (see [Install on QNAP NAS](https://github.com/Entware/Entware/wiki/Install-on-QNAP-NAS). Run then the commands below to install the required packages:

```
opkg update
opkg install git git-http screen perl-image-exiftool sed coreutils-seq imagemagick imagemagick-tools imagemagick-jpeg
```

Switch then to the folder in your home directory, and clone the project’s Git repository using the following command:

```
git clone https://gitlab.com/dmpop/natsukashii.git
```

Switch then to the *natsukashii* directory and run the `./natsukashii.sh` command.

Creating a cron job on QNAP is slightly different from the standard procedure. Open the */etc/config/crontab* file in a text editor, and add the following cron job:

```
@daily /bin/sh /absolute/path/to/natsukashii.sh
```

Save the changes and restart the cron service using the `/etc/init.d/crond.sh restart` command.

## Add password protection to Natsukashii

Natsukashii is designed to publish all photos that match the current date, even private ones. If you don’t feel like letting the entire world see all your photos, you might want to protect access to the page generated by Natsukashii with a user name and password. If you are using the Apache web server with the htaccess functionality enabled, you can add password protection using *.htpasswd* and *.htaccess* files.

To generate the *.htpasswd* file, run the following command on your server (replace */path/to/server/doc/root* with the actual path to the document root of the web server, e.g., */var/www* or */var/www/html*. Replace *user* with the desired user name):

```
htpasswd -c /path/to/server/doc/root .htpasswd user
```

When prompted, specify the desired password.

Create a new text file and paste the following code into it:

```
AuthType Basic
AuthName "Natsukashii"
AuthUserFile /path/to/server/doc/root/.htpasswd
require valid-user
```

Save the file under the *.htaccess* name in the directory containing the Natsukashii web page. Now, point the browser to the Natsukasii page. If everything works properly, you should see a dialog prompting you to enter credentials. Entering the specified user name and password should grant you access to the page.

# Command-line photographic workflow on Android with Termux

There are plenty of Android apps for organizing, processing, and sharing photos. But if you want to implement a photographic workflow based on popular Linux tools, then [Termux](http://termux.com) is all you need.

Termux is available on Google Play Store and [F-Droid](http://f-droid.org), so you can install it from your preferred source. The app’s default functionality can be extended by installing add-ons. The Termux:API add-on, for example, adds support for Android API, while the Termux:Styling package lets you pick an alternative color scheme and font. The Termux:Widget add-on gives you a homescreen widget containing shortcuts to shell scripts, so you can run scripts in Termux with a single tap. You can install these add-ons for free from F-Droid. If you choose to install the add-ons from Google Play Store, you have to purchase them. Think of it as a way to donate to the project and support its developer.

Working in the terminal using the on-screen keyboard can quickly become tedious. Fortunately, Termux provides shortcuts to many common keyboard actions. Most of these shortcuts are identical to those in the Bash shell. For example, the **Ctrl+A** and **Ctrl+E** shortcuts move the cursor to the beginning and the end of the line respectively, while the **Ctrl+C** and **Ctrl+D** shortcuts abort the current process and log out of the terminal session. The only difference is that Termux uses the **Volume Down** hardware button instead of the **Ctrl** key. The **Volume Up** button in combination with various letters is used to emulate keyboard keys. The **Volume Up+T** shortcut emulates the **Tab** key, while **Volume Up+W**, **Volume Up+A**, **Volume Up+S**, and **Volume Up+D** act as arrow keys.

There are three things you need to do when running Termux for the first time: update the app’s software repository, install the desired packages, and configure storage access. Termux uses the pkg tool for package management, so if you are coming from Debian or Ubuntu, you should feel at home in Termux. To update the repository, run the `pkg update` command. Want to see all packages in the repository? Run the `pkg list` command. To find a specific package, use the `pkg search [PACKAGE]` command, and to install the package, issue the `pkg install [PACKAGE]` command. Upgrading the installed packages is a matter of running the `pkg upgrade` command, while the `pkg remove [PACKAGE]` command can be used to remove an installed package.

What packages to install depends entirely on what you want to use Termux for, but at the very least you might want to install the nano text editor, the rsync file copying tool, and the OpenSSH SSH connection tool. These three tools allow you to edit text and configuration files and perform backups as well as access and control remote machines. To install these packages in one go, use the following command:

```
pkg install nano rsync openssh git curl wget
```

To configure storage access, run the `termux-setup-storage` command. Doing this grants Termux permission to access shared storage on Android 6.0 and higher as well as creates the dedicated *storage* folder containing symbolic links to various storage locations. This includes *~/storage/shared* (the root folder shared by all apps), *~/storage/dcim* (the standard folder for photos and videos), and *~/storage/downloads* (the default folder for downloaded files).

Having a tooled-up Linux environment on your Android device lets you perform tasks that usually require third-party commercial apps. For example, using rsync, you can easily set up a robust solution for backing up photos and RAW files on your Android device to a remote machine. To do this, it’s a good idea to enable password-less SSH login, so you don’t have to type the password every time you perform backup. Start with running the `ssh-keygen` command. Skip password creation when prompted by pressing **Enter**. Once a key pair has been created, run the `ssh-copy-id -i .ssh/id_rsa.pub user@host` command (replace *user* and *host* with the user name and the remote machine’s IP address or domain name). This copies the public key to the remote machine, thus enabling passwordless login. Backing up data on your Android device to the remote server is a matter of using an appropriate rsync command. If you want to back up photos and videos, the following command will do the trick:

```
rsync -avz -e ssh ~/storage/dcim user@host:/path/to/backup/dir
```

Instead of running this command manually every time you need to perform a backup, you can write a simple Bash shell script, save it in the *~/.shortcuts* directory, and add a Termux widget that links to the script. This way, you can trigger a backup operation directly from the homescreen.

Staying on the subject of photos, the jhead utility makes it possible to process photos stored on your Android device. Run the `pkg install jhead` command to install the utility in Termux. Using jhead, you can replace generic file names with something more meaningful, like timestamps. The following command renames all *.jpg* files using the *YYYYMMDD-hhmmss* rule (e.g., *DC_0001.jpg* becomes *20161010-152557.jpg*):

```
for file in *.jpg; do jhead -n%Y%m%d-%H%M%S $file; done
```

jhead can come in useful for basic EXIF metadata operations, but for more advanced metadata manipulations, you need ExifTool. Since it’s not available in Termux’ software repository, you have to compile and installed ExifTool manually. Start with installing the required packages using the `apt install perl make` command. Use then the wget tool to fetch the latest version of ExifTool source code (replace *Image-ExifTool-xx.xx.tar.gz* with the actual current version):

```
wget http://www.sno.phy.queensu.ca/~phil/exiftool/Image-ExifTool-xx.xx.tar.gz
```

Unpack the downloaded archive and switch to the resulting directory:

```
tar xzvf Image-ExifTool-xx.xx.tar.gz
cd Image-ExifTool-xx.xx
```

Run then the following commands to compile and install ExifTool:

```
perl Makefile.PL
make test
make install
```

Once the compilation and installation process is completed, you can check whether ExifTool has been properly installed by running the `which exiftool` command.

If you happen to shoot in RAW, you can convert RAW files into JPEG photos on your Android device using a combination of DCRaw, Netpbm and ImageMagick. Start with installing these tools by running the `pkg install dcaw, netpbm imagemagick` command. Use then the following command to convert a single RAW file to the PNG format:

```
dcraw -c foo.RAW | pnmtopng > foo.png
```

In this command, the dcraw tool decodes the RAW file and pipes the output to the pnmtopng tool that saves it in the PNG format. You can then use the convert tool to convert the resulting PNG file into JPEG:

```
convert foo.png foo.jpg
```

To process all RAW files and save them in the JPEG format, use these two commands:

```
for file in *.RAW ; do dcraw -c -g 2.4 12.92 "$file" | pnmtopng > "${file%%.*}".png ; done
for file in *.png ; do convert "$file" "${file%.*}.jpg" ; done
```

Instead of convert, you can use the mogrify tool as follows:

```
mogrify -format jpg *.png
```

Keep in mind, though, that mogrify overwrites originals, so use it with care.

Want to apply effects to photos without resorting to a dedicated app? Termux and ImageMagick can handle that too. The latter supports the Hald CLUT technology that makes it possible to use special color lookup tables to perform color transformations. To make use of Hald CLUT, you don’t need to understand all its intricacies, but you need to do some preparatory work. Install ImageMagick on your regular Linux machine, and run the `convert hald:9 hald-9.png` command to generate a Hald CLUT table. Open then the generated `hald-9.png` file in a photo editing application like digiKam, apply the desired color corrections (curves, levels, saturation, brightness, etc.), and save the changes under a descriptive name (e.g., `hald-9-vintage.png`). Now you have a reference Hald CLUT table that can be used as a preset. Using this technique, you can create as many presets as needed. Move them then on your Android device into the folder accessible by Termux. To apply the desired preset to a photo, use the following command:

```
convert foo.JPG hald-9-vintage.png -hald-clut foo-modified.jpeg
```

# Store photos and RAW files on an encrypted external storage device

It’s a good idea to have a backup of your photos and RAW file on an external storage device like a USB hard disk. It’s an even better idea to encrypt the hard disk. This way, no one except you can access the data on the disk.

The first step is to identify the connected external storage device using the `sudo lsblk` command. Take the look at the output, and note the name of the external storage device:

```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:16   0 111.8G  0 disk 
├─sda1   8:17   0     2G  0 part [SWAP]
└─sda2   8:18   0 109.8G  0 part /
sdb      8:32   0 931.5G  0 disk
```

In this case, it’s */dev/sdb*. If the storage device is already partitioned, the output would look something like this:

```
sdb      8:32   0 931.5G  0 disk 
└─sdb1   8:33   0 931.5G  0 part 
```

If necessary, you can remove the existing partition using the fdisk tool. Run the `sudo fdisk /dev/sdb1` command, choose the *d* option, type *1* to select the partition, and press **Enter**. To create a new partition, run the `sudo fdisk /dev/sdb` command, use the *n* option, and press *p* for a primary partition. Press *1* to edit the first partition, then use the defaults for first and last sectors. Finally, press *w* to apply the changes.

Next, install the *cryptsetup* tool. To do this on openSUSE, use the `sudo zypper in cryptsetup` command. To encrypt the partition on the hard disk, run the following command:

```
sudo cryptsetup -v -y -c aes-xts-plain64 -s 512 -h sha512 -i 5000 --use-random luksFormat /dev/sdc1
```

Before you proceed, create a backup of the LUKS header that holds metadata required for the encrypted partition to function:

```
sudo cryptsetup luksHeaderBackup --header-backup-file /path/to/luks-header.img /dev/sdc1
```

Create then a directory in your home for mounting the external hard disk:

```
mkdir ~/external-storage
```

Unlock the encrypted device and create a file system on it:

```
sudo cryptsetup luksOpen /dev/sdc1 ext-hdd
sudo mkfs.ext4 /dev/mapper/ext-hdd
```

From now on, you can mount the device using the following command (replace *user* with your actual user name):

```
sudo mount /dev/mapper/ext-hdd /home/user/external-storage
```

Now, move your photos and RAW files to the mount directory (i.e., *~/external-storage*). When you are done working with the external storage, unmount and lock the device:

```
sudo umount /home/user/external-storage
sudo cryptsetup luksClose /dev/mapper/ext-hdd
```

To speed up the process of unlocking/mounting and locking/unmounting, you can add the following aliases to your *.bashrc* file

```
alias mountext='sudo cryptsetup luksOpen /dev/sdc1 ext-hdd && sudo mount /dev/mapper/ext-hdd /home/user/external-storage'
alias umountext='sudo umount /home/user/external-storage && sudo cryptsetup luksClose /dev/mapper/ext-hdd' 
```

# olympus-photosync: wireless bridge between Olympus cameras and Linux

Although modern Olympus cameras are not particularly hacker-friendly, enterprising and determined coders still manage to extend the existing functionality beyond its intended use. Case in point: [olympus-photosync](https://github.com/mauriciojost/olympus-photosync), a handy little tool that makes it possible to wirelessly transfer JPEG and RAW files from a supported Olympus camera to a Linux machine (or Windows and macOS X for that matter). The tool makes use of the camera’s Wi-Fi capabilities, and you don’t have to hack or tweak the camera for it to work with olympus-photosync. The list of Olympus cameras that are known to work with the tool is rather short, but if you have a recent Wi-Fi-enabled Olympus camera model, chances are it will work just fine with olympus-photosync.

There is no need to compile anything in order to deploy olympus-photosync on a Linux machine. Just download the latest DEB or RPM package from the project’s repository and install it using your system’s package manager. To install olympus-photosync on openSUSE, grab the latest *.noarch.rpm* package, then run the `sudo zypper in photosync-x.x-x.noarch.rpm` command. Alternatively, you can download the *.tgz* or *.zip* archive and unpack it in the desired location.

Next, turn your camera on, press the **Menu** button, and switch to the **Setup Menu → Wi-Fi Settings** section. Make sure that **Wi-Fi Connect Settings** is set to *Private*, and enable Wi-Fi.

![](media/file35.jpg)

On your Linux machine, connect to the camera’s wireless network, open the terminal, and run the `olympus-photosync` command. This should automatically detect the camera and transfer all JPEG and RAW files to the default *~/output* directory. Despite being a one-trick pony, olympus-photosync supports several options that allow you to control its behavior. The `--output-directory` (`-o`) parameter can be used to specify an alternative directory for saving the transferred file. The `--until <DD-MM-YYYY>` option lets you transfer files that are created before the specified date, while the `--from <DD-MM-YYYY>` option limits the transfer to files created after the given date.

Although olympus-photosync is straightforward in use, transferring files wirelessly is not exactly fast. So you would probably want to use the tool to offload the occasional file or two, and not as a replacement for a dedicated (or built-in) card reader.

# Turn Raspberry Pi into a wireless camera server

Controlling your camera from a regular Linux machine over a USB connection can be useful in many situations. But having your camera physically attached to the machine limits the practicality of this otherwise clever solution. Raspberry Pi to the rescue. Deploy a USB server on the tiny machine, plug your camera into it, and you can access and control the latter from any Linux machine via a wireless network.

While it’s possible to use the USB/IP open source software for this project, [VirtualHere](https://www.virtualhere.com/) USB server and client tools provide a less cumbersome and more flexible solution. VirtualHere software is easy to deploy, it requires no configuration, and the client tool is available for all mainstream platforms. The latter means that you can access and control your camera not only from Linux but also Windows and macOS.

Although VirtualHere USB server and client are commercial closed-source products, you can download and use them for free. The only limitation is that you cannot share more than one USB device at a time. Since you are not going to share anything besides your camera, this is not an issue.

The first order of business is to install the VirtualHere USB server on the Raspberry Pi. Open the terminal on the Raspberry Pi, or connect to it via SSH, and run the following commands:

```
sudo apt-get update
wget https://www.virtualhere.com/sites/default/files/usbserver/vhusbdarm
sudo chmod +x ./vhusbdarm
sudo mv vhusbdarm /usr/sbin
wget http://www.virtualhere.com/sites/default/files/usbserver/scripts/vhusbdpin
sudo chmod +x ./vhusbdpin
sudo mv vhusbdpin /etc/init.d
sudo update-rc.d vhusbdpin defaults
sudo reboot
```

Download a VirtualHere client binary from [virtualhere.com/usb_client_software](https://www.virtualhere.com/usb_client_software) to your Linux machine and use the `chmod +x vhuitXX` command (replace *vhuitXX* with the actual name of the downloaded file) to make the file executable. To work with the camera, install the gPhoto tool. To do this on openSUSE, run the `sudo zypper in gphoto` command. On Debian and Ubuntu, use the `sudo apt install gphoto2` command.

Connect the camera to the Raspberry Pi, and power the camera. On your Linux machine, launch the VirtualHere client by running the `sudo ./vhuitXX` command. If everything work properly, you should see the camera listed under **Raspberry Pi Hub**. Double-click on the camera item, to enable it.

![](media/file36.png)

Run then the `gphoto2 --auto-detect` command, and see the output listing your camera, for example:

```
Model                          Port
----------------------------------------------------------
Sony Alpha-A6000 (Control)     usb:002,008
```

At this point, you can control the camera as if it was connected directly to your Linux machine.

# Draw inspiration from Unsplash with the Unbash script

[Unsplash](https://unsplash.com/), with its vast collection of high-quality photos released under the CC0 license, is the perfect place for getting your daily dose of inspiration for any topic imaginable. But instead of wading aimlessly through thousands of photos, you can let the Unbash script fetch photos matching your specific interest and compile them into a simple slideshow:

```
#!/usr/bin/env bash

# User-defined parameters
undir="$HOME/unbash"
default_keyword="monkey"
keyword_list="$HOME/keywords.txt"
default_count="9"

# Check whether the required packages are installed
if [ ! -x "$(command -v wget)" ] || [ ! -x "$(command -v convert)" ] || [ ! -x "$(command -v xdpyinfo)" ]; then
    echo "Install xdpyinfo, wget, and ImageMagick."
    exit 1
fi

# Usage prompt
usage(){
cat <<EOF
$0 [OPTIONS]

$0 downloads a specified number of random photos matching a given keyword from Unsplash and generates an animated GIF

Usage:
  $0 -c <number> -k <keyword>

Options:
  -c --count       Specifies a number of photos to download
  -k --keyword     Specifies the desired keyword
EOF
  exit 1
}

# Specify options
OPTS=`getopt -o c:k: -l count:keyword: -- "$@"`
[[ $# -eq 0 ]] && usage
eval set -- "$OPTS"

# Obtain values
while true; do
  case "$1" in
    -c | --count ) count="$2"; shift 2;;
    -k | --keyword ) keyword="$2"; shift 2;;
    -- ) shift; break ;;
    * ) break ;;
  esac
done

# Check internet connection
wget -q --spider http://source.unsplash.com/
if [ $? -ne 0 ]; then
    echo "Unsplash is not reachable. Check your Internet connection."
    exit 1
fi

# If no keyword specified, check whether the keyword_list file exists
# and pick a random word from the file.
# If the keyword_list file doesn't exist, use the default keyword
if [ -z "$keyword" ]; then
    if [ ! -f "$keyword_list" ]; then
    keyword=$default_keyword
    else
    keyword=$(shuf -n 1 "$keyword_list")
    fi
fi

# If the count value is empty, use the default count
if [ -z "$count" ]; then
    count=$default_count
fi

# Check whether the unspiration directory exists
# Remove and create if the directory already exists
# Create it if the directory doesn't exist
# Switch to the created directory
if [ -d "$undir" ]; then
    rm -rf "$undir"
    mkdir "$undir"
    cd "$undir"
else
    mkdir "$undir"
    cd "$undir"
fi

# Determine screen resolution to fetch photos in the correct size
size=$(xdpyinfo | grep dimensions | awk '{print $2}')

# Fetch the specified number of random photos matching the given keyword from Unsplash
# Sleep interval is necessary for Unsplash randomizer
i=1
while [ $i -le "$count" ]
do
    wget https://source.unsplash.com/$size/?"$keyword" -O $i-"$keyword".jpg
    i=$((i + 1))
    sleep 3
done

# Generate an animated GIF using the fetched photos
convert -delay 300 -loop 0 *.jpg "$keyword"-inspiration.gif

# Open the animated GIF in the default image viewer
xdg-open "$keyword"-inspiration.gif
```

This script performs a number of tasks and offers a certain degree of customization. First, it checks whether the required packages are installed. The script requires two parameters: the number of photos to fetch (the *-c* or *–count* parameter) and the keyword (*-k* or *–keyword*). And a dedicated code block defines these parameters and obtains the provided values. Before the script proceeds, it checks whether there is an internet connection. If the keyword value is missing, the script checks whether a text file containing keywords exists. If the file exists, the script picks a random word and uses it as the script’s parameter. If the file doesn’t exist, the script uses the default keyword. The same applies to the count parameter: if it’s missing, the script uses the default count value. Next, the script creates a dedicated directory for storing all working files and uses the xdpyinfo tool to determine the screen resolution in order to fetch photos of the appropriate dimensions. Once the script has done that, it downloads a specified number of random photos that match the given keyword from Unsplash using the wget tool. The downloaded photos are combined into an animated GIF file which is then opened in the default image viewer.

To deploy the script, paste it into a text file and save it under the *unbash* name. Use the following commands to move the script and make it executable:

```
sudo mv unbash /local/bin/unbash
sudo chown root:root /local/bin/unbash
sudo sudo chmod 755 /local/bin/unbash
```

You can then launch the script by running the `unbash -c COUNT -k KEYWORD` command (replace *COUNT* and *KEYWORD* with the desired number of photos and keyword). Alternatively, create the *keywords.txt* file containing a list of desired keywords in your home directory, and run the `unbash -c COUNT` command.

# Generate super-resolution photos with the Highrise script

Some camera models with sensor-shift image stabilization can use this feature to create super-resolution images by taking multiple photos and assembling them into a single super-high resolution image either directly in the camera or using a dedicated application.

It is possible, though, to produce super-resolution images using a regular camera courtesy of the [Highrise](https://github.com/dmpop/highrise) Bash shell script. To understand what the script does, here is a brief explanation of how super-resolution images are generated¹.

Imagine you have a regular camera with a sensor that can be shifted half a pixel in any direction. Instead of taking one image, this camera takes four: one centered, one shifted half a pixel right, one shifted half a pixel down, and one shifted half a pixel right and half a pixel down. We can then take the centered image, make it double the size (i.e. upscale it to 200%), spacing out the pixels as follows:

```
xxxx               x x x x 
xxxx
xxxx    ------>    x x x x 
xxxx
                   x x x x

                   x x x x
```

Then we can fill in the gaps, using the other shifted images: 1, 2, and 3:

```
x1x1x1x1
23232323
x1x1x1x1
23232323
x1x1x1x1
23232323
x1x1x1x1
23232323
```

This produces an image with twice the resolution of the original. Super-resolution with a standard camera is a bit more complex, as when you have uncontrolled camera or subject motion, you don’t get anywhere near an exact half pixel shift. But unless you are extremely unlucky, your shifted image will be offset by some amount from the original. By combining enough images you will get a very irregularly sampled image (with pixel samples that don’t fall onto a grid), but one which can be interpolated into a regular image by tracing the lines between samples to guess a result that does fall on an exact gridline. This is precisely what the Highrise script tries to achieve.

The script relies on ImageMagick and Hugin tools for upscaling, aligning, and assembling a stack of lower-resolution photos into a super-resolution image. This means that you need to install the required dependencies for the script to work. To do this on openSUSE, use the `sudo zypper in ImageMagick hugin exiftool` command.

You can then install Highrise by running the following commands:

```
git clone https://gitlab.com/dmpop/highrise.git
cd highrise
sudo cp highrise.sh /usr/local/bin/highrise
sudo chown root:root /usr/local/bin/highrise
sudo chmod 755 /usr/local/bin/highrise
```

To generate a super-resolution image, you need to take a series of photos first. Set your camera to the continuous shooting mode, and disable image stabilization. Take between 9 and 15 photos of the desired scene. It’s important that you don’t use a tripod, but shoot hand-held. For an even better result, enable manual focusing and shoot in the Manual mode. Also, keep in mind that the script works best with photos of static scenes.

Transfer the photos to your machine, then run the Highrise script using the following command:

```
highrise -e JPG -d /path/to/source/dir
```

Replace *JPG* with the actual file extension of the source photos, and */path/to/source/dir* with the absolute path to the directory containing the source photos. Generating super-resolution images is a computationally-intensive task, so depending on the size and number of source photos, it could take a while. Once the script is finished, you’ll find the resulting super-resolution images in the source directory. These files are recognizable by the *mean* and *median* postfixes in their names.

If the script failed to properly align the source photos, you can adjust several parameters to fix that. Open the script in a text editor and modify the available align parameters. Save the changes, and run the script again.

¹Source: [How does Super Resolution work?](https://photo.stackexchange.com/questions/24726/how-does-super-resolution-work)

# Konbini: KDE’s little photo helper

If you happen to use KDE as your preferred graphical desktop, [Konbini](https://gitlab.com/dmpop/konbini) might be right up your alley. It adds several useful image manipulation actions to the Dolphin file manager as well as installs and configures a handful of photography-related tools.

The supplied installer does the donkey job of fetching and installing the required pieces. It also adds the dedicated **Konbini** item to the right-click context menu in Dolphin. This menu gives you quick access to several useful commands that let you recompress and resize the currently selected image file, rename the file using date and time values extracted from its EXIF metadata, quickly geotag the selected photo, show the selected geotagged photo on OpenStreetMap, and more.

Installing Konbini is supremely easy. In the Terminal, run the `curl -sSL https://is.gd/konbini | bash` command for the installer to finish. The installer script is designed for use with openSUSE, Ubuntu, and Debian. But it can be easily modified to work with other Linux distributions.

In the *template* folder in the *konbini* directory you’ll find example files that you can use to create your own actions. Let’s say you want to create an action that uploads the currently selected photo to an FTP server. First, rename the *example* file in the *template/script* folder to something more descriptive like *upload-ftp*. Open the file for editing, remove the existing commands, and add the following code (replace the example values with the actual FTP server address or domain name, user name, and password):

```
[](#cb165-1)curl -T "$file" ftp://ftp.example.com/path/to/dir/ --user user:password
[](#cb165-2)notify-send "It works!"
```

Save the changes, then move the file to the */usr/local/bin/* directory, and make the script executable:

```
[](#cb166-1)sudo mv upload-ftp /usr/local/bin/
[](#cb166-2)sudo chown root:root /usr/local/bin/upload-ftp
[](#cb166-3)sudo chmod 755 /usr/local/bin/upload-ftp
```

Next, rename the *example.png* icon in the *template/icon* folder to *upload-ftp.png* and move it to the */usr/share/icons/konbini-icons/* directory:

```
mv upload-ftp.png /usr/share/icons/konbini-icons/
```

Instead of the supplied generic example icon, you can use a more appropriate icon from the [Feather Icons](https://feathericons.com/) set.

Finally, rename the *example.desktop* file in the *template/desktop* folder to *upload-ftp.desktop*, open it for editing and replace the example values:

```
[Desktop Entry]
Type=Service
X-KDE-Priority=TopLevel
X-KDE-Submenu=Konbini
ServiceTypes=KonqPopupMenu/Plugin
MimeType=image/jpeg;image/JPG;image/JPEG;image/jpg;
Actions=UploadFTP
[Desktop Action UploadFTP]
Name= Upload via FTP
Exec=/usr/local/bin/upload-ftp %f
Icon=/usr/share/icons/konbini-icons/upload-ftp.png
```

Save the changes, and move the file to the */usr/share/kservices5/ServiceMenus* directory:

```
mv upload-ftp.desktop /usr/share/kservices5/ServiceMenus/
```

Launch Dolphin, right-click on a JPEG image, and you should see the newly-added action in the **Konbini** menu.

# Keep tabs on what’s in your photo bag with Everyday Photo Carry

Need to keep tabs on the photographic equipment you carry in your photo bag? There are several apps and tools that can help you with that. But if you prefer to keep things simple and not share your data with third parties, then [Everyday Photo Carry](https://gitlab.com/dmpop/epc) (EPC) is what you need. It’s a simple PHP script that pulls data stored in the comma-separated format from a text file and renders it as an HTML page with a table.

![](media/file37.png)

EPC requires no installation. Clone the project’s GitLab repository using the `git clone https://gitlab.com/dmpop/epc.git` command, or download the source code directly from the project’s page. Open the *login.php* file, replace the example password with the desired one, and save the changes. Do the same with the *protect.php* file.

Since EPC is just a PHP script, you can run it on a web server with PHP, so you can access your data from anywhere. Move the *epc* folder into the document root of your server and point the browser to *http://127.0.0.1/epc* (replace *127.0.0.1* with the actual domain name or IP address of the server).

To run EPC on your local machine, you need to install PHP. To do this on openSUSE, run the `sudo zypper in php7` command. Use the `sudo apt-get install php7.2` command to install PHP on Ubuntu. In the terminal, switch to the *epc* directory, and run the `php -S localhost:8000` command. Point then the browser to the *localhost:8000* address to access EPC.

During the first run, EPC creates a data file and insert an example entry. To add and manage entries, press the **Edit** button. All data in EPC is stored in the comma-separated format, so each entry should look as follows:

```
ilce-6500.jpeg; Sony α6500 (ILCE-6500); 3157099; 1973-10-31
```

The first item in each entry should be a file name of the product. If you don’t want to add a product photo, enter *na* (as in *not available*).

To add product photos either copy them manually to the *epc/img folder*, or press the **Upload** link next to the **Edit** button and use the upload form to upload a photo.

# Plan photo travels with Simple Photo Planner

[Simple Photo Planner](https://gitlab.com/dmpop/sphp) (SPHP) is exactly that: a no-frills PHP tool that can be used to keep track of locations you plan to visit and photograph. It pulls data stored in the comma-separated format from a text file and renders it as an HTML page with a table.

![](media/file38.png)

SPHP requires no installation. Clone the project’s GitLab repository using the `git clone https://gitlab.com/dmpop/sphp.git` command, or download the source code directly from the project’s page, and you are good to go. To run SPHP on your local machine, you need to install PHP. To do this on openSUSE, run the `sudo zypper in php7` command. Use the `sudo apt-get install php7.2` command to install PHP on Ubuntu. In the Terminal, switch to the *sphp* directory, and run the `php -S localhost:8000` command. Point then the browser to the *localhost:8000* address to access SPHP.

You can add new entries to the list and modify the existing ones by editing the accompanying *data.csv* file in any text editor or spreadsheet application. You can specify three values for each entry: location (the name of the place), map link (shows the location on OpenStreetMap or Google Maps), and note.

Creating a map link in OpenStreetMap requires a few simple steps.

1.  Point your browser to [https://www.openstreetmap.org/](www.openstreetmap.org).
2.  Use the search box to find the desired place. Alternatively, use the mouse to find the place on the map.
3.  Click **Share** in the right-side toolbar to expand the **Share** palette. Enable the **Include marker** option, and switch to the **Short Link** section.
4.  If necessary, use the mouse to drag the marker to the exact location on the map.
5.  Copy the generated short link.

Generating a map link in Google Maps is equally simple. Use the search functionality to locate the desired place on the map, then use the **Share** option to generate a short link.

While SPHP may not be the most sophisticated PHP tool out there, it does have a few useful features. You can view the current weather conditions and forecast for the specific place by clicking on it. It’s possible to order by clicking the **Location** and **Note** column headers, and you can edit the data using the **Edit** button.

Since SPHP is just a PHP script, you can run it on a web server with PHP, so you can use the application from anywhere. Move the *sphp* folder into the document root of your server and point your browser to *http://127.0.0.1/sphp* (replace *127.0.0.1* with the actual domain name or IP address of the server).

## Protect Simple Photo Planner with a password

If you choose to run SPHP on a public web server, anyone can see and edit your data, which is probably not what you want. The solution is to protect your SPHP instance with a user name and password. On the Apache web server, this can be done using the *.htpasswd* and *.htaccess* files.

The *.htpasswd* file is a plain text file containing a list of user names and passwords. There are several ways to generate the file. If you have PHP installed on your system, you can use a simple PHP script for that:

```
[](#cb171-1)<?php
[](#cb171-2)$password = crypt($argv[2], base64_encode($argv[2]));
[](#cb171-3)echo $argv[1].":".$password;
[](#cb171-4)?>
```

Paste the code above into a new text file and save it under the *htpasswd.php* name. Run the `php htpasswd.php user password >> htpasswd` command, replacing *user* and *password* with the actual user name and password. Move the generated *htpasswd* file to the server, and make the file invisible by renaming it to *.htpasswd*.

Create a new text file, and paste the following code into it (replace */path/to/* with the actual absolute path to the *.htpasswd* file):

```
AuthType Basic
AuthName "Simple Photo Planner"
AuthUserFile /path/to/.htpasswd
require valid-user
```

Save the file under the *htaccess* name, move it into the *sphp* directory on the server, and make the file invisible by renaming it to *.htaccess*.

# Follow photographers on Instagram without an account

Love it or hate it, but plenty of great photographers use Instagram to share their photos. But like many other services, Instagram calls itself a sharing social platform, when in reality it’s just another walled garden that forces you to create an account and use their app. But it is entirely possible to follow your favorite photographers on Instagram without joining the service, courtesy of [RSS-Bridge](https://github.com/RSS-Bridge/rss-bridge). As the name suggests, this nifty PHP-based web application can generate RSS feeds for services and platforms that lack this functionality. Using RSS-Bridge, you can create RSS feeds for each Instagram account you want to follow, and then use any RSS reader to subscribe to the generated RSS feed. Better still, RSS-Bridge is supremely easy to install and use, so it doesn’t introduce any complexity or inconvenience. In fact, following your favorite photographers outside Instagram has its advantages. There are no distracting ads, no algorithms deciding what to show you, and no pointless likes and comments.

Since RSS-Bridge is written in PHP, it will happily run on any web server or hosted service that has PHP. Deploying the application is not particularly complicated. Use the `git clone https://github.com/RSS-Bridge/rss-bridge.git` command to clone the project’s Git repository. Alternatively, use the **Download ZIP** button to grab the latest source code and unpack the downloaded archive. Rename the resulting directory (e.g., *rss-bridge*) if necessary, move it to the document root of your web server, and you’re done.

Point your browser to the installed RSS-Bridge instance (e.g., *https://127.0.0.1/rss-bridge*, where *127.0.0.1* is the domain name or IP address of the web server). Scroll down to the **Instagram Bridge** section and click **Show more**. Enter the desired Instagram user name into the appropriate field and press the **Atom** button. Use the generated link to add the generated Atom RSS feed to your favorite RSS reader. With RSS-Bridge, you can create feeds not only for users but also specific hashtags.

![](media/file39.png)

In addition to generating RSS feeds in the Atom and MRSS formats, RSS-Bridge can render the fetched data as an HTML page. This can come in useful if you need to quickly check an Instagram account without using a dedicated RSS reader.

RSS-Bridge supports other photo sharing services, such as Flickr, NASA Astronomy Picture of the Day, and Unsplash. However, they are disabled by default. To enable the desired bridge, open the *whitelist.txt* file in the *rss-bridge* directory, add the name of the bridge (e.g., *FlickrBridge*), and save the changes.

# Revision History

## Revision 20.05.19

*   [New] Geotag JPEG files using reference photo
*   [New] Using FTP feature in Sony α7 Mark III
*   [Update] Efficient JPEG compression with jpeg-recompress
*   [Remove] Build a simple Android photo app with Jasonette
*   [Remove] Extend Sony Alpha camera functionality with Sony-PMCA-RE

## Revision 20.04.05

*   [Update] Add useful info to EXIF metadata
*   [Update] Import and organize photos with Otto
*   [Update] Import photos and RAW files with Photo Funnel
*   [Remove] Build a simple Android photo app with Jasonette

## Revision 20.01.07

*   [Removed] Build a Raspberry Pi-based photo backup device

## Revision 19.12.15

*   [New] Use Hald CLUT presets with Lilut
*   [New] Use Little Backup Box to manage and process RAW files and photos
*   [Updated] Keep tabs on what’s in your photo bag with Everyday Photo Carry

## Revision 19.09.29

*   [New] Build a Raspberry Pi-based photo backup device: Add a 128x64 OLED display to Little Backup Box
*   [New] Build a Raspberry Pi-based photo backup device: Mobile backup workflow with Little Backup Box
*   [Updated] Build a Raspberry Pi-based photo backup device: Change the default backup mode
*   [New] Squeeze JPEG files with jpegoptim

## Revision 19.08.11

*   [Updated] Build a Raspberry Pi-based photo backup device

## Revision 19.07.29

*   [Updated] Build a Raspberry Pi-based photo backup device: Remote synchronization with Little Backup Box
*   [New] Build a Raspberry Pi-based photo backup device: Add notification functionality to Little Backup Box with Simplepush

## Revision 19.06.21

*   [Updated] Build a Raspberry Pi-based photo backup device
*   [New] Build a Raspberry Pi-based photo backup device: Configure internal storage backup

## Revision 19.04.29

*   [New] WIRC: Wi-Fi infrared remote control for Sony Alpha cameras
*   [Removed] Extend and Improve Microblog
*   [Updated] Import and organize photos with Otto

## Revision 19.03.31

*   [New] Show Your Photos in a New Browser Tab

## Revision 19.02.17

*   [Updated] Build a Raspberry Pi-Based Photo Backup Device

## Revision 19.01.13

*   [New] Plan Photo Travels with Simple Photo Planner
*   [Updated] Keep Tabs on What’s in Your Photo Bag with Everyday Photo Carry

## Revision 19.01.01

*   [New] Keep Tabs on What’s in Your Photo Bag with Everyday Photo Carry

## Revision 18.12.21

*   [New] Simple PHP Script for Showcasing Photos
*   [New] Konbini: KDE’s Little Photo Helper
*   [Updated] Import and Organize Photos on a Linux-Based NAS with Momo

## Revision 18.09.30

*   [New] Turn Raspberry Pi into a Wireless Camera Server
*   [Updated] Take a Stroll down Memory Lane with Natsukashii: [Updated] Add Password Protection to Natsukashii

## Revision 18.08.25

*   [New] Add Useful Info to EXIF Metadata
*   [New] Follow Photographers on Instagram without an Account
*   [New] Built a Remote-Controlled Raspberry Pi Camera
*   [New] Build a Raspberry Pi-Based Photo Backup Device: Remote Backup with Little Backup Box

## Revision 18.07.21

*   [New] Import Photos and RAW Files: Import and Organize Photos on a NAS with Momo
*   [New] Take a Stroll down Memory Lane with Natsukashii
*   [Removed] Sonnenhut: Simple Dashboard for Photographers
*   [Removed] Control Camera via Web with gPhoto2 Bottle

## Revision 18.06.03

*   [New] Import Photos and RAW Files: Drag-and-Drop Import with Photo Funnel

## Revision 18.05.21

*   [New] Build a Raspberry Pi-Based Photo Backup Device: Extend and Improve Little Backup Box
*   [Updated] raw -> RAW
*   [Updated] Geotag Photos with Geophotobash

## Revision 18.04.03

*   [New] Build a Raspberry Pi-Based Photo Backup Device: Using Little Backup Box with an Android Hotspot

## Revision 18.03.25

*   [Updated] Build a Raspberry Pi-Based Photo Backup Device
*   [New] Extend and Improve Microblog

## Revision 18.03.19

*   [New] Build Static Photo Essays with Expose
*   [New] Generate Super-Resolution Photos with the Highrise Script

## Revision 18.02.07

*   [New] Backup and Recovery: Installing rclone on Android
*   [New] Build a Simple Android Photo App with Jasonette
*   [New] Extend Sony Alpha Camera Functionality with Sony-PMCA-RE
*   [New] Raspberry Pi-Based Photo Backup Device: Geocorrelate Photos with Little Backup Box

## Revision 17.12.27

*   [New] Raspberry Pi-Based Photo Backup Device: Troubleshooting Little Backup Box
*   [New] olympus-photosync: Wireless Bridge Between Olympus Cameras and Linux
*   [Updated] Efficient JPEG Compression with jpeg-recompress: Improved *monitor-recompress* script

## Revision 17.10.03

*   [New] Manage photos with digiKam
*   [New] Draw Inspiration from Unsplash with the Unbash Script
*   [Removed] Turn GIMP into a Digital Darkroom with the UFRaw Plugin and Scripts
*   [Removed] Post-Process Photos and RAW Files with Pixeluvo

## Revision 17.08.17

*   [New] Faster Access to Image Processing Actions via Context Menus: Compare Photos with ImageMagick and a KDE Service Menu Action
*   [New] Store Photos and Raw Files on an Encrypted Encrypted Storage Device
*   [New] Raspberry Pi-Based Photo Backup Device: Reconfigure Wi-Fi on Little Backup Box

## Revision 17.07.01

*   [New] Faster Access to Image Processing Actions via Context Menus
*   [Updated] This Day Last Year Photo with a Bash Script -> Travel Back in Time with a Bash Script

## Revision 17.06.23

*   [New] This Day Last Year Photo with a Bash Script

## Revision 17.05.15

*   [New] Sonnenhut: Simple Dashboard for Photographers
*   [New] Publish and Share Photo with Mejiro: Map Photos with uMap and PHP
*   [Updated] Optimized images

## Revision 17.04.09

*   [New] Efficient JPEG Compression with jpeg-recompress

## Revision 17.02.19

*   [New] Backup and Recovery: Detect Data Rot in Photos and Raw Files
*   [New] Geotag and Organize Photos with Geophotobash: Geophotobash Simplified

## Revision 17.01.15

*   [Updated] Add Useful Functions to the Bash Shell: Add Captions with Basic EXIF Data to Photos
*   [New] Add Useful Functions to the Bash Shell: Show Geotagged Photos on OpenStreetMap

## Revision 17.01.05

*   [New] Color Transformations with Hald CLUT: Apply Multiple Hald-CLUT Presets in a Single Action with a Bash Shell Script
*   [New] Post-Process Photos and Raw Files with Pixeluvo: Running Pixeluvo on openSUSE
*   [New] Add Useful Functions to the Bash Shell: Add Captions with Basic EXIF Data to Photos

## Revision 16.12.29

*   [Updated] Fixed typos and errors
*   [New] Give Your Bash Shell Photo Powers: Assemble Photos into a GIF Animation or a Slideshow with ImageMagick

## Revision 16.12.19

*   [Updated] Fixed typos and replaced `#!/usr/bin/bash` with `#!/usr/bin/env bash`

## Revision 16.12.03

*   [Updated] Fixed typos and updated links

## Revision 16.11.21

*   [New] Drag-and-Drop Photo Copying Tool
*   [Updated] Replaced RAW with raw
*   [Updated] Cloud Backup with rclone: Replaced HubiC with Amazon Drive

## Revision 16.11.07

*   [New] Turn GIMP into a Digital Darkroom with the UFRaw Plugin and Scripts

## Revision 16.10.03

*   [New] Command-Line Photographic Workflow on Android with Termux

## Revision 16.09.13

*   [Updated] Import Photos and RAW Files

## Revision 16.09.03

*   [Updated] Import Photos and RAW Files

## Revision 16.08.05

*   [New] Post-Process Photos and RAW Files with Pixeluvo
*   [Updated] Raspberry Pi-Based Photo Backup Device: Camera Backup with Little Backup Box

## Revision 16.07.25

*   [New] Geocorrelate Photos with GPS Logger for Android and ExifTool
*   [New] Rename Photos and Edit EXIF Metadata with jhead
*   [Updated] Import Photos and RAW Files

## Revision 16.07.11

*   [New] Control Camera via Web with gPhoto2 Bottle

## Revision 16.07.09

*   [New] Organize and Manage Photos with ExifTool
*   [Updated] Backup and Recovery + Raspberry Pi-Based Photo Backup Device

## Revision 16.07.01

*   [New] Mobile Raspberry Pi-Based Photo Backup Device: Controlling and Updating Little Backup Box

## Revision 16.06.21

*   [New] Mobile Raspberry Pi-Based Photo Backup Device: Preparatory Work
*   [Updated] Give Your Bash Shell Photo Powers: Resize Photos

## Revision 16.06.19

*   [New] Organize Photos: ExifTool-Based Multi-Purpose Bash Script
*   [New] Backup and Recovery: Recovering Photos with PhotoRec

## Revision 16.06.17

*   [Updated] Cloud and Mobile Backup: Installing rclone

## Revision 16.06.13

*   [New] Control Sony Alpha Camera from Linux with Sony Camera Remote API

## Revision 16.06.03

*   [New] Color Management on Linux

## Revision 16.05.30

*   [New] Cloud and Mobile Backup: Back up Photos from Android Device on Little Backup Box
*   [New] Cloud and Mobile Backup: Connect Little Backup Box to A Wireless Network and Access Photos via DLNA
*   [Updated] Cloud and Mobile Backup: Mobile Raspberry-Pi-Based Photo Backup Device
*   [Updated] Import Photos and RAW Files: Improving Basic Import Script

## Revision 16.05.23

*   [New] Import Photos and RAW Files: Improving Basic Import Script
*   [New] Color Correction with Hald CLUT: Practical Example
*   [New] Give Your Bash Shell Photo Powers: Geotag Photos with Reference Snapshots
*   [Updated] Cloud and Mobile Backup: Cloud Backup with rclone

## Revision 0 16.05.19