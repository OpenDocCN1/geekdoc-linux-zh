
# More Obscure PHP

```php
$tile_northing+=250)
for($tile_easting=$leftmost_tile_easting;
$tile_easting<=$rightmost_tile_easting;
$tile_easting+=250)
{
$full_image_x = 100*($tile_easting-$minimum_easting)/250;
$full_image_y = 100*($maximum_northing-$tile_northing)/250;
$tile_name = sprintf('%07d%07d.png', $tile_northing, $tile_easting);
if(!file_exists('tiles/'.$tile_name)) continue;
$tile = imagecreatefrompng('tiles/'.$tile_name);
imagecopy($full_image, $tile, $full_image_x, $full_image_y, 0, 0, 100, 100);
imagedestroy($tile);
}
ob_start();
imagepng($full_image);
imagedestroy($full_image);
$this->png_data = ob_get_contents();
ob_end_clean();
$this->data_length = strlen($this->png_data);
return true;
}

function stream_close()
{
$this->png_data = null;
}

function stream_read($bytes)
{
if(strlen($this->png_data)==0)
return false;
$return = substr($this->png_data, 0, $bytes);
$this->png_data = substr($this->png_data, $bytes);
return $return;
}

function stream_write(){}
function stream_eof()
{
return $this->png_data == 0;
}

function stream_tell()
{
return $this->data_length-strlen($this->png_data);
}

function stream_seek()
{
return false;
}

function stream_flush(){
    return false; // We don't store data, silly.
}

function stream_stat() 
{ 
    return false; 
} 

// We put the stream wrapper registration here, with the wrapper it 
// registers, to save the hassle of remembering to register it every 
// time we include the file. 
// 
// This of course assumes that we're never tempted to use the same 
// wrapper protocol (nzmg) for different types of stream. 
stream_wrapper_register('nzmg', 'orthophoto_stream');
```

## Chapter 3

As noted by the last line in the code, this class is registered with the “nzmg” protocol. The full format for an nzmg URL as implemented here is nzmg:///nnnnnnneeeeeeeerrrrrrr, with seven digits specifying each of the northing (a certain number of meters between 6460000 and 6489750 for Auckland), easting (meters between 2650000 and 2689750), and radius (also in meters, although there’s little point asking for anything larger than 20000, as it is the diagonal length of the entire 16 × 12 kilometer image).

The reason why position is given in terms of “northing” and “easting” rather than latitude and longitude is because with the Earth being neither a perfect sphere nor even an especially symmetrical spheroid, conversion from one to the other is by no means trivial. The New Zealand Map Grid employed in the present example was empirically determined and the resulting latitude/longitude-northing/easting mapping involves such things as evaluating a six-degree complex polynomial. (The precise specification from the Surveyor-General’s Office is available as OGS Technical Report 4.1, and can be obtained from the LINZ website.) It’s not relevant to the objective of this example, any more so than the exercise of mapping landmarks and delivery addresses to coordinates. Nor, for that matter, is the question of input data validation, including limiting the radius to something more sensible than 20 kilometers. All such specific tasks should be dealt with before reaching this stage, each item as broadly applicable as possible.

The imagery is stored as a collection of PNG files, each 100 × 100 pixels in size, corresponding to 250 × 250 meters in the real world, so there are 19,200 such files in total. Each is named according to the northing and easting of their southwest (bottom left) corner. Northings increase upwards, and eastings increase towards the right. Since northings and eastings are themselves measured in meters (that’s what they’re for), the tile immediately north of 647000202660000.png will be 64702502660000.png, and the tile immediately east would be 6470002660250.png. The tiles have been positioned so that the northings and eastings they’re known by are all multiples of 250. Since this property is shared by the parent image, the dimensions of which are also multiples of 100 pixels, these tiles cover the parent image exactly.

Again, most of the work is done in stream_open(), determining the size of the requested image, which tile contains its lower-left pixel, and how many tiles are required vertically and horizontally. GD Lib is used to create a new image (since the imagery is grayscale, there is no need to use truetype) of the intended size, and then a pair of nested loops reads appropriate tiles from disk and copies them into the image in progress. The total memory consumed at any one time for the storage of image data is sufficient for the image in progress and a single 100 × 100-pixel tile.

The last act of `stream_open()` is to convert the assembled GD Lib image into PNG data. This is by the simple expedient of asking GD Lib to output the image as a PNG, and using output buffering to capture the result.

Each call of `stream_read()` returns another chunk of the PNG data, discarding what has already been returned.

