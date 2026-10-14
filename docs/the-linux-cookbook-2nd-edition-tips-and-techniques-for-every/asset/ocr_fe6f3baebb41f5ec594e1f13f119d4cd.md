⇒ To make a PBM image out of the text “Recommended Reading,” writing the new file to header.pbm, type:

```
$ pbmtext Recommended Reading > header.pbm [RET]
```

This is useful for making image files of large texts, for purposes such as including that text as an illustration. To send a compressed file to pbmtext, use zcat (otherwise, the < redirection operator works fine).

⇒ To make a JPEG image containing the contents of the compressed file /usr/share/state/us-constitution.gz, writing to a file named constitution.jpeg, type (all on one line):

```
$ zcat /usr/share/state/us-constitution.gz | pbmtext |
convert - constitution.jpeg [RET]
```

# 19.5 Using Other Image Import Tools

There are many other tools for importing images from various sources. This field is changing all the time, with the introduction of new hardware devices and new tools to import from them. The following table describes some of the tools currently in popular use.

Camediaplay Downloads images from any digital cameras with Sanyo firmware, including the Olympus Camedia series.
DEB: camediaplay
RPM: camediaplay

Cqcam Captures images from Color QuickCams.
DEB: cqcam
RPM: cqcam
WWW: http://www.cs.duke.edu/~reynolds/cqcam/

Dvgrab Captures audio and video from those digital camcorders that use a IEEE1394 link (also known as FireWire), writing the output as an AVI file.
DEB: dvgrab
RPM: dvgrab
WWW: http://kino.schirmacher.de

Fuji Imports images from (and otherwise manipulates) Fuji digital cameras.
DEB: fujiplay