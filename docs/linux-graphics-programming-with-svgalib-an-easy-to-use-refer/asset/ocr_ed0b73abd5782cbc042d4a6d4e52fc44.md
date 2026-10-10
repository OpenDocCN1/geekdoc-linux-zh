```
```
)
else if ((x >= 9) && (x <28) && (y >250)) {
    /* we're in the left palette column */
    if ((y >= 250) && (y <= 269))
        /* color 0 */
        {
            color[19] = color[0];
            gl_fillbox(16, 426, 28, 28, color[19]);
        } else if ((y >= 271) && (y <= 290))
            /* color 2 */
            {
                color[19] = color[2];
                gl_fillbox(16, 426, 28, 28, color[19]);
            } else if ((y >= 292) && (y <= 311))
                /* color 4 */
                {
                    color[19] = color[4];
                    gl_fillbox(16, 426, 28, 28, color[19]);
                } else if ((y >= 313) && (y <= 332))
                    /* color 6 */
                    {
                        color[19] = color[6];
                        gl_fillbox(16, 426, 28, 28, color[19]);
                    } else if ((y >= 334) && (y <= 353))
                        /* color 8 */
                        {
                            color[19] = color[8];
                            gl_fillbox(16, 426, 28, 28, color[19]);
                        } else if ((y >= 355) && (y <= 374))
                            /* color 10 */
                            {
                                color[19] = color[10];
                                gl_fillbox(16, 426, 28, 28, color[19]);
                            } else if ((y >= 376) && (y <= 395))
                                /* color 12 */
                                {
                                    color[19] = color[12];
                                    gl_fillbox(16, 426, 28, 28, color[19]);
                                } else if ((y >= 397) && (y <= 416))
                                    /* color 14 */
                                    {
                                        color[19] = color[14];
                                        gl_fillbox(16, 426, 28, 28, color[19]);
                                    }
                        } else if ((x >= 30) && (x <49) && (y > 250)) {
                            /* we're in the right palette column */
```
```