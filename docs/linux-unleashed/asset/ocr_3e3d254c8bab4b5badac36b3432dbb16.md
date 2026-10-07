the program name ghostscript and class name Ghostscript in the `.xdafults` file. Your `.Xdafults` file should have three entries at a minimum in it, like this:

```
Ghostscript*geometry:             -0+0
Ghostscript*xResolution:        72
Ghostscript*yResolution:        72
```

If these entries are missing from your `.Xdafults` file, enter them using an editor and reload the defaults either by restarting the server or by issuing the following command, assuming you are in your home directory:

```
xrdb -merge ./.Xdafults
```

If not, specify the path to your `.Xdafults` file.

Ghostscript can make use of a number of resources in the `.xdafults` file, although most are of little use to you since defaults work just fine. The resources you can set in Ghostscript are shown in Table 24.1.

# TABLE 24.1. X RESOURCES SUPPORTED BY GHOSTSCRIPT.

| Resource name | Class of resource | Default value |
| :--- | :--- | :--- |
| background | Background | white |
| foreground | Foreground | black |
| borderColor | BorderColor | black |
| borderWidth | BorderWidth | 1 |
| geometry | Geometry | NULL |
| xResolution | Resolution | calculated |
| yResolution | Resolution | calculated |
| useExternalFonts | UseExternalFonts | true |
| useScalableFonts | UseScalableFonts | true |
| logExternalFonts | LogExternalFonts | false |
| externalFontTolerance | ExternalFontTolerance | 10.0 |
| palette | Palette | Color |
| maxGrayRamp | MaxGrayRamp | 128 |
| maxRGBRamp | MaxRGBRamp | 5 |
| useBackingPixmap | UseBackingPixmap | true |
| useXPutImage | UseXPutImage | true |

continues

![](bbox=[0.88, 0.61, 1.0, 0.77])