# ## Curves

The most obvious deficiency in SVGAlib's shape-drawing functions is the curve, or arc. That's not to say that SVGAlib is incapable of drawing a rounded object—of course it can. However, you won't find anything beyond gl_circle() in the base package. To compensate for this absence, you just need to do some math (uh, oh!).

> > **Note**
> >
> > I have to admit that I'm not a mathematician. Although all the examples in this chapter work, they may not be the most brilliant lines of code ever written. I hope you'll be able to forgive any inadequacies in my formulas—I've done the best I could. Perhaps those of you who are math wizards can contribute some knock-your-socks-off code to the SVGAlib Web site so that we may all learn from your expertise. Now, on with the show.

Let's start out by creating a function to draw a circle. After all, a circle is nothing more than connected arcs or one large arc, right? This code will be different from that found in gl_circle() so that those of you who are also mathematically disadvantaged can see multiple ways to accomplish the same thing. I've named this new function book_circle(), and Listing 4.1 contains the code. If this program looks familiar, it may be because I took the liberty of lifting most of it from GNU's libplot, from the plottul package. Actually, it wasn't a total theft; I've simplified it some for the book. Note that you'll need to include the `<math.h>` header file in your program; otherwise, you won't be able to compile. (Some people also find it necessary to link to the math library with the -lm flag, too.)

**Listing 4.1** Code for book_circle().

```
```c
void book_circle(int xc, int yc, int radius)
{
    double theta,
           costheta,
           sintheta;

    int degrees;

    for (degrees = 0; degrees < 360; degrees++)
    {
        /* Define PI as 3.14, if your compiler doesn't accept
           the following line. */
        theta = (PI / 180) * degrees;
        costheta = cos(theta);
        sintheta = sin(theta);

        vga_drawpixel(xc + radius * costheta,
                      yc + radius * sintheta);
    }
}
```
```