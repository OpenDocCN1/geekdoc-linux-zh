```
b = radius % 55;

if (((b > 5) && (b < 11)) || (b >= 50))
{
    a++;
}

for (i = 0; i < radius; i += a)
{
    gl_setpalettecolor(color, 63, j, j);
    book_fillcircle(xc, yc, (radius - i), color);
    color = (color + 1 < 64) ? color + 1 : color;
    j = (j + 1 <= 63) ? j + 1 : 63;
}
} else {
    gl_setpalettecolor(color, 63, j, j);
    book_fillcircle(xc, yc, radius, color);
    xc += (radius / 4);
    yc -= (radius / 4);
    radius *= .65;

    for (i = 0; i <= 63; i++)
    {
        gl_setpalettecolor(color, 63, j, j);
        book_fillcircle(xc, yc, (radius - i), color);
        color = (color + 1 < 64) ? color + 1 : color;
        j = (j + 1 <= 63) ? j + 1 : 63;
    }
}
}
```

# ## Antialiasing

Despite the long name, *antialiasing* is quite simple. Briefly, it refers to the process of "smoothing" rough edges on diagonal lines.

![](bbox=[0.125, 0.75, 0.435, 0.885])

**Figure 6.1**

Pseudo-sphere.