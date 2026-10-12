# More Obscure PHP

The stream’s activity starts at stream_open(). The first three substr()s split off the logged:// part of the URL, and then the username. The remainder is the URL of the resource actually requested:

```
$this->stream = fopen($path, $mode, $options&=~STREAM_REPORT_ERRORS);
$this->log_stream = fopen($path.'...log', 'a');
```

The logging stream opens the resource itself (with the STREAM_REPORT_ERRORS flag turned off, because those will be handled by this stream), and also reads a log file for appending. In this example, for simplicity the resource is merely another stream with an identical name as the one requested except for an extra .log extension. In a more practical setting, the logging would be done in some other way, since (for one thing) this mechanism would fail for read-only streams, but such an issue can be dealt with by writing a new stream class and registering it under a protocol name of its own. The second fopen() call would use this protocol and whatever happens from there on is a problem for the new class.

After that the two streams are checked to see that they’re actually open. An error is triggered and FALSE returned if either failed.

The last thing the stream does before returning true is to write a line to the newly opened logfile saying that the stream was opened, how, by whom, and when.

The bulk of the functionality of this class merely passes the corresponding file operations directly on to the stream it is keeping a log for. stream_read() and stream_write() have the added task of counting bytes as they pass back and forth, and rename() makes a note about the new name of the file (which, if it is opened as a logged stream, will have its own log file).

Finally, stream_close() writes the time and the total number of bytes transferred each way, before closing both of its own streams down.

# GIS Photographic Database Query

Land Information New Zealand (http://www.linz.govt.nz/) maintains a 2.5-meter resolution photographic atlas of the country. These aerial photos have been scaled and oriented so that their vertical and horizontal axes are respectively exactly north-south and east-west, to result in so-called “orthophotos.” The photography is available in the form of images 8000 × 6000 pixels in size, corresponding to an area of ground 3.2 × 2.4 kilometers in extent. Four such photos suffice to encompass Auckland City. Combined as a single grayscale PNG, an image of the entire city is 115MB in size.

Now imagine an online service in which users provide latitude and longitude for a point within Auckland, together with a radius, and the service responds with the appropriate image. The most straightforward method would be to load the image of the entire city, and copy the relevant portion. But that is infeasible simply due to the size of the image (remember that it is 115MB only while it is still compressed into a PNG file: uncompressed it’s about a byte for each of 192 million pixels).

Another approach would be to store the imagery in an uncompressed form (LINZ provides the imagery as uncompressed TIFF files), and write a program that can locate and read the relevant bytes only from one or more files (it’s 192 million bytes for one city, but it’s quite a lot more for the entire country, making for a lot of raw data that needs storing for ready access), without having to load the whole lot into memory. This is certainly the better option of the two, but it is not something that is well-suited to PHP, mainly due to speed considerations when it comes to assembling the final image from the bytes being read. A custom extension written in C would be more appropriate. Since the current discussion is looking at PHP’s stream wrapper interface, such a solution wouldn’t be especially edifying.