
为了允许用户处理现有的图像，我添加了一些`liblug`的读写例程。就目前而言，传入的图形文件必须在命令行中指定。然而，当用户界面完成后，它们也将可以通过下拉菜单访问。

不幸的是，这意味着由于图像文件可以包含16、256或更多颜色，因此需要一些编程上的变通方法。如果图形文件中的颜色与您所选屏幕等级中可用的颜色不匹配，你很可能会看到一些损坏和失真。沿同样的思路，许多图形文件包含它们自己的调色板，这通常会与你的屏幕调色板发生冲突。为了规避这种情况，我采取了以下预防措施：

1. 如果图像的颜色超过256种，它将被量化（缩减）为256种颜色。
2. 然后，屏幕将设置为256色模式，并且调色板将设置为与传入图形的调色板匹配。
3. 图像将显示，随后其颜色信息将被记录到一个数组中。
4. 最后，屏幕将重置为允许32K种颜色，并绘制正常的背景 и 工具栏。然后，通过读取第3步创建的数组来重新创建图像。

为了防止图像在屏幕上瞬间闪烁（在使用256种颜色时），我采用了两个新函数：`vga_screenoff()`和`vga_screenon()`。它们的作用正如它们听起来那样——第一个将屏幕变黑，第二个恢复屏幕。不会丢失任何图像数据。由于屏幕最初是黑色的，用户甚至不应该注意到正在发生的事情。

最后，为了保持井井有条，我将所有屏幕准备命令移动到一个自己的函数中，`prep_screen()`。这就是绘制菜单等的地方。

列表18.8展示了基本的`liblug`部分。请记住，你需要将：

```c
int main(void)
```

更改为更复杂的：

```c
int main(int argc, char *argv[])
```

以接受命令行变量。

### 列表 18.8 读取文件

```c
if (argc > 1)
{
    if ((a = read_lug_file(argv[1], &file)) == 0)
    {
        int c[file.xsize * file.ysize];
        int palr[256], palg[256], palb[256];
        byte *ptr;

        if (file.colors > 256)
        {
            quantize(&file, &quantfile, 256);
            copy_bitmap(&quantfile, &file);
            free_bitmap(&quantfile);
        }

        vga_setmode(G640x480x256);
        gl_setcontextvga(G640x480x256);
        vga_screenoff();

        a = 0;
        for (i = 0, ptr = file.cmap; i < file.colors; i++)
        {
            r = (double)*ptr++;
            palr[a] = r;
            g = (double)*ptr++;
            palg[a] = g;
            b = (double)*ptr++;
            palb[a] = b;
            gl_setpalettecolor(r, r>>2, g>>2, b>>2);
            a++;
        }

        gl_putbox(0, 0, file.xsize, file.ysize, file.r);

        a = 0;
        for (i = 0; i < file.ysize; i++)
        {
            for (j = 0; j < file.xsize; j++)
            {
                c[a] = vga_getpixel(j, i);
                a++;
            }
        }

        vga_setmouseesupport(1);
        vga_setmode(6640x480x32K);
        gl_setcontextvga(6640x480x32K);
        vga_screenon();

        prep_screen();

        a = 0;
        for (i = 0; i < file.ysize; i++)
        {
            for (j = 0; j < file.xsize; j++)
            {
                gl_setpixelrgb(LEFT + j, TOP + i, palr[c[a]],
                               palg[c[a]], palb[c[a]]);
                a++;
            }
        }
    } else {
        exit(1);
    }
} else {
    vga_setmouseesupport(1);
    vga_setmode(6640x480x32K);
    gl_setcontextvga(6640x480x32K);
    prep_screen();
}
```

# 完整代码

此时，你已经拥有一个可用的界面和一些可用的工具。下一步将是创建下拉菜单。由于菜单是任何GUI的固有元素，我决定在第19章中对该主题进行完整讲解。

矩形和圆形例程可以或多或少地从直线函数中复制。剩下的就是泛洪填充，我将留给你去弄清楚。你可能会发现采用另一种但相似的变体更容易，即改变特定颜色的每个像素，无论它接触什么。

现在，我将本章的完整代码留给你。列表18.9包含了我迄今为止讨论的所有内容，以及更多内容。同样，菜单将在下一章中编码。如果你决定创建自己的绘图工具，我为你留出了充足的空间。

### 列表 18.9 （或多或少）完整的绘图程序

```c
#include <stdlib.h>
#include <math.h>
#include <unistd.h>
#include <lug.h>
#include <lugfnts.h>
#include <vga.h>
#include <vgagl.h>
#include <vgamouse.h>

/* parameters of drawing window */
#define LEFT      62
#define RIGHT     617
#define TOP        27
#define BOTTOM    457
#define BOX_WIDTH  555
#define BOX_HEIGHT 430

void move_cursor(int x, int y, int ox, int oy);
void draw_cursor(int x, int y);

void tool10_up();
void tool10_down();
void tool11_up();
void tool11_down();
void tool12_up();
void tool12_down();
void tool13_up();
void tool13_down();
void tool14_up();
void tool14_down();
void tool15_up();
```
