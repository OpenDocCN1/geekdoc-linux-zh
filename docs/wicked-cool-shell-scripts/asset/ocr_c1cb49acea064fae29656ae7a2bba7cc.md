# Running the Script

Listing 14-8 shows the script at work, creating new thumbnails in different sizes for a photo of Hawaii.

# The Results

```
$ thumbnails
Usage: thumbnails (-e|-f) thumbnail-size image [image] [image]
-e resize to exact dimensions, ignoring original proportions
-f fit image into specified dimensions, retaining proportion
-s strip EXIF information (make ready for web use)
please use WIDTHxHEIGHT for requested size (e.g., 100x100)
$ thumbnails -s -e 300x300 hawaii.png
Creating 300x300 (exact size) thumb for file hawaii.png
$ thumbnails -f 300x300 hawaii.png
Creating 300x300 (max size) thumb for file hawaii.png
$
```

Listing 14-8: Running the thumbnails script

# Hacking the Script

A neat addition to this script would be the ability to make an assortment of thumbnails based on multiple size ranges passed in, so for example, you could create a 100 × 100, 500 × 500, and wallpaper-sized 1024 × 768 image all in one go. On the other hand, perhaps such a task is better left to another shell script.

# #98 Interpreting GPS Geolocation Information

Most photographs nowadays are taken with cell phones or other smart digital devices that know their latitude and longitude. There’s a privacy issue with this, of course, but there’s also something interesting about being able to pinpoint where a photograph was taken. Unfortunately, while ImageMagick’s identify tool lets you extract that GPS information, the format of the data makes it hard to read:

```
exif:GPSLatitude: 40/1, 4/1, 1983/100
exif:GPSLatitudeRef: N
exif:GPSLongitude: 105/1, 12/1, 342/100
exif:GPSLongitudeRef: W
```

The information shown is in degrees, minutes, and seconds—which makes sense—but the format is nonintuitive, particularly since the format that a site like Google Maps or Bing Maps expects is more akin to this:

```
40 4' 19.83'' N, 105 12' 3.42'' W
```