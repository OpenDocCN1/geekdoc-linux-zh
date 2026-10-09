```
```c
char shift = 0;

unsigned char *c = text_color;
for(i=0; i<info->bytes_per_pixel; i++) {
    *c++ = (native_c0 & mask) >> shift;
    mask <<= BITS_PER_BYTE;
    shift += BITS_PER_BYTE;
}
```

```c
void l3d_rasterizer_3d_sw_imp::draw_text(int x, int y, const char *text) {
#define FONT_Y_SIZE 13
#define FONT_X_SIZE 8
#define FONT_SPACING 2

int i;
int font_y, font_x;
int x_offset;

x_offset = x * sinfo->bytes_per_pixel;
unsigned char *pix;

unsigned char *fg_color;

for(font_y=0; font_y < FONT_Y_SIZE; font_y++) {
    pix=sinfo->p_screeenBuf+(x_offset +
    SW_RAST_Y_REVERSAL(ysize,y + font_y)*xsize)
    *sinfo->bytes_per_pixel);

    unsigned int c;
    for(c=0; c<strlen(text); c++) {
        int current_bit;
        for(font_x=0, current_bit=0x80;
            font_x < FONT_X_SIZE;
            font_x++, current_bit >>= 1)
        {
            if(font_bitmaps[text[c]] [FONT_Y_SIZE-font_y] & current_bit) {
                fg_color = text_color;
                for(register int b=0; b<sinfo->bytes_per_pixel;b++) {
                    *pix++ = *fg_color++;
                }
            } else {
                pix += sinfo->bytes_per_pixel;
            }
        }

        for(font_x=0; font_x < FONT_SPACING; font_x++) {
            pix += sinfo->bytes_per_pixel;
        }
    }
}
```

```

Two other items deserve special mention in the texture mapping code. First, all of the real-valued variables are of type `l3d_fixed` instead of `l3d_real`. This means that we explicitly force the usage of fixed-point values within the texture mapping code. As with `l3d_real` values, we also use macros to multiply and divide `l3d_fixed` values; `fixfixmul` and `fixintmul` multiply a fixed point by another fixed-point or integer value; and `fixfixdiv` and `fixintdiv` divide a fixed-point value by another fixed-point or integer value. Addition and subtraction of `l3d_`