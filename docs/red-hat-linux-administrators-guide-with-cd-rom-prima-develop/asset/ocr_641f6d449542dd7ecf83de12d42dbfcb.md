# Listing 12.3 Configuring the Default Resolution for the X Window Envronment

```
```
#...................................

# Screen sections
#
..................................

# The Colour SVGA server

Section "Screen"
	Driver		"svga"
	# Use Device "Generic VGA" for Standard VGA 320x200x256
	#Device		"Generic VGA"
	Device		"3Dfx Interactive, Inc.|Voodoo 3 2000"
	Monitor		"My Monitor"

	Subsection "Display"
		Depth		16
		Modes		"1640x480"	"1280x1024"
		ViewPort	0 0
	EndSubsection
EndSection

# The accelerated servers (S3, Mach32, Mach8, 8514, P9000, AGX, W32,
# I128, and S3V)
Section "Screen"
	Driver		"accel"
	Device		"3Dfx Interactive, Inc.|Voodoo 3 2000"
	Monitor		"My Monitor"

	Subsection "Display"
		Depth		16
		Modes		"640x480"	"1280x1024"
		ViewPort	0 0
	EndSubsection
EndSection
```
```