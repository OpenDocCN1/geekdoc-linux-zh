```
book_circle(200, 200, 100);

	a_vga_getch();
	a_vga_setmode(TEXT);

		return 0;
}

void book_circle(int xc, int yc, int radius)
{
	double theta,
		a_costheta,
		a_sintheta;

	int degrees;

	for (degrees = 0; degrees < 360; degrees++)
	{
		/* Define PI as 3.14, if your compiler doesn't accept
		the following line. */
		theta = (PI / 180) * degrees;
		costheta = cos(theta);
		a_sintheta = sin(theta);

		vga_drawpixel(xc + radius * costheta,
					a_yc + radius * sintheta);
	}
}

```

Listing 4.2 demonstrates a circle centered at point 200, 200, with a radius of 100 pixels. If the pixels of the circle were to extend beyond the borders of the screen matrix, SVGAlib would simply wrap them around to the other side. But, that doesn't happen in this case, because, as I said, the radius is only 100 pixels. What you end up with is a circle like the one shown in Figure 4.2.

![](bbox=[0.13, 0.76, 0.35, 0.9])

# **Figure 4.2**
Output of book_circle().