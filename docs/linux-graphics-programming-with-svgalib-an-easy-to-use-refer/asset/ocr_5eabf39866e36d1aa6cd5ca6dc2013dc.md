You may have also noticed my first use of **vga_setgacolor()**. This function is similar to **vga_setcolor()**, except that its argument may only be in the range of 0–15. The intended purpose is to allow you easy access to the 16 primary "computer" colors, regardless of the graphics mode you're in. This will come in handy later, when you'll be capable of tweaking color values by hand. Sometimes, it's nice to come back to the basics.

# # Moving Beyond gl_circle()

At this point, though, no progress has been made over the original **gl_circle()** function. Let's begin customizing the code by making the circle thicker—something **gl_circle()** can't do. Basically, all you'll be doing is drawing a succession of hollow circles, one inside another. Because they touch at the edges, they'll conglomerate to become one large (thick) circle. (Yes, I know you can execute several **gl_circle()** statements, but this will be all within one function.) Take a look at Listing 4.3 to see how I did it.

# **Listing 4.3** A thick circle.

```
```c
void book_circle(int xc, int yc, int radius, int thickness)
{
    double theta,
        costheta,
        sintheta;
    int degrees,
        i;
    
    for (degrees = 0; degrees < 360; degrees++)
    {
        /* Define PI as 3.14, if your compiler doesn't accept the following line. */
        theta = (PI / 180) * degrees;
        costheta = cos(theta);
        sintheta = sin(theta);
        
        for (i = radius; i > radius - thickness; i--)
        {
            vga_drawpixel(xc + i * costheta,
                yc + i * sintheta);
        }
    }
}
```
```

Now you've got yourself a big ol' circle, just like the one shown in Figure 4.3. See, we're making progress.