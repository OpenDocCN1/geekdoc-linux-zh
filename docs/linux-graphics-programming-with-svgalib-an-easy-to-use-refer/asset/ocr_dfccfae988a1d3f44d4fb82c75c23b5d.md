```
```
(
    gl_fillbox(204, y, 22, 18, 3);
    b -= 2;
    pos[p + 6] = 1;
} else {
    gl_fillbox(204, y, 22, 18, 15);
    pos[p + 6] = 0;
}

if (b > 0)
{
    gl_fillbox(228, y, 22, 18, 3);
    pos[p + 7] = 1;
} else {
    gl_fillbox(228, y, 22, 18, 15);
    pos[p + 7] = 0;
}
if (p != 55)
{
    p += 8;
}

vga_setcolor(14);
hol1ow_box(x1, y1, x2, y2);
gl_write(58, 175, "This character is:\0");
gl_write(218, 175, c);
init_chooser_font(3);
gl_write(0, 185, "space to select, 'q' to return to menu \0");

do
{

    inkey = vga_getch();
if (inkey == 97)
/* "a" */
{
    vga_setcolor(7);
    hol1ow_box(x1, y1, x2, y2);
if (x1 != 59)
{
    x1 -= 24;
    x2 -= 24;
} else {
    x1 = 227;
    x2 = 250;
}

    vga_setcolor(14);
    hol1ow_box(x1, y1, x2, y2);
```