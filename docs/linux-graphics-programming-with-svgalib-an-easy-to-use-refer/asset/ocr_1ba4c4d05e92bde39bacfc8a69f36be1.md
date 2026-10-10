![](bbox=[0.13, 0.07, 0.48, 0.26])

Figure 3.4
Neatly arranged boxes.

they were before. Now you know why. This problem can be fixed by altering the color palette, which we’ll get into in Chapter 5.

# ### Circles

Enough with these squares and rectangles. If you’ve seen one, you’ve seen them all. Let’s draw some circles.

You use gl_circle(int x, int y, int r, int c) to draw a circle under vggsl. This time, x and y refer to the center of the circle (not the upper-left corner, as with rectangles); r is the radius, and c is the color, as usual. If you position your circle so that it can’t be drawn (for example, if x = 0 and y = 0), you’ll get a segmation fault, so be careful.

Unfortunately, circles created with gl_circle() are hollow. If you need a filled-in circle, you’ll have to wait until Chapter 4. Until then, you can try to fill it in yourself using a variety of means. (I’ll save you some time, though, by telling you that simply drawing several circles and decreasing the radius by one with each successive circle won’t cut it.) See the code snippet in Listing 3.17 and Figure 3.5 for an example of what I mean.

# Listing 3.17 A faulty method for filling in circles.

```
```
int x = 50,
    y = 50,
    r,
    c = 4;

/* This still doesn't get all the spaces */
for (r = 50; r > 0; r--) {
    gl_circle(x, y, r, c);
}
```
```

You do get a pretty neat pattern, though.