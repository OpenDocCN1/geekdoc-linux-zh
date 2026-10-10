
## History Of Fractals

The emergence of fractal science is due entirely to the efforts of one man: Benoit Mandelbrot. Finding traditional geometry to be cold and dry, Mandelbrot began his study of the regularities and irregularities of patterns in nature. His research was based on the work of earlier mathematicians such as duBois Reymond, Cantor, and Peano. He first published his findings in 1975, and fractals have been a part of modern science ever since.

Mandelbrot coined the term *fractal* from the Latin word *fractus*, which means *fragmented* or *irregular*. It pertains to recursion in chaos and random events. We'll have a look at an actual equation in the following section.

## Mandelbrot Set

The classic fractal equation is as follows:

$z_{(n+1)} = z_{(n)}^2 + c$

Using Table 8.1 as a reference, you could rewrite this as:

(a, b) = (axa-bxb, axb+bxa) + (x, y)

By plugging values into *z* and *c* (with both *z* and *c* being sets of ordered pairs/planar coordinates/complex numbers), one gets the famous *Mandelbrot* set. When mapped on a screen matrix, these numbers create the image seen in Figure 8.4. Note that *z* always starts at zero (0, 0).

Once again, the interesting thing about fractals (aside from their frequently amoebae-like appearance) is that if you were to magnify one, you would see a design that's identical to the appearance of the full-sized fractal. That is, they're recursive—a small segment resembles the whole. Figure 8.5 demonstrates this aspect quite well.

## Code

Listing 8.1 shows how to implement the Mandelbrot set in C. Because C can't handle complex numbers directly, a little finagling is necessary. However, the resultant code is still fairly compact. Also, note that a screen mode of at least 800×600 is necessary for the best results. I've gone ahead and stepped up to screen mode 12 (G1, 024×768×256) to provide even greater detail. Finally, be sure to use the `-Ivgag1` flag when compiling (hint, hint).

*Note*

Note that you might not need to include `<math.h>` and/or the `-lm` command line compilation flag. I don't seem to need this on my machine; this code compiles fine without it. However, some people whom I correspond with do, so I've included it for your convenience.

![](img/2e475714ef8969ed272622c46473d334_202_0.png)

**Figure 8.4**
The Mandelbrot set.

![](img/2e475714ef8969ed272622c46473d334_202_1.png)

**Figure 8.5**
Mandelbrot magnification.

**Listing 8.1** One way to code the Mandelbrot set.

```c
#include <stdlib.h>
#include <math.h>
#include <vga.h>
#include <vgagl.h>

int main(void)
{
    int sx=1024;         /* Screenwidth */
    int sy=768;          /* Screenheight */
    double xmin=-2;      /* smallest real value (x-axis) */
    double xmax=1.25;    /* largest real value (x-axis) */
    double ymin=-1.25;   /* smallest imaginary value (y-axis) */
    double ymax=1.25;    /* largest imaginary value (y-axis) */
    int maxiter=255;     /* Max number of iterations */

    double old_x;        /* temporary variable to store x-value */
    double fx,fy;        /* variable to store number of iterations */
    int m;

    double dx=(xmax-xmin)/sx; /* how much to add for each x-pixel? */
    double dy=(ymax-ymin)/sy;  /* how much to add for each y-pixel? */

    int px;               /* Variable storing current x-pixel */
    int py=0;             /* Variable storing current y-pixel */
    double x;            /* Variable storing current x-value */
    double y=ymin;       /* Variable storing current y-value */

    vga_init();
    vga_setmode(G1024x768x256);
    gl_setcontextvga(G1024x768x256);

    while (py<sy) {
        px=0;
        x=xmin;
        py++;
        while (px<sx) {
            px++;

            fx=x;
            fy=0;
            m=0;
            do {
                old_x=fx;
                fx=fx*fx-fy*fy+x;
                fy=2*old_x*fy+y;
                m++;
            } while ((fx*fx+fy*fy)<4) && (m<maxiter));

            gl_setpixelrgb(px, py, 0, 0, m);
            x+=dx;
        }
        y+=dy;
    }

    vga_getch();
    vga_setmode(TEXT);
    return 0;
}
```

I'll have to be candid; I didn't write this code myself (although I did port it to SVGA11b). Unfortunately, I have also managed to lose track of the original author. It may be possible, however, that it was written and enhanced by Ramiro Perez, Fausto Barbuto, and/or Michael Sargent. My apologies if that isn't the case.

This version of the program does provide you with another use of the `gl_setpixelrgb()` function (first seen in Chapter 5). The benefits of this should be immediately obvious—you get to set a point's color and actually plot it, all in one move.

