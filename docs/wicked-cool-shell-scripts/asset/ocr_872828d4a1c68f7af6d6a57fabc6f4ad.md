For a filename like abandoned-train.png, the suffix would be png and the prefix would be abandoned-train. Notice that the period (.), but we’ll add that back in when we build the new filename ②. Once that’s accomplished, it’s just a matter of invoking the convert program with all the parameters ③.

# Running the Script

Specify the type of frame you want—either with -frame (for more elaborate, 3D effects) or with -border (for a simple border)—along with the appropriate ImageMagick geometry values, a preferred color for the border or matte portion, and the input filename (or filenames). Listing 14-6 shows an example.

```
$ frameit -f 15x15x10+10 -m black abandoned-train.png
Adding a frame to image abandoned-train.png, saving as abandoned-train+f.png
```

Listing 14-6: Running the frameit script

# The Results

The result of this invocation is shown in Figure 14-2.

![](bbox=[0.22, 0.62, 0.85, 0.84])

Figure 14-2: A museum-style 3D matte frame

# Hacking the Script

If you forget a parameter, ImageMagick issues a typically baffling error:

```
$ frameit -f 15x15x10+10 alcatraz.png
Adding a frame to image alcatraz.png, saving as alcatraz+f.png
convert: option requires an argument `-mattecolor' @ error/convert.c/ConvertImageCommand/1936.
```