
## 图 13.3

DistRay.c 的输出。

![](img/2e475714ef8969ed272622c46473d334_286_0.png)

## 表 13.1 近似渲染时间。

| DISTLEVELS | 时间 |
| :--- | :--- |
| 0 | 5.6 秒 |
| 6 | 6 分钟 |
| 16 | 1 小时 21 分钟 |
| 25 | 14 小时+ |

下一个示例，称为 DistRay，也将 24 位 PPM 图像直接写入标准输出，因此你还需要再次将 stdout 重定向到文件。

表 13.1 展示了使用不同的 DISTLEVELS 值时，重新渲染所需预计时间的量。渲染时间是基于 Cyrix 166 计算得出的。

当然，DISTLEVELS 的值越高，质量就越好。

最后，DistRay 的代码如清单 13.2 所示。我再次擅自利用 Geelnard 的代码来达成我自己的不良目的。谢谢，Marcus。

## 清单 13.2 Distray.c.

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define WIDTH 640
#define HEIGHT 480
#define EPSILON (1e-5)
/* Very small value, used for coordinate-comparisons */
#define MAXT (1e5)
/* Maximum t-distance for an intersection-point */
#define MAXREC 5
/* Maximum amount of recursions (reflection etc.) */
#define DISTRIB 6
/* Amount of distributed rays per "virtual" ray */
#define DISTLEVELS 2
/* How deep in the recursion-tree to allow distribution */
typedef unsigned char UBYTE;
typedef struct { double x,y,z; } VECTOR;

typedef struct {
    VECTOR color; /* Object color (r,g,b) */
    double diffuse; /* Diffuse reflection (0-1) */
    double reflect; /* Reflection (0-1) */
    double roughness; /* How rough the reflection is (0=very sharp) */
} TEXTURE;

typedef struct {
    VECTOR pos; /* Position (x,y,z) */
    double r; /* Radius (or size) */
    TEXTURE t; /* Texture */
} OBJ;

/*
* Objects ( - spheres). Only one sphere.
* Add more if you like :)
*/
OBJ objs[] = {
    /* Object 1 */
    {
        { 0, 4, 1.0 }, 1,
        {
            { 1.0, 0.4, 0.0 },
            0.4,
            0.8,
            0.02
        }
    }
};

#define NUMOBJS 1

/*
* Ground position (z-pos), and textures (tiled)
*/
double Groundpos = 0.0;
TEXTURE Groundtxt[2] = {
    {
        { 0.0, 0.1, 0.5 },
        0.8,
        0.44,
        0.02
    },
    {
        { 0.6, 1.0, 0.5 },
        0.8,
        0.44,
        0.01
    }
};

/*
* Only one light-source is supported (and it's white).
*/
VECTOR Lightpos = {-3.0, 1.0, 5.0};
double Lightr = 0.4;
/* Light-radius (for soft shadows) */

/*
* The camera position (x,y,z), and orientation.
*/
VECTOR Camerapos = {1.5, -1.4, 1.2};
VECTOR Cameraright = {3.0, 1.0, 0.0};
VECTOR Cameradif = {-1.0, 3.0, 0.0};
VECTOR Cameraup = {0.0, 0.0, 2.3717};

/*
* Ambient lighting (0.0-1.0)
*/
double Ambient = 0.3;

/* Skycolor (Skycolor[0] = horizon, Skycolor[1] = zenith ) */
VECTOR Skycolor[2] = { { 0.5, 0.3, 0.7 }, { 0.0, 0.0, 0.2 } };

/** ******************************************************
*
* Helpers (geometrical etc).
*** ******************************************************/

long rnd = 0x52462467L;

double Jitter( void )
{
    rnd = (1103515245L*rnd + 12345L) & 0x7fffffffL;
    return 1.0-((double)rnd/(double)0x3fffffff );
}

