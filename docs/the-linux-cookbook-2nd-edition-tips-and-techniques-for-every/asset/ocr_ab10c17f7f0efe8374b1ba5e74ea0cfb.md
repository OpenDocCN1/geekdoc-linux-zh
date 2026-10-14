To *view* an image at a particular scale without modifying the file, use `display`; when you resize its window, you resize the image on the screen only, unless you choose to save it (see Recipe 4.3.2 [Resizing an X Window], page 106).

![](bbox=[0.03, 0.28, 0.95, 0.78])

*Figure 18-3. The* `phoenix.jpeg` *image scaled to exactly 640x480 pixels.*

# METHOD #1

To resize an image but maintain its *aspect ratio*, so that the ratio between the width and height stays the same, use `mogrify` with the `-geometry` option, and give the ideal width and height values, in pixels, as an argument.

⇒ To resize `phoenix.jpeg` to 480x320 pixels, type:

```
$ mogrify -geometry 480x320 phoenix.jpeg [RET]
```