
## Spatial Subdivision

Fortunately, you can extend the range of your mountain(s) into the third dimension, too. The process then becomes what's known as *spatial subdivision*, an example of which is shown in Figures 16.6 through 16.9. For now, though, concentrate on Figure 16.5, which displays the entirety of one loop (*or iteration*). In the beginning (on the left) you can see a square extending off into the distance. The square is subdivided (in the middle) and then randomly perturbed so that the intersections of the lines are randomly raised or lowered (ending with the final image on the right).

Again, just a few iterations of this process are all that's needed to demonstrate the effect. By the final subdivision, shown in Figure 16.9, what you have does indeed appear to be a wire-frame model of a landscape. As you can see, the “mountainous” effect becomes more and more apparent with each cycle. It stands to reason that if the squares were colored in at some point, the effect might look fairly realistic.

This is one way—albeit a crude way—to generate a landscape. If you further broke down the squares into triangles, you could even employ SVGAlib's threeDKit (using gl_triangle()) to smoothly color your mountains, thereby eliminating any abrupt changes in hue.

> > **Note**
> > *This triangle shading process would be an application of the “filled polygon” technique discussed in Chapter 12.*

![](img/2e475714ef8969ed272622c46473d334_331_0.png)

**Figure 16.5**
Spatial subdivision.

![](img/2e475714ef8969ed272622c46473d334_331_1.png)

**Figure 16.6**
Recursive subdivision (2×2).

![](img/2e475714ef8969ed272622c46473d334_332_0.png)

**Figure 16.7**
Recursive subdivision (4×4).

![](img/2e475714ef8969ed272622c46473d334_332_1.png)

**Figure 16.8**
Recursive subdivision (8×8).

![](img/2e475714ef8969ed272622c46473d334_332_2.png)

**Figure 16.9**
Recursive subdivision (32×32).

## The Diamond-Square Algorithm

The actual mechanics of spatial subdivision were first documented by Alain Fournier, Don Fussell, and Loren Carpenter at the height of New Wave fashion—1982. In their paper entitled, “Computer Rendering of Stochastic Models,” they described what is now commonly known as the Diamond-Square algorithm. The methodology is simple, as can be evidenced in Figures 16.10 and 16.11.

![](img/2e475714ef8969ed272622c46473d334_333_0.png)

**Figure 16.10**
Steps 1 through 3 of the Diamond-Square Algorithm.

Beginning with a simple grid (such as the ones in Figures 16.5 and 16.10), the following two-step process is undertaken for as many times as needed:

1. For each of the “squares” in the grid, a midpoint is determined, and a new, central point is created. This is known as the diamond step, because the grid now appears to be comprised of diamonds.
2. Next, each of the diamonds has its midpoint calculated and subsequently plotted. This is the square step, as the grid again resembles a bunch of squares.

It should only take a few iterations to develop a sufficiently detailed grid. For more detail, simply lather, rinse, and repeat. If the end result were destined to be a three-dimensional landscape, then each new point would also be assigned a random elevation, based on the height of its surrounding neighbors. In such a way, a terrain map could be generated very quickly.

![](img/2e475714ef8969ed272622c46473d334_333_1.png)

**Figure 16.11**
Finishing up the Diamond-Square Algorithm.

## Heightfields

The next technique involves the use of heightfields. A heightfield is an array of values that describes the elevation of points on a grid. In other words, if you have an x-y grid that stretches off into the distance (not unlike the left image in Figure 16.5), you could assign a value to every point on that grid. The value would then represent the height (or elevation) of the point.

A heightfield is nice to work with because it’s portable. Because it consists of nothing more than an array, it can be created on one computer and then transferred to another for rendering. More simply, it allows you to split up the process of landscape design. One function (or program) creates the landscape, whereas another does the actual drawing.

The program given in Listing 16.1 creates a heightfield and then renders it with a simple raytracing (or ray-casting) algorithm. The interesting thing is that you can view the landscape from a first-person perspective. In other words, it appears that you’re actually involved in the scene and not just a distant observer. Furthermore, by using the mouse, you can turn left and right, and move up and down to inspect the terrain. A sample view is shown in Figure 16.12 later in this chapter.

