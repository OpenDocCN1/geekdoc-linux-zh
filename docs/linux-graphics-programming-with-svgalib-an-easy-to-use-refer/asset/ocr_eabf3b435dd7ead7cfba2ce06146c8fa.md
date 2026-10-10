```
```cpp
    16, g);
glSetFont(FONT_WIDTH, FONT_HEIGHT, fontw);
gl_write((FILE_MENU_LEFT + 15),
    (FILE_MENU_TOP + 4), "Open\0");
gl_getbox(x, y, 11, 19, mouse_box);
draw_cursor(x, y);
} else if (y > (FILE_MENU_TOP + 17) &&
    (y <= (FILE_MENU_TOP + 31)) &&
    choice != 2) {
    choice = 2;
    gl_putbox(x, y, 11, 19, mouse_box);

gl_fillbox((FILE_MENU_LEFT + 1),
    (FILE_MENU_TOP + 1),
    (FILE_MENU_RIGHT - FILE_MENU_LEFT - 1),
    (FILE_MENU_BOTTOM - FILE_MENU_TOP - 1),
    w);
glSetFont(FONT_WIDTH, FONT_HEIGHT, fontb);
gl_write((FILE_MENU_LEFT + 15),
    (FILE_MENU_TOP + 4), "Open\0");
gl_write((FILE_MENU_LEFT + 15),
    (FILE_MENU_TOP + 34), "Save\0");
gl_write((FILE_MENU_LEFT + 15),
    (FILE_MENU_TOP + 49), "Close\0");
gl_hline((FILE_MENU_LEFT + 1),
    (FILE_MENU_TOP + 62),
    (FILE_MENU_RIGHT - 1), b);
gl_write((FILE_MENU_LEFT + 15),
    (FILE_MENU_TOP + 66), "Exit\0");

glSetFont(FONT_WIDTH, FONT_HEIGHT, fontw);
gl_fillbox((FILE_MENU_LEFT + 1),
    (FILE_MENU_TOP + 16),
    (FILE_MENU_RIGHT - FILE_MENU_LEFT - 1),
    16, g);
gl_write((FILE_MENU_LEFT + 15),
    (FILE_MENU_TOP + 19), "Save As\0");
gl_getbox(x, y, 11, 19, mouse_box);
draw_cursor(x, y);
} else if (y >=(FILE_MENU_TOP + 32) &&
    (y <= (FILE_MENU_TOP + 46)) &&
    choice != 3) {
    choice = 3;
    gl_putbox(x, y, 11, 19, mouse_box);

gl_fillbox((FILE_MENU_LEFT + 1),
```
```