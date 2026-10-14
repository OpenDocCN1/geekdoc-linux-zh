⇒ To increase the height of phoenix.jpeg by 25 percent and decrease its width by 50 percent, type:

```
$ mogrify -geometry 125%x50% phoenix.jpeg [RET]
```

This command transforms the original phoenix.jpeg to an image whose height was increased by 25 percent and width increased by 50 percent, as in Figure 18-4.

# 18.1.2 Rotating an Image

To rotate an image, use mogrify with the -rotate option followed by the number of degrees to rotate by. If the image width exceeds its height, follow this number with a ">", and if the height exceeds its width, follow it with a "<". (Because both < and > are shell redirection operators, enclose this argument in quotes, omitting either if the image height and width are the same.)

⇒ To rotate phoenix.jpeg, whose height exceeds its width, by 90 degrees, type:

```
$ mogrify -rotate '90<' phoenix.jpeg [RET]
```

This command transforms the original phoenix.jpeg so that it is rotated by 90 degrees, as in Figure 18-5.

![](bbox=[0.32, 0.68, 0.68, 0.88])

Figure 18-5. The phoenix.jpeg image rotated.

NOTES: After this command, the width of phoenix.jpeg now exceeds its height, so to rotate it again use ">" instead of "<".

# 18.1.3 Adjusting the Colors of an Image

You can use mogrify to make a number of adjustments in the color of an image. To reduce the number of colors in an image, use the -colors option, followed by the number of colors to use.