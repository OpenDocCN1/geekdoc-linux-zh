```
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

/******  ******
* Object intersection calculation routines.
**** */

double IntersectObjs(VECTOR *LinP, VECTOR *LinD,
VECTOR *Pnt, VECTOR *Norm, TEXTURE **txt)
{
int objn, tilenum;
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
```