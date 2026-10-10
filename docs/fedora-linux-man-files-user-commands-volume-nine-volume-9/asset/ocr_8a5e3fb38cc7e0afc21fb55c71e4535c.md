-l -t -x -y
control the scan area: -l sets the top left x coordinate, -t the top left y coordinate, -x selects the width and -y the height of the scan area. All paratemers are specified in milliters by default.

# Enhancent options

—custom-gamma
(color mode only) allows the user to specify a gamma table (see the next 3 paraters).

—red-gamma-table
(color mode only) can be used to download a user defined gamma table for the red channel. The table st be 256 bytes long.

—green-gamma-table
(color mode only) can be used to download a user defined gamma table for the green channel. The table st be 256 bytes long.

—blue-gamma-table
(color mode only) can be used to download a user defined gamma table for the blue channel. The table st be 256 bytes long.

—dither
(Black & White only) select the dither mask to use. Possible values are Line art, 2x2, 3x3, 4x4 bayer, 4x4 smooth, 8x8 bayer, 8x8 smooth, 8x8 horizontal and 8x8 vertical

—preview
requests a preview scan. The resolution used for that scan is 22 dpi and the scan area is the maxim allowed. The scan mode is user selected. The default is “no”.