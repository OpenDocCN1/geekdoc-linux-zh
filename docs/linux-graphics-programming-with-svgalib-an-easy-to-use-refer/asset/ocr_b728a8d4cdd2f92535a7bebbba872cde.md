We've now got a square ranging from points (10, 10) in the upper left, (100, 10) in the upper right, (100, 100) in the lower right, and (10, 100) in the lower left. See Figure 3.2 for an illustration of this.

The problem is, this square is hollow. Let’s go ahead and draw three filled-in squares, and we’ll color them red, green, and blue. You can see how to do this in Listing 3.10.

# Listing 3.10 Three squares.

```
#include <stdlib.h>
#include <vga.h>
int main(void)
{
    int y;

    vga_init();
    vga_setmode(6320x200x256);

    vga_setcolor(4);
    for (y = 75; y < 120; y++)
    {
        vga_drawline(30, y, 80, y);
    }

    vga_setcolor(2);
    for (y = 75; y < 120; y++)
    {
        vga_drawline(130, y, 180, y);
    }

    vga_setcolor(1);
    for (y = 75; y < 120; y++)
    {
        vga_drawline(230, y, 280, y);
    }

    vga_getch();
    vga_setmode(TEXT);
    return 0;
}
```

Now, you may have noticed that I cheated; these squares aren’t perfectly square. However, if these squares are exactly 50 pixels wide by 50 pixels tall, they appear elongated, due to the distorting layout of screen mode 5. We can compensate for this by knocking five pixels off of the height of the squares (making them rectangles, in reality), and this makes them appear to be plumb. Figure 3.3 shows the grayscale version of what we just did.