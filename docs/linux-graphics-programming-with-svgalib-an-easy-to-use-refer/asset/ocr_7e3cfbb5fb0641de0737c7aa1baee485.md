```
c22 = (c2 << 8) + (((u & 0xffff) >> 8) * (c3 - c2));
\(value) = (c11 << 8) + (((v & 0xffff) >> 8) * (c22 - c11));
```

```
/*-------------------
 *  Types used in rendering process
 ------------------------------*/
typedef struct tview
{
    float cx, cy;
    float angle;
    int z;
} tview;
```

```
/*-------------------
 * Global Variables
 ------------------------------*/
char heightmap[NAPSIZE * MAPSIZE];
    /* height field for the voxels */
char colormap [NAPSIZE * MAPSIZE];
    /* colors for the voxels */
char vpage [RENDERWIDTH * RENDERHEIGHT];
    /* a virtual screen page */
```

```
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
```

```
/*-------------------
 * Da main funk!
 ------------------------------*/
int main(void)
{
```