
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
    pix=sinfo->p_screenBuf+(x_offset +
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

Two other items deserve special mention in the texture mapping code. First, all of the real-valued variables are of type `l3d_fixed` instead of `l3d_real`. This means that we explicitly force the usage of fixed-point values within the texture mapping code. As with `l3d_real` values, we also use macros to multiply and divide `l3d_fixed` values; `fixfixmul` and `fixintmul` multiply a fixed point by another fixed-point or integer value; and `fixfixdiv` and `fixintdiv` divide a fixed-point value by another fixed-point or integer value. Addition and subtraction of `l3d_fixed` values, as with `l3d_real`, can be done with the normal C++ addition and subtraction operators.

The reason we use fixed-point values in the texture mapping code is speed. Fixed-point arithmetic represents real-valued numbers as integers (see the Appendix); therefore, the conversion from a fixed-point number to an integer is quite fast — it is simply a bit shift operation. On the other hand, converting a floating-point number to an integer is comparatively slow. This might seem trivial, but we must convert the real-valued (u, v) coordinates to integer texture map indices for every pixel. In the `l3d` library, for instance, simply changing from floating point to fixed point doubled the performance of the texture mapping code.

The other item of note is the use of the z_MULT_FACTOR and z_ADD_FACTOR constants in the code. Instead of computing 1/z, we compute z_MULT_FACTOR/(z + z_ADD_FACTOR). The 1/z values in camera space can be very small; for instance, if z is 1000, then 1/z is 0.001. The z_MULT_FACTOR has the effect of scaling the 1/z values to be slightly larger so that interpolation between the 1/z values occurs between larger values and is thus more accurate. The z_ADD_FACTOR has the effect of making all z values slightly smaller before computing 1/z. The idea is that because of the near z clipping plane, none of the z values will ever be smaller than a certain value. For instance, if the near z plane is at 5, then z will always be at least 5, meaning that 1/z is at most 1/5, or 0.2. Even with the z_MULT_FACTOR, there is still a certain range of larger 1/z values which never occur due to the near z clipping. The purpose of the z_ADD_FACTOR is to move the clipped z values slightly closer to the origin, so that the range of possible 1/z values is larger. These numerical range considerations are particularly important when using fixed-point arithmetic since numerical accuracy is always a troublesome problem — troublesome because we only have a fixed number of bits to store whole and fractional parts, and if our computations are carelessly formulated, the resulting values will require either more or less precision than we have, leading to incorrect results. Essentially, therefore, we use the z_MULT_FACTOR and z_ADD_FACTOR to scale our computations such that the results always lie within the fixed precision of our fixed point values.

The text drawing code in the software rasterizer relies on a table of bitmaps, containing one bitmap for each character, and the two overridden methods set_text_color and draw_text. The constructor for the rasterizer implementation creates the table of bitmaps in variable font_bitmaps. Each character is associated with an 8 by 13 bitmap, stored as a series of 13 bytes. Each bit in each byte of each character’s bitmap represents one pixel forming the shape of the character; a value of 1 for the bit means the pixel should be drawn to fill the shape of the character, while a value of 0 means the bit should not be drawn. The bits are interpreted such that the most-significant (leftmost) bit is the leftmost pixel to be displayed. Since each character is 8 pixels wide (an admittedly hard-coded assumption in the code), one byte represents the eight horizontal pixels belonging to each character’s bitmap.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_131_0.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_131_1.png)

**Figure 2-41**: The character bitmap for the character "0". Each horizontal line in the bitmap (left) is interpreted as a byte, where a 1 pixel represents bit value 1 and an unlit pixel represents bit value 0 (middle). The bits for each byte, represented in hex, are shown on the right, and are the actual values stored in the font bitmap array. We store one such bitmap for each possible character we want to draw (letters, numbers, punctuation, etc.).

We use the following methods to draw the text. Method `set_text_color` takes a red, green, and blue color specification in external format, converts the color to native internal screen format, then stores the color as a series of bytes in the array `text_color`. Then, method `draw_text` draws a given string using the previously set color. It takes each character in the string to be printed, finds the appropriate bitmap for the character by using its ASCII code, and, for each bit in the character’s bitmap with a value of 1, draws the color stored in `text_color` into the rasterizer buffer. Thus, the string is drawn character for character, pixel by pixel into the buffer.