void ReflectVector( VECTOR *v2, VECTOR *v1, VECTOR *n )
{
    double a, b;

    b = n->x*v1->x + n->y*v1->y + n->z*v1->z;        /* b = |n|n^2 */
    a = v1->x*n->x + v1->y*n->y + v1->z*n->z;        /* a = v1.n */
    a = -2.0 * a / b;                                 /* a = -2*(v1.n)/|n|^2 */
    v2->x = v1->x + a*n->x;                           /* v2 = v1 + n*a */
    v2->y = v1->y + a*n->y;
    v2->z = v1->z + a*n->z;
}

double VectorLength( VECTOR *v )
{
    return sqrt( v->x*v->x + v->y*v->y + v->z*v->z );
}

void ScaleVector( VECTOR *v, double s )
{
    v->x *= s; v->y *= s; v->z *= s;
}

void DistribVector(VECTOR *d, VECTOR *n, double sa, double sb) 
{
    VECTOR a, b;
    double nl;

    if( fabs( n->z ) > EPSILON ) {
        a.x = n->y* n->z; a.y = -n->x*n->z; a.z = 0.0;
        b.x = a.y*n->z; b.y = -a.x*n->z;
        b.z = a.x*n->y - a.y*n->x;
    } else {
        a.x = n->y; a.y = -n->x; a.z = 0.0;
        b.x = b.y = 0.0; b.z = 1.0;
    }
    nl = VectorLength( n );
    ScaleVector( &a, sa*(nl/VectorLength( &a ))*Jitter() );
    ScaleVector( &b, sb*(nl/VectorLength( &b ))*Jitter() );
    d->x = a.x+b.x; d->y = a.y+b.y; d->z = a.z+b.z;
}

/****** ******
* Object intersection calculation routines.
**** */

double IntersectObjs(VECTOR *LinP, VECTOR *LinD,
VECTOR *Pnt, VECTOR *Norm, TEXTURE **txt)
{
    int objjn, tilenum;
    double t, tmp, A, B, C;
    VECTOR Pos;

    t = -1.0;

    /* Try intersection with ground plane first */
    if( fabs(LinD->z) > EPSILON ) {
        tmp = (GroundPos - LinP->z)/LinD->z;
        if( ( tmp > EPSILON ) && ( tmp < MAXT ) ){
            t = tmp;
            Pnt->x = LinP->x + LinD->x*t;
            /* Calculate intersection point */
            Pnt->y = LinP->y + LinD->y*t;
            Pnt->z = LinP->z + LinD->z*t;
            Norm->x = 0.0;
            /* Surface normal (always up) */
            Norm->y = 0.0;
            Norm->z = 1.0;
            tilenum = ( ((int)(Pnt->x*50000.0))+
                  ((int)(Pnt->y*50000.0)) ) & 1;
            *txt = & Groundtxt[ tilenum ];
        }
    }

    /* Get closest intersection (if any) */
    for( objjn = 0; objjn < NUMOBJS; objjn++ ) {
        Pos = objs[objjn].pos;
        Pos.x -= LinP->x;
        /* Translate object into "line-space" */
        Pos.y -= LinP->y;
        Pos.z -= LinP->z;
        A = 1.0 / (LinD->x*LinD->x + LinD->y*LinD->y +
                   LinD->z*LinD->z);

        B = (Pos.x*LinD->x + Pos.y*LinD->y +
             Pos.z*LinD->z) * A;
        C = (objs[objjn].r*objs[objjn].r - Pos.x*Pos.x -
             Pos.y*Pos.y - Pos.z*Pos.z) * A;
        if( (A - C + B*B) > 0.0 ) { /* ...else no hit */
            A = sqrt(A);
            if( (ttmp = B - A) < EPSILON ) ttmp = B + A;
            if( EPSILON<ttmp )&& ( (ttmp<t)||t<0.0) ) {
                t = ttmp;
                Pnt->x = LinD->x*t;
                /* Calculate intersection point */
                Pnt->y = LinD->y*t;
                Pnt->z = LinD->z*t;
                Norm->x = Pnt->x*Pos.x;
                /* Calculate surface normal */
                Norm->y = Pnt->y*Pos.y;
                Norm->z = Pnt->z*Pos.z;
                Pnt->x += LinP->x;
                /* Translate object back to "true-space" */
                Pnt->y += LinP->y;
                Pnt->z += LinP->z;
                *txt = &objs[objjn].t;
                /* Get surface properties */
            }
        }
    }

    return( t );
}

