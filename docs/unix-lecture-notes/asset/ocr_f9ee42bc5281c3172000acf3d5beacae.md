# 6.12.5 Simulating Multiple Timers

Even though a process can have only a single timer, it is still possible to animate an unlimited number of independently moving objects. The key is to simulate in the program exactly what the kernel does with its timers relatively to the system clock. The idea is to create an array of the objects to be animated. Each entry of the array can have all of the information needed to animate a single object, and in particular, the length of the interval between movements of that object. In the world of animation, these movable creatures are called sprites, so I will call them that here.

In essence, a sprite can be represented by a structure such as the one below.

```
struct sprite
{
    int      interval;    // number of time units between redraws
    int      counter;     // counter for elapsed time between redraws
    char     shape;       // shape used to draw object
    position display_pos; // current location on screen (int,int)
    position real_pos;    // current real location  (double, double)
    double   dx;          // current x-coordinate of direction
    double   dy;          // current y-coordinate of direction
};
```

For each tick of the process's single interval timer, it can iterate through an array of sprites, decrementing each counter. If any counter reaches 0, it copies the interval value into it and issues a request to move the sprite in the (dx,dy) direction from position real_pos. The particular implementation above uses two positions, a real position and a display position. The idea is to keep track of the actual position as a floating point value, and display it in the cell in which its center of mass resides. The real position is updated by the (dx,dy) value and then the display position is calculated from that. The (dx,dy) pair is a vector of length 1 that is added to the real position of the point. The display cell is obtained by rounding the x and y values to the nearest integer. Moving a sprite can be accomplished with the following function.

# Listing 6.20: move_sprite()

```
void move_sprite(sprite *sp)
{
    erase_sprite(*sp);

    sp->real_pos.y += sp->dy;
    sp->real_pos.x += sp->dx;
    sp->display_pos.r = (int)( sp->real_pos.y + 0.5 );
    sp->display_pos.c = (int)( sp->real_pos.x + 0.5 );
    draw_sprite(*sp);

    if ( ( sp->real_pos.y > LINES-0.5 ) && ( sp->dy > 0 ) )
        sp->dy = -sp->dy;
}
```