# A Mesa/OpenGL 3D Rasterizer Implementation: `l3d_rasterizer_3d_mesa_imp`

Mesa can also draw texture mapped polygons for us. For a computer without hardware acceleration, there is no speed benefit to be gained by using Mesa instead of a custom software texture mapper, because Mesa must do exactly the same math. The picture looks quite different, though, with a 3D graphics card. In this case, Mesa simply forwards the request to draw a texture mapped polygon on to the hardware, which then draws the polygon at speeds impossible to achieve via software alone. Therefore, let’s now take a look at a Mesa/OpenGL 3D rasterizer implementation. As usual, the rasterizer implementation is chosen via a factory at the program start, and is plugged into the rasterizer interface. Application code need not be modified to use either software or hardware rasterizers.

### Listing 2-12: `ras3_mesa.h`

```c
#ifndef _RAS3_MESA_H
#define _RAS3_MESA_H
#include "../tool_os/memman.h"

#include <GL/glut.h>
#include "rast3.h"
#include "ras_mesa.h"

class l3d_rasterizer_3d_mesa_imp {
virtual public l3d_rasterizer_2d_mesa_imp,
virtual public l3d_rasterizer_3d_imp
{
    private:
        
        GLuint fontOffset;
        void make_raster_font(void);
        
    protected:
        
        void texture_setup(const l3d_polygon_3d_textured *p_poly);
        void ogl_texturing_between_glbegin_end
            (const l3d_polygon_3d_textured *p_poly);
        l3d_real ui_xs, ui_ys, ui_z, vi_xs, vi_ys, vi_z, zi_xs, zi_z,
                ui_y, vi_z;
        
        unsigned long text_color;
        
    public:
        
        l3d_rasterizer_3d_mesa_imp(int xs, int ys, l3d_screen_info *si);
        
        void draw_point(int x, int y, unsigned long col);
        void draw_line(int x0, int y0, int x1, int y1, unsigned long col);
        void draw_polygon_flatshaded(const l3d_polygon_2d_flatshaded *p_poly);
        
        void draw_polygon_textured(const l3d_polygon_3d_textured *p_poly);
        void draw_polygon_textured_lightmapped
                (const l3d_polygon_3d_textured_lightmapped *p_poly);
        
        void draw_text(int x, int y, const char *string);
        void set_text_color(int red, int green, int blue);
        
        void clear_buffer(void);
        
    };
```

```c
class l3d_rasterizer_3d_mesa_imp_factory :
        public l3d_rasterizer_3d_imp_factory {
    public:
        
        l3d_rasterizer_3d_imp *create(int xs, int ys, l3d_screen_info *si);
        
    };
```

```c
#endif
```

### Listing 2-13: `ras3_mesa.cc`

```c
#include "ras3_mesa.h"
#include <math.h>
#include "../tool_os/memman.h"

static const Glubyte period[] =
    {0x00, 0x00, 0x18, 0x18, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

static const Glubyte space[] =
    {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

static const Glubyte digits[][13] = {
    {0x0,0x0, 0x18,0x3C,0x66,0xC3, 0xC3,0xC3,0xC3,0x66,0x3C,0x18},
    {0x0,0x0, 0xFF,0xFF,0xC, 0xC,0xC, 0xC,0x7C,0x3C,0xC},
    {0x0,0x0, 0xFF,0xFF,0xC3,0x03,0x30,0x18,0xC,0x4C,0x0C,0x66,0x3C},
    {0x0,0x0, 0x7E,0xC3,0xC,0x6,0xC,0x38,0xC,0x6,0xC3,0xC,0x7E},
    {0x0,0x0, 0x6,0x6,0x6,0x6,0xFF,0xFF,0xC6,0xC6,0x66,0x36,0x1C},
    {0x0,0x0, 0x7E,0xFF,0xC3,0x3,0x3,0xFF,0xC,0x0,0xC0,0x0C,0x0C,0x7E},
    {0x0,0x0, 0x7E,0xFF,0xC3,0xC3,0xC3,0xFF,0xC,0x60,0x0,0xC0,0x7E},
```