Since this is a read-only stream consisting of on-the-fly generated data, most of the remaining stream-access methods are meaningless. One thing that can be said about the data is how much remains available for reading, allowing `stream_tell()` to be defined.

Code that uses this class need know nothing about what it’s doing to match `nmgz://` requests with responses. For all it cares, `nmgz://648208926677120000500` is just another file, one that happens to contain a PNG image of a 1 kilometer-wide snapshot of central Auckland.

But hold on. If it’s just PNG data, and it’s just a file, then for all intents and purposes *it is just a PNG file*. Precisely. Here is an example of the wrapper being used. With the class in its own `orthophoto_stream.php` file, it assumes that latitude and longitude have been converted to northing and easting, and that the radius isn’t too large or small.

```php
include_once('orthophoto_stream.php'); // the class has to be declared before
                                       // it can be used, of course.
function display_orthophoto($northing, $seasting, $radius)
{
  $filename = sprintf('nmgz://%07d%07d', $northing, $seasting, $radius);

  // All the stream-based stuff happens here.
  $image = imagecreatefrompng($filename);

  // A bit of post-processing to raise this code above triviality.
  // Draw a circle of the specified radius (the image is a square, after
  // all), and place a cross at the centre.
  // We need to find the image's white value
  $white = imagecolorsearch($image, 255, 255, 255);
  if($white==-1) // Okay, it's not already there.
    $white = imagecolorallocate($image, 255, 255, 255);
  // The circle is centered on the image, and is just large enough to
  // touch the sides.
  $imagesize = imageX($image);
  $middle = $imagesize>>1;
  imageellipse($image, $middle, $middle, $imagesize, $imagesize, $white);
  imageline($image, $middle, $middle+5, $middle, $middle-5, $white);
  imageline($image, $middle+5, $middle, $middle-5, $middle, $white);
  imagestring($image, 0, 0, 0, 0,
              'Sourced from Orthophoto R11 Auckland Crown Copyright Reserved.',
              $white);
  imagepng($image);
  imagedestroy($image);
}
```

Needless to say, this example has been constructed as a compromise between real-world and pedagogical use, and there are plenty of directions in which the `orthophoto_stream` class could be improved.

One is that the supplied 21-digit filename could have an extension attached to indicate the desired image format, rather than remain fixed on PNG generation. Others include a more realistic (or at least flexible) storage mechanism that users control through a more fully-developed URL including hostnames and paths. Consider also the possibility of moving some of the time-leading work into stream_read(), thus cutting down on the amount of image data that needs to be retained at any given time. (Observe, however, that since GD Lib buffers only complete images, you'll be required to write your own code to output image data that is correct, yet incomplete pending future input.)

You would be serving yourself well if you follow the URL system for naming stream resources, as defined in RFC 3986, with guidelines given in RFC 2718. There may in fact already be a naming scheme in use that matches your application. (The official registry is maintained by the Internet Assigned Numbers Authority at http://www.iana.org/assignments/uri-schemes). If there is, use it. Then your application will cooperate with other applications in the future that use the same scheme without needing an extra layer of URL conversion to glue them together. (Actually, the same goes for any data format or communications protocol—if the rest of the world already has an agreed-upon standard for what you want, use it and save yourself the time and effort of creating a new one.)

> Note that all PHP URLs require the use of :// after the scheme name, regardless of whether or not there is a naming authority (host) involved, as PHP uses that character sequence to distinguish URLs from local file paths. In RFC 3986's terms, PHP only implements the first production of the four given for the "hier-part" component and leaves the "naming-authority" component optional. The RFC-Compliant workaround would be to use :///, implicitly specifying the local host as the naming authority.

## Summary

This has been a brief tour of some of the more underutilized areas of PHP's native function set. By using this functionality your code can be more compact and more reliable without sacrificing legibility. Array functions can often be used in place of sometimes complex loops, reducing the task to a single line of code and a helper function that can be captured and stored in a library for reuse. Function-handling functions allow you to decide at runtime not only which function you wish to use (a switch statement could do that), but also decide which functions are in this list you wish to select from, or even create the function from scratch. Streams allow you to hide the implementation details of how external data is read or written, allowing the rest of your program to be able to treat it as just another file.

There are always new features being added to PHP—new initialization settings to fine-tune its operation, new arguments to existing functions that enhance their utility (even the venerable function str_replace() has been given a new argument in PHP5), new functions, and even whole new categories of functions. All this makes learning PHP an ongoing affair in which there is always something you don't know about yet.
