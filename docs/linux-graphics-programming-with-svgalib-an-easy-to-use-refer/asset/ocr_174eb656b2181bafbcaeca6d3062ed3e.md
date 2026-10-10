```
dx = 2000; dy = -2000; dz = 0;
break;
case 5:
dx = 0; dy = 0; dz = 0;
break;
default:
dx = dy = dz = 0;
break;
}

printf("\tmatrix Pre scale 1000 1000 1000:\n");
printf("\tmatrix Pre translate %d %d %d \n", dx, dy, dz);
}

void pphigs_trailer()
{
printf("\n");
}
```

# Texture Mapping

Texture mapping is an intriguing concept, and it's fairly easy to understand, conceptually. Imagine taking a flat piece of aluminum foil and wrapping it around a baseball so that the baseball is completely covered. This, in essence, is texture mapping. If you have a flat (two-dimensional) piece of artwork, it's possible to transpose this onto a 3D object by means of texture mapping. If done properly, the “texture” (the artwork) will distort, appearing to trail off in the distance as it covers the object in space.

SVGAlib comes complete with its own 3D toolset called, simply enough, the threeDKit. One of the sample programs provided with the threeDKit is wrapdemo, which demonstrates texture mapping with a picture of Susanna Rubens (who we can assume is/was an object of desire for threeDKit's creator, Paul Sheer). The program is actually composed of multiple source files, but Listing 12.2 shows the functions that actually compute the image's surface.

# Listing 12.2 Wrapsurf.c.

```
/*
File: wrapsurf.c

Comments or suggestions welcome.

This function wraps a bitmap over a surface.
See wrapdemo.c for a demonstration of its use.
Use bitmap data of only 256x512 (see writriangle.c)
although any region within the bitmap can be drawn
to the full extents of the surface, so multiple
```