/**********************************************************************/
*
* Line-tracer routine (works recursively).
**********************************************************************/

void Traceline( VECTOR *LinP, VECTOR *LinD, VECTOR *Color,
                int reccount )
{
    VECTOR  Pnt, Norm, LDir, NewDir, NewDir2, TmpCol, TmpCol2;
    VECTOR  TmpPnt, TmpNorm, D;
    double  t, A, cosfi;
    TEXTURE *txt, *tmpxt;
    int     i, shadowcount, usedist;

    Color->x = Color->y = Color->z = 0.0;

    if( reccount > 0 ) {
        /* Only use distributed tracing in higher nodes of the
           recursion tree */
        usedist = ( (MAXREC-reccount) < DISTLEVELS ) ? 1 : 0;

        /* Try intersection with objects */
        t = IntersectObjs( LinP, LinD, &Pnt, &Norm, &txt );

        /* Get light-intensity in intersection-point
           (store in cosfi) */
        if( t > EPSILON ) {
            LDir.x = Lightpos.x-Pnt.x;
            /* Get line to light from surface */
            LDir.y = Lightpos.y-Pnt.y;
            LDir.z = Lightpos.z-Pnt.z;
            cosfi = LDir.x*Norm.x + LDir.y*Norm.y +
                    LDir.z*Norm.z;

            if(cosfi > 0.0) {
                /* If angle between lightline and normal < PI/2 */
                shadowcount = 0;
                if( usedist ) {
                    A = Lightr / VectorLength( &LDir );
                    for( i = 0; i < DISTRIB; i++ ) {
                        DistribVector( &D, &LDir, A, A );
                        NewDir = LDir;
                        NewDir.x += D.x; NewDir.y += D.y;
                        NewDir.z += D.z;

                        /* Check for shadows (ignore hit info,
                           may be used though)
                        */
                        t = IntersectObjs( &Pnt, &NewDir,
                                          &TmpPnt, &TmpNorm, &tmptxt );
                        if ( ( t < EPSILON ) || ( t > 1.0 ) )
                            shadowcount++;
                    }
                } else {
                    t = IntersectObjs( &Pnt, &LDir, &TmpPnt,
                                      &TmpNorm, &tmptxt );
                    if ( ( t < EPSILON ) || ( t > 1.0 ) )
                        shadowcount = DISTRIB;
                }
                if( shadowcount > 0 ){
                    A = Norm.x*Norm.x + Norm.y*Norm.y +
                        Norm.z*Norm.z;
                    A *= LDir.x*LDir.x + LDir.y*LDir.y +
                        LDir.z*LDir.z;
                    cosfi = (cosfi/sqrt(A))*txt->diffuse*
                        (double)shadowcount/DISTRIB;
                } else {
                    cosfi = 0.0;
                }
            } else {
                cosfi = 0.0;
            }
        } else {
            cosfi = 0.0;
        }
        Color->x = txt->color.x*(Ambient+cosfi);
        Color->y = txt->color.y*(Ambient+cosfi);
        Color->z = txt->color.z*(Ambient+cosfi);
        if( txt->reflect > EPSILON ) {
            ReflectVector( &NewDir, LinD, &Norm );
            TmpCol.x = TmpCol.y = TmpCol.z = 0.0;
            if( usedist && ( txt->roughness > EPSILON ) ) {
                for( i = 0; i < DISTRIB; i++ ) {
                    DistribVector( &D, &NewDir,
                                   txt->roughness, txt->roughness );
                    NewDir2 = NewDir;
                    NewDir2.x += D.x; NewDir2.y += D.y;
                    NewDir2.z += D.z;
                    TraceLine( &Pnt, &NewDir2, &TmpCol2,
                               reccount-1 );
                    TmpCol.x += TmpCol2.x;
                    TmpCol.y += TmpCol2.y;
                    TmpCol.z += TmpCol2.z;
                }
            }
        }
    }
}
```
