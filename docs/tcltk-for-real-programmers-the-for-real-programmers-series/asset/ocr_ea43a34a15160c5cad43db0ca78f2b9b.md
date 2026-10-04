# 8.3 Common Options

values, with an equal number of digits in each value, and assigned to the red, green, and blue color intensities in that order. The intensities range from 0 (black) to 0xF, 0xFF, 0FFF, or 0xFFFF (full brightness), depending on the number of digits used to define the colors.

Thus, #f00 (bright red, no green, no blue) creates deep red, #aa02dd (medium red, dim green, medium blue) creates purple, and #ffffee0000 (bright red, bright green, no blue) creates a golden yellow.

# 8.2.3 Dimension Conventions

The size or location of a Tk object is given as a number followed by an optional unit identifier. The numeric value is maintained as a floating-point value. Even pixels can be described as fractions. If there is no unit identifier, the numeric value defaults to pixels. You can describe a size or location in inches, millimeters, centimeters, or points (1/72 of an inch) by using the unit identifiers shown in the following examples.

+   15.3 15.3 pixels
1.5i 11/2 inches
10m 10 millimeters (1 cm)
1.3c 1.3 centimeters (13 mm)
90p 90 points (1 1/4 inches)

# 8.3 Common Options

The Tk widgets support many display and action options. Unfortunately, these options have reasonable default values associated with them; thus you don't need to define every option for every widget you use.

These are some common options supported by many Tk widgets. They will be described once here, rather than with each widget that supports these options. Widget-specific options will be defined with the individual widget discussions.

215