Use the `-dither` option to reduce the colors with Floyd–Steinberg error diffusion, a popular algorithm for improving image quality during color reduction.

+   To reduce the colors in `phoenix.jpeg` to four and apply Floyd–Steinberg error diffusion, type:

```
$ mogrify -colors 4 -dither phoenix.jpeg RET
```

This transforms the original `phoenix.jpeg` to:

![](bbox=[0.38, 0.62, 0.62, 0.78])

Use the `-map` option with a second file name as an argument to read the color map, or the set of colors, from the second image and use them in the first image.

+   To change the colors in the file `rainbow.jpeg` to those used in the file `prism.jpeg`, type:

```
$ mogrify -map prism.jpeg rainbow.jpeg RET
```

Use the `-monochrome` option to make a color image black and white.

+   To make the color image `rainbow.jpeg` black and white, type:

```
$ mogrify -monochrome rainbow.jpeg RET
```

If you have a PPM file, use ppmquant to quantize, or reduce to a specified quantity the colors in the image—see the ppmquantman page for details (see section Reading a Page from the System Manual).

Because of differences in display hardware, the brightness of an image may vary from one computer system

![](bbox=[0.45, 0.12, 0.55, 0.28])