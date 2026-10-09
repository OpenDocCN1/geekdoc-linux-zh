

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

纹理映射代码中有另外两个项目值得一提。首先，所有实数变量均为 `l3d_fixed` 类型，而非 `l3d_real`。这意味着我们在纹理映射代码中显式强制使用定点数值。与 `l3d_real` 值类似，我们也使用宏来乘法和除法 `l3d_fixed` 值；`fixfixmul` 和 `fixintmul` 将定点数分别乘以另一个定点数或整数；而 `fixfixdiv` 和 `fixintdiv` 则用另一个定点数或整数除以定点数。`l3d_fixed` 值的加法和减法，与 `l3d_real` 一样，可以使用标准的 C++ 加法和减法运算符执行。

我们在纹理映射代码中使用定点值的原因是速度。定点算术用整数表示实数值（参见附录）；因此，将定点数转换为整数非常快——它只是一个位移位操作。另一方面，将浮点数转换为整数相比之下要慢得多。这看似微不足道，但我们必须将实数的 (u, v) 坐标转换为整数纹理映射索引，针对每个像素都要进行此操作。例如，在 `l3d` 库中，仅仅将浮点改为定点，纹理映射代码的性能就提高了一倍。

另一个值得注意的是代码中使用了 z_MULT_FACTOR 和 z_ADD_FACTOR 常量。我们不是计算 1/z，而是计算 z_MULT_FACTOR/(z + z_ADD_FACTOR)。摄像机空间中的 1/z 值可能非常小；例如，如果 z 是 1000，则 1/z 是 0.001。z_MULT_FACTOR 的作用是将 1/z 值放大得稍大一些，以便在 1/z 值之间进行插值时发生在较大的数值范围内，从而更加准确。z_ADD_FACTOR 的作用是在计算 1/z 之前使所有 z 值略微变小。其想法是，由于存在近处 z 裁剪平面，z 值永远不会小于某个特定值。例如，如果近 z 平面位于 5，则 z 始终至少为 5，这意味着 1/z 最多为 1/5，即 0.2。即使使用了 z_MULT_FACTOR，仍然有一系列较大的 1/z 值由于近 z 裁剪而不会发生。z_ADD_FACTOR 的目的是将裁剪后的 z 值稍微向原点移动，以使可能的 1/z 值范围更大。这些数值范围考虑在使用定点算术时尤为重要，因为数值准确性始终是一个棘手的问题——棘手在于我们只有固定的位数来存储整数部分和小数部分，如果我们的计算构建不当，结果所需的精度可能会超出或低于我们拥有的精度，从而导致错误的结果。因此，本质上，我们使用 z_MULT_FACTOR 和 z_ADD_FACTOR 来缩放我们的计算，使得结果始终位于定点数的固定精度范围内。

软件光栅化器中的文本绘制代码依赖于一个位图表，其中包含每个字符的一个位图，以及两个被重写的方法 set_text_color 和 draw_text。光栅化器实现的构造函数在变量 font_bitmaps 中创建位图表。每个字符与一个 8x13 的位图相关联，存储为 13 个字节的一系列数据。每个字符位图中每个字节的每个位代表构成字符形状的一个像素；位值为 1 意味着应该绘制该像素以填充字符形状，而值为 0 意味着不应绘制该位。位的解释方式是，最高有效位（最左边）是所要显示的最左边像素。由于每个字符宽度为 8 像素（代码中承认这是一个硬编码的假设），一个字节代表属于每个字符位图的八个水平像素。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_131_0.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_131_1.png)

**图 2-41**：字符 "0" 的字符位图。位图（左）中的每个水平行被解释为一个字节，其中像素 1 代表位值 1，未点亮的像素代表位值 0（中）。每个字节以十六进制表示的位在右侧显示，并且是存储在字体位图数组中的实际值。我们为想要绘制的每个可能字符（字母、数字、标点符号等）存储这样一个位图。

我们使用以下方法绘制文本。方法 `set_text_color` 接收外部格式的红、绿、蓝颜色规格，将颜色转换为本地内部屏幕格式，然后将颜色作为一系列字节存储在数组 `text_color` 中。然后，方法 `draw_text` 使用先前设置的颜色绘制给定的字符串。它获取要打印的字符串中的每个字符，通过其 ASCII 码找到该字符的相应位图，并且对于字符位图中值为 1 的每个位，将存储在 `text_color` 中的颜色绘制到光栅化器缓冲区中。因此，字符串是逐字符、逐像素地绘制到缓冲区中的。

# 一个 Mesa/OpenGL 3D 光栅化器实现：`l3d_rasterizer_3d_mesa_imp`

Mesa 也可以为我们绘制纹理映射的多边形。对于没有硬件加速的计算机，使用 Mesa 而不是自定义软件纹理映射器并没有速度上的优势，因为 Mesa 必须执行完全相同的数学运算。然而，使用 3D 显卡时，画面看起来会有所不同。在这种情况下，Mesa 只是将绘制纹理映射多边形的请求转发给硬件，然后硬件以软件无法达到的速度绘制多边形。因此，让我们现在来看一下一个 Mesa/OpenGL 3D 光栅化器实现。通常，光栅化器实现在程序开始时通过工厂选择，并插入到光栅化器接口中。应用程序代码无需修改即可使用软件或硬件光栅化器。

### 列表 2-12：`ras3_mesa.h`

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

### 列表 2-13：`ras3_mesa.cc`

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

