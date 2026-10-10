```
void gl_trisdrawpoint(void (setpixelfunc) (int x, int y, int color))
```

If this function is called with setpixelfunc set to a nonzero value, the function setpixelfunc is used thereafter to draw each pixel (instead of the usual direct screen buffer writes). This function need never be used, except if you want to use your own pixel-drawing function for extra effects. If you use this feature, you can be assured that none of the triangle routines will access the hardware, thus enabling portability to other environments.