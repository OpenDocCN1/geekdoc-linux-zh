```
gl_hline(x, (y + 1), (x + 1), 254);  /* line 2 */
gl_setpixel(x, (y + 2), 254);       /* line 3 */
gl_setpixel((x + 1), (y + 2), 255);
gl_setpixel((x + 2), (y + 2), 254);
gl_setpixel(x, (y + 3), 254);       /* line 4 */
gl_hline((x + 1), (y + 3), (x + 2), 255);
gl_setpixel((x + 3), (y + 3), 254);
gl_setpixel(x, (y + 4), 254);       /* line 5 */
gl_hline((x + 1), (y + 4), (x + 3), 255);
gl_setpixel((x + 4), (y + 4), 254);
gl_setpixel(x, (y + 5), 254);       /* line 6 */
gl_hline((x + 1), (y + 5), (x + 4), 255);
gl_setpixel((x + 5), (y + 5), 254);
gl_setpixel(x, (y + 6), 254);       /* line 7 */
gl_hline((x + 1), (y + 6), (x + 5), 255);
gl_setpixel((x + 6), (y + 6), 254);
gl_setpixel(x, (y + 7), 254);       /* line 8 */
gl_hline((x + 1), (y + 7), (x + 6), 255);
gl_setpixel((x + 7), (y + 7), 254);
gl_setpixel(x, (y + 8), 254);       /* line 9 */
gl_hline((x + 1), (y + 8), (x + 7), 255);
gl_setpixel((x + 8), (y + 8), 254);
gl_setpixel(x, (y + 9), 254);       /* line 10 */
gl_hline((x + 1), (y + 9), (x + 8), 255);
gl_setpixel((x + 9), (y + 9), 254);
gl_setpixel(x, (y + 10), 254);      /* line 11 */
gl_hline((x + 1), (y + 10), (x + 5), 255);
gl_hline((x + 6), (y + 10), (x + 10), 254);
gl_setpixel(x, (y + 11), 254);      /* line 12 */
gl_hline((x + 1), (y + 11), (x + 2), 255);
gl_setpixel((x + 3), (y + 11), 254);
gl_hline((x + 4), (y + 11), (x + 5), 255);
gl_setpixel((x + 6), (y + 11), 254);
gl_setpixel(x, (y + 12), 254);      /* line 13 */
gl_setpixel((x + 1), (y + 12), 255);
gl_setpixel((x + 2), (y + 12), 254);
gl_setpixel((x + 4), (y + 12), 254);
gl_hline((x + 5), (y + 12), (x + 6), 255);
gl_setpixel((x + 7), (y + 12), 254);
gl_hline(x, (y + 13), (x + 1), 254); /* line 14 */
gl_setpixel((x + 4), (y + 13), 254);
gl_hline((x + 5), (y + 13), (x + 6), 255);
gl_setpixel((x + 7), (y + 13), 254);
gl_setpixel(x, (y + 14), 254);      /* line 15 */
gl_setpixel((x + 5), (y + 14), 254);
gl_hline((x + 6), (y + 14), (x + 7), 255);
```