## Julia Set

The Julia set (named for Gaston Julia) actually uses the same equation as the Mandelbrot set. How then is it different? Instead of *z* starting at zero (0, 0) and *c* being a coordinate point, the tables are turned: *z* is now the coordinate and *c* is a constant. The program in Listing 8.2 is a little different; you now get to input some values. I'll show you similar to my results after the listing. Note my use of `vga_getkey(void)`. This function is similar to `vga_getch()`, but instead of pausing the program's execution, it allows the loop to continue while it waits for input. This will be an important function in animation.

> **Note**
> You can find the original DOS version of this program (along with a plethora of others) at *spanky.triumf.ca/pub/fractals/code*. I'd copy the whole directory—it's that good.

**Listing 8.2** Julia Set.

```c
/*  Pre-SVGA11b code by Fausto Barbuto  */

#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <vga.h>

int main(int argc, char *argv[])
{
    register double xmin, xmax, ymin, ymax, fact=1.0;
    register double x, y, x0, y0, xp, yp, const_scr=1.0;
    register double deltax, deltay, p, q, ya, r, xkpl, ykpl;
    register int nplX=1024, nplY=768, kcolor;
    register int k, np, nq, ipen;
    char *endptr;

    p = strtod(argv[1],&endptr);
    q = strtod(argv[2],&endptr);
    xmin = strtod(argv[3],&endptr);
    xmax = strtod(argv[4],&endptr);
    ymin = strtod(argv[5],&endptr);
    ymax = strtod(argv[6],&endptr);
    Kcolor = atoi(argv[7]);
    if(Kcolor == 0) Kcolor = 256;

    vga_init();
    vga_setmode(VIDEOXGA); // G1024x768x256

    if(fact!=1.0 || fact <=0.0)
    {
        fact = 1.0;
    } else {
        npix = (int)(npix*fact);
        npiy = (int)(npiy*fact);
    }
    deltax = (xmax-xmin)/(double)(npix-1);
    deltay = (ymax-ymin)/(double)(npiy-1);

    vga_clear();
    for (np=0; np<=npix-1; np++)
    {
        x0 = xmin + (double)np*deltax;
        for (nq=0; nq<=npiy-1; nq++)
        {
            y0 = ymin + (double)nq*deltay;
            x = x0;
            y = y0;
            k = 0;

            /* Real part: XKP1 ; Imaginary: YKP1 */

            do {
                xkp1 = (x+y)*(x-y) + p;
                ya = x*y;
                ykp1 = ya + ya + q;
                r = xkp1*xkp1 + ykp1*ykp1;
                k++;
            } while (r < M && k < Kcolor); // Assuming M and Kcolor are defined elsewhere

            if (r >= kcolor)
            {
                ipen = 30 + k;
                xp = const_scr*(double)np;
                yp = (double)nq;
                vga_setcolor(ipen);
                vga_drawpixel(xp, yp);
            }

            /* Converging points in blue color. */
            if (k == kcolor)
            {
                ipen = 1;
                xp = const_scr*(double)np;
                yp = (double)nq;
                vga_setcolor(ipen);
                vga_drawpixel(xp, yp);
            }

            /* Returns if no convergence is achieved on either escape or attraction. */

            x = xkpl;
            y = ykpl;
        }
        if(vga_getkey())
        {
            break;
        }
    }

    /* Clean-up. */
    vga_getch();
    vga_setmode(TEXT);
    return 0;
}
```

Figure 8.6 shows what I get with the following input:

`julia .5 .25 -2 1.25 -1.25 1.25 156`

![](img/2e475714ef8969ed272622c46473d334_207_0.png)

**Figure 8.6**
The Julia set seen one way.

Now try it like this:

`julia -0.74356 0.11135 -2.0 2.0 -2.0 2.0 256`

Figure 8.7 shows the result of this input. Isn’t it nice to be able to get all these great patterns without recompiling the code?

## Fractal Plants

I’ve shown you some abstract fractal imagery in the preceding examples. They’re fun to play with, but what’s the point? Believe it or not, there is one. This is where the science of fractals and chaos comes in.

Some people believe that fractals contain the secrets of our physical world. (These are respectable scientists, mind you, and not people like the late Timothy Leary—although I have nothing against him). These people believe that nothing is truly random, and that all events in nature are based on predictable formulae. They point out that fractal equations can re-create coastlines, mountains, and other objects in nature that are self-similar. One such object is a fern leaf.

Look at Listing 8.3 and then at Figure 8.8 to see one way to create a fern. (I’ll bet before this example, you thought ferns were for sissies). All jokes aside, I find this code to be absolutely amazing. See what you think.
