Once the tools have been created, they need to be checked to see whether they’re being used. I accomplish this with a switch() statement, as shown in Listing 18.6. If the left mouse button has been pressed, and you’re in the drawing window, then switch() will determine which tool function to call. If you’re on the left side of the screen, the code checks to see whether you’re above a tool button or a palette choice.

# **Listing 18.6  What to do when a mouse button is pressed.**

```
```
if (button & MOUSE_LEFTBUTTON)
{
	if ((x >= LEFT) && (x <= RIGHT)
		&& (y >= TOP) && (y <= BOTTOM))
	/* we're in the drawing area */
	{
		switch(tool)
		{
			case 1:
				line(x, y, color[19]);
				break;
			case 2:
				rectangle(x, y, color[19]);
				break;
			case 3:
				circle(x, y, color[19]);
				break;
			case 4:
				/* eyedropper */
				vga_waitrettrace();
				g1_putbox(x, y, 11, 19, box);
				g1_getpixelrgb(x, y, &r, &g, &b);
				draw_cursor(x, y);
				color[19] = g1_rgbcolor(r, g, b);
				g1_fillbox(16, 426, 28, 28, color[19]);
				break;
			case 5:
				flood_fill(x, y, color[19]);
				break;
			default:
				freehand(x, y, color[19]);
		}
	}
}
```
```

Five of the six tools are external functions, whereas the “eyedropper” (which can make any color in the drawing window the current color) is simple enough that I handled it right there. Make sure you remove the mouse cursor before you read the color value; otherwise, you’ll read the mouse and not the screen.