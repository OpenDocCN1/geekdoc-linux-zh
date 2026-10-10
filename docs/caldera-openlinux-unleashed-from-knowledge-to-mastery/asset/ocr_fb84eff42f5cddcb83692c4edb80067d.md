that, then there may be fewer rows, or if there are fewer than five images, the composite will be wide enough to fit only the given images. If there are more images than can be placed in the maximum number of tiles for the composite (determined by the tiles per row and maximum number of rows), montage will create more than one composite image.

For example, to create a montage of your favorite fish and save it to the file `fishes.tif`, you could use a command similar to this:

```
$ montage salmon.tif trout.tif catfish.tif fishes.tif
```

To create a montage of all your fish pictures in the `fish` directory with tiles that are at most 256 by 192 pixels, surrounded by a red border, and separated by 10 pixels of back- ground color, you could use a command similar to this:

```
$ montage -geometry 256x192+10+10 -bordercolor red fish/* fish.stif
```

Table 27.6 lists some options that can be used with montage. See the montage manual page (man montage) for more information.

| TABLE 27.6 | Options for Use with montage |  |  |  |  |  |  |  |  |

| Option | Description |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -adjoin | Joins images into a single multi-image file. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -font _name_ | Specifies the font to use for the title and image labels. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -geometry _<width>x_<height>++<border>_<width>++<border>_height_> | Sets the preferred tile size and border width and height. Note: This is not the same as the image border; this is the spacing between tiles. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -label _name_ | Assigns a label to an image. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -mode _type_ | Sets the type of montage. Valid modes are Frame, UnFrame, and Concatenate. The default mode is UnFrame. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -pointsize _value_ | If montage is unable to get an X font, a PostScript font is used. This option specifies the point size for the font. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -shadow | Adds a shadow beneath a tile. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -texture _file_ | Uses the given file as a texture to tile on the background of the composite. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| -tile _<cols>x_<rows>> | Specifies the number of tiles per row and the maximum number of rows for the composite. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |