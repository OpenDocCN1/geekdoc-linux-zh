```
```c
printf("Please specify an output file.\n");
exit(1);
}

/* You might want to check if the specified file already
   exists, and return an error if it does. */

file = fopen(argv[1], "w");
if (file == NULL)
{
    printf("Can't write to file.\n");
    exit(1);
}

/* Set all font strips to 0. */
for (a = 0; a < 256; a++)
{
    for (b = 0; b < 7; b++)
    {
        glyph[a][b] = 0;
    }
}

vga_init();
vga_setmode(G320x200x256);
g1_setcontextvga(G320x200x256);

/* This is the main loop. The program alternates between
   the "chooser screen" (the main menu) and the drawing
   screen. Pressing "Q" while in the chooser screen quits
   and saves your font info to your selected filename.
   */

do
{
    ascii = 0;
    chooser_screen();

    /* Spacebar - ASCII code 32. */
    if (inkey == 32)
    {
        draw_screen(ascii);
    }

    /* "Esc" - ASCII code 27.
       "Q"   - ASCII code 81. */
```
```