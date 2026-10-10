# **Listing 10.2  A sane method of drawing a repetitious shape.**

```
```
void book_example(int x, int y, int c)
{
  vga_setcolor(c);

  vga_drawline(x, y, x + 9, y);
  vga_drawline(x, y + 1, x + 9, y + 1);
  vga_drawline(x, y + 2, x + 9, y + 7);
  vga_drawline(x + 1, y + 2, x + 1, y + 7);
  vga_drawline(x + 8, y + 2, x + 8, y + 7);
  vga_drawline(x + 9, y + 2, x + 9, y + 7);
  vga_drawline(x, y + 8, x + 9, y + 8);
  vga_drawline(x, y + 9, x + 9, y + 9);
}
```
```

Using the method in Listing 10.2, you could very easily render a shape moving across the screen. My example can be found in Listing 10.3, sans the book_example() function. (I figure you can manage pasting that function in from Listing 10.2.)

# **Listing 10.3  A first stab at animation.**

```
```
#include <stdio.h>
#include <vga.h>

void book_example(int x, int y, int c);

int main(void)
{
  int x,
    y = 100,
    c,
    white;

  vga_init();
  vga_setmode(6320x200x256);

  white = vga_white();

  for (x = 300; x > 0; x--)
    {
      c = white;
      book_example(x, y, c);
      c = 0;
      vga_waitretrace();
      book_example(x, y, c);
    }
}
```
```