The landscape is drawn in shades of red, which gives it an otherworldly look. By pressing the plus key (+), you can “move forward” over this strange environment, which is rendered as you go. The result is absolutely spectacular, and if you compile only one program in this book, I highly recommend you compile this one. The closest thing I can compare it to is the scene near the end of 2001: A Space Odyssey, where Dave is flying over the surface of a distant moon. Of course, the code has been included on the companion CD-ROM, so you can save yourself the trouble of retyping everything. Have a look.

## **Listing 16.1  A ray-casting heightfield engine.**

```c
//
//      Ray-Casting Heightfield Engine
//      written by: Alex Chalfin
//      ported to SVGAlib by: Jay Link
//

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <malloc.h>
#include <math.h>
#include <time.h>
#include <unistd.h>
#include <vga.h>
#include <vgagl.h>
#include <vgamouse.h>

/*---------------------------
* Floating point related macros
*---------------------------*/
#define  FLT2INT(a) (int(a))
/*  float to integer conversion */
#define  FLT2FXD(a) (FLT2INT((a)*65536))
/*  float to 16.16 fixed point */

/*----------------------------------------------------*/
Map size and indexing related macros
/*----------------------------------------------------*/
#define MAPSHIFT    8
/* log2(map_dimension) */
#define MAPSIZE      (1 << MAPSHIFT)
/* size of one side of the map */
#define BYTE(a)      (a & (MAPSIZE-1))
/* map wrapping macro */
#define INDEX(x,y)   ((BYTE(y)<<MAPSHIFT)+BYTE(x))
/* std index calculation */
#define fpINDEX(x,y) (INDEX(x)>>16, y>>16))
/* fixed point 16.16 index calc */
#define iINDEX(x,y)  (INDEX(FLT2INT(x), FLT2INT(y)))
/* flt index calc */

/*----------------------------------------------------*/
A nice random macro (ranged)
/*----------------------------------------------------*/
#define RANDOM(range)  (rand() % (range))
#define DEG2RAD(ang)   ((ang)*2*3.141592/360)

/*----------------------------------------------------*/
Rendering related constants
/*----------------------------------------------------*/
#define FARDEPTH     100
/* how far into horizon to render */
#define HEIGHTMUL    48
/* perspective multiplication factor */
#define FIELD_OF_VIEW 90
/* 90 degree field of view */
#define RENDERWIDTH  320
/* width of the screen to render to */
#define RENDERHEIGHT 200
/* height of the screen to render to */

/*----------------------------------------------------*/
Bi-linear filter blend
/*----------------------------------------------------*/
#define BLENDE(map,u,v,value) {
c0 = (int)(map)[fpINDEX(u, v)];        
c1 = (int)(map)[fpINDEX((u+65536), v)]; 
c2 = (int)(map)[fpINDEX(u, (v+65536))]; 
c3 = (int)(map)[fpINDEX((u+65536), (v+65536))]; 
c11 = (c0 << 8) + ((u & 0xffff) >> 8) * (c1 - c0); 
c22 = (c2 << 8) + (((u & 0xffff) >> 8) * (c3 - c2));
(value) = (c11 << 8) + (((v & 0xffff) >> 8) * (c22 - c11));
}

/*-------------------
 *  Types used in rendering process
 ------------------------------*/
typedef struct tview
{
    float cx, cy;
    float angle;
    int z;
} tview;

/*-------------------
 * Global Variables
 ------------------------------*/
char heightmap[MAPSIZE * MAPSIZE];
    /* height field for the voxels */
char colormap [MAPSIZE * MAPSIZE];
    /* colors for the voxels */
char vpage [RENDERWIDTH * RENDERHEIGHT];
    /* a virtual screen page */

/*-------------------
 * Function Headers
 ------------------------------*/
void  CreateMaps();
void  CreateFractalMap(int x1, int y1, int x2, int y2);
void  NewColor(int xa, int ya, int x, int y, int xb, int yb);
void  SmoothMap();
void  MakeColorMap();
void  DrawScreen(tview *v);
void  MakePalette();
void  SetRGB(char n, char r, char g, char b);
void  SetRenderView(float speed, float moveangle, tview *v);
short int InitMouse();
void  ReadMouseCoords(short int *, short int *y);
void  CastRay(float x1, float y1, float x2, float y2,
        int viewer, int scr_x);

/*-------------------
 * Da main funk!
 ------------------------------*/
int main(void)
{
```
