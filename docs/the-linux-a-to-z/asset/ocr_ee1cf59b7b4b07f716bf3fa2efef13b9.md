![](bbox=[0.28, 0.08, 0.78, 0.72])

# Figure 9.1 A character grid and its encoding, for the letter A.

where sc.fnt is the name of the font file to load. If you try it, you will find that sc.fnt is quite a fun font, though you probably wouldn't want to use it all the time. By default, the font files are stored in the directory:

```
/usr/lib/kbd/consolefonts
```

In order to understand the contents and layout of a character font file, we need to take a simplified look at the mechanics of displaying text characters. On a VGA screen when it is displaying 25 lines of text that are 80 characters long, each character occupies a pixel grid on the screen which is eight pixels wide and 16 pixels high.

Next, each displayable character is made up of a set of lit and unlit pixels, also on an 8×16-pixel grid. To display a particular character on the screen in a particular position, all that is required is to copy the pixels from the correct character grid into the appropriate pixel grid position on the screen.

In the character grids, a pixel is represented by a single bit which just specifies whether the corresponding pixel is lit or unlit. This means that an easy way to store the pixel information for a complete 8×16-pixel grid is just as a set of 16 single-byte values - 1 byte for each 8-pixel row in the grid. Figure 9.1 shows a typical pixel grid for the letter A and the set of 16 byte values (in hex) that result. As you can see, the example letter A has a grid which is encoded as: