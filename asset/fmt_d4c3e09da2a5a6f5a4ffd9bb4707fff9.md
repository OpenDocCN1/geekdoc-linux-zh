
```c
/*************************************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter6_1.c                                   *
/************************************************************************/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <gd.h>
#include <gdfonts.h>
#include "c_in_linux.h"

int main(int argc, char *argv[], char *env[])
{
    int text=0,background=0,height=50,width=0;
    char value[255] = "";
    gdImagePtr im_out = NULL;

    decode_value("TEXT=", (char *) &value, 255);
    width = ( strlen(value) * 10 ) + 5;
    im_out = gdImageCreate(width,height);
    background = gdImageColorAllocate(im_out, 255,0,255);
    text  = gdImageColorAllocate(im_out,0,0,255);
    gdImageFilledRectangle(im_out, 0,0, width-1, height-1, background);
    gdImageString(im_out,gdFontGetSmall(),10,5,(unsigned char *)value,    text);
    printf("Content-type: image/gif\n\n");
    gdImageGif(im_out,stdout);
    gdImageDestroy(im_out);
    return 0;
}
```

当使用 `cgi-bin/gdgraph1?TEXT=DavidHaskins` 调用该程序时，会产生如下输出：

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_59_0.png)

虽然这并不是最花哨或最吸引人的练习，但它至少展示了生成图形输出的关键原理。使用 `GD` 库，你可以加载现有图像，并以 `GIF`、`JPEG`、`PNG`、`WBMP` 等多种格式生成图像，甚至可以创建 `动画 GIF`。

如果你使用过 `PHP` 开发工具，你会认出 `GD` 库函数，因为它们几乎完全相同，这表明在这种情况下 `PHP` 只是同一个 `C` 库的封装层。

这里显示的文本使用了内部字体之一，包括 `Tiny`、`Small`、`Medium Bold`、`Large` 和 `Giant`。这些字体足以满足简单的标签需求，但你也可以使用 `TrueType` 字体以获得更吸引人的输出。

可以使用线条或特定样式、填充和多边形（开放或封闭）以及圆形、圆弧进行几何绘图。需要牢记的主要一点是，图像的**左上角**是原点，对于学过数学的人来说，这可能显得反直觉——我从未发现为什么是这样，只能想象最早在这一领域从事工作的程序员恰好不熟悉我们通常认为原点 `x=0, y=0` 位于左下角的坐标系。

颜色以 0 到 255 范围内的 `RGB` 值指定，因此白色是 `255,255,255`，红色是 `255,0,0`。要确定细微的色调，请使用 `GNU GIMP` 等图形工具，它拥有取色器功能，帮助查明细微的 `RGB` 值。可以从一张图像的调色板中获取颜色，并在另一张图像中使用，请求的调色板中最接近的颜色将被使用，如果还有空间则会自动创建该颜色。

## 6.2 使用 `TrueType` 字体

在这个例子中，我们修改了之前的程序，使用 `TrueType` 字体生成标签。

```c
/*************************************************************
 * C Programming in Linux (c) David Haskins 2008 * chapter6_2.c
 ************************************************************/

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <gd.h>
#include <gdfonts.h>
#include "c_in_linux.h"

int main(int argc, char *argv[], char *env[]) {
    int text=0,background=0,height=50,width=0,x=0,y=0,size=30,string_rectangle[8];
    double angle=0.0;
    char value[255] = "";
    //OpenSuse TrueType Font
    char font[]=" /usr/share/fonts/truetype/DejaVuSans.ttf";
    //Ubuntu TrueType Font
    // char font[256] =
    "/usr/share/fonts/truetype/ttf-dejavu/DejaVuSans.ttf";
    char *err = NULL;
    gdImagePtr im_out = NULL;

    decode_value("TEXT=" ,(char *) &value, 255);
    //call gdImageStringFT with NULL image to obtain size
    err = gdImageStringFT(NULL,&string_rectangle[0],
        font,size,angle,0,0,value);

    x = string_rectangle[2]-string_rectangle[6] + 6;
    y = string_rectangle[3]-string_rectangle[7] + 6;
    // create an image big enough for the string plus a little space
    im_out = gdImageCreate(x,y);
    //allocate colours
    background = gdImageColorAllocate(im_out, 0,0,0);
    text    = gdImageColorAllocate(im_out,255,0,255);
    //get starting position
    x = 3 - string_rectangle[6];
    y = 3 - string_rectangle[7];
    //draw the string
    err = gdImageStringFT(im_out,&string_rectangle[0],
        text,font,size,angle,x,y,value);

    //output
    printf("Content-type: image/gif\n\n");
    gdImageGif(im_out,stdout);
    gdImageDestroy(im_out);

    return 0; }
```

我们像之前一样调用此程序 `cgi-bin/gdgraph1?TEXT=C+PROGRAMMING+IN+LINUX`

得到类似以下的输出，你很可能发现这是一种更实用的工具类型。你系统字体的位置和内容包括会因环境而异，但代码提供了一个示例：

- `OpenSuse` `/usr/share/fonts/truetype/*.ttf`

- `Ubuntu` `/usr/share/fonts/truetype/ttf-dejavu/*.ttf`

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_61_0.png)

要想熟练使用 `GD` 这样的库，你必须做好实验的准备，并花大量时间去理解函数参数，仔细查看位于以下地址的详细可用文档：

`[http://www.boutell.com/gd](http://www.boutell.com/gd)`

### 6.3 `GD` 函数参考

完整的详细文档集维护在：`[http://www.boutell.com/gd](http://www.boutell.com/gd)`

`GD` 包含了丰富的功能，支持各种类型的绘图和许多格式，以及 `TrueType` 字体和动画 `Gif` 图像。以下是按类别划分的函数列表：

**图像创建、销毁、加载和保存：**

```c
gdImageCreate(int sx, int sy)
gdImageCreateFromJpeg(FILE *in)
gdImageCreateFromPng(FILE *in)
gdImageCreateFromGif(FILE *in)
gdImageCreateFromGd(FILE *in)
gdImageCreateFromWBMP(FILE *in)
gdImageDestroy(gdImagePtr im)
```

```c
void gdImageJpeg(gdImagePtr im, FILE*out, int quality)
void gdImageGif(gdImagePtr im, FILE*out)
void gdImagePng(gdImagePtr im, FILE*out)
void gdImageWBMP(gdImagePtr im, int fg, FILE*out)
void gdImageGd(gdImagePtr im, FILE*out)
```

**绘图函数：**

```c
void gdImageSetPixel(gdImagePtr im, int x, int y, int color)
void gdImageLine(gdImagePtr im, int x1, int y1, int x2, int y2, int color)
void gdImageDashedLine(gdImagePtr im, int x1, int y1, int x2, int y2, int color)
void gdImagePolygon(gdImagePtr im, gdPointPtr point_s, int point_sTotal, int color)
void gdImageOpenPolygon(gdImagePtr im, gdPointPtr point_s, int point_sTotal, int color)
void gdImageRectangle(gdImagePtr im, int x1, int y1, int x2, int y2, int color)
void gdImageFilledPolygon(gdImagePtr im, gdPointPtr point_s, int point_sTotal, int color)
void gdImageFilledRectangle(gdImagePtr im, int x1, int y1, int x2, int y2, int color)
void gdImageArc(gdImagePtr im, int cx, int cy, int w, int h, int s, int e, int color)
void gdImageFilledArc(gdImagePtr im, int cx, int cy, int w, int h, int s, int e, int color, int style)
void gdImageFilledEllipse(gdImagePtr im, int cx, int cy, int w, int h, int color)
void gdImageFillToBorder(gdImagePtr im, int x, int y, int border, int color)
void gdImageFill(gdImagePtr im, int x, int y, int color)
void gdImageSetAntiAliased(gdImagePtr im, int c)
void gdImageSetAntiAliasedDontBlend(gdImagePtr im, int c)
void gdImageSetBrush(gdImagePtr im, gdImagePtr brush)
void gdImageSetTile(gdImagePtr im, gdImagePtr tile)
void gdImageSetStyle(gdImagePtr im, int *style, int styleLength)
void gdImageSetThickness(gdImagePtr im, int thickness)
void gdImageAlphaBlending(gdImagePtr im, int blending)
void gdImageSaveAlpha(gdImagePtr im, int saveFlag)
void gdImageSetClip(gdImagePtr im, int x1, int y1, int x2, int y2)
void gdImageGetClip(gdImagePtr im, int *x1P, int *y1P, int *x2P, int *y2P)
```

#### 查询函数：

```cpp
int gdImageAlpha(gdImagePtr im, int color)(MACRO)
int gdImageGetPixel(gdImagePtr im, int x, int y)
int gdImageBoundsSafe(gdImagePtr im, int x, int y)
int gdImageGreen(gdImagePtr im, int color)(MACRO)
int gdImageRed(gdImagePtr im, int color)(MACRO)
int gdImageSX(gdImagePtr im)(MACRO)
int gdImageSY(gdImagePtr im)(MACRO)
int gdImageTrueColor(im)(MACRO)
```

#### 文本处理函数：

```cpp
gdFontPtr gdFontGetSmall(void )
gdFontPtr gdFontGetLarge(void )
gdFontPtr gdFontGetMediumBold(void )
gdFontPtr gdFontGetGiant(void )
gdFontPtr gdFontGetTiny(void )
void gdImageChar(gdImagePtr im, gdFontPtr font, int x, int y, int c, int color)
void gdImageCharUp(gdImagePtr im, gdFontPtr font, int x, int y, int c, int color)
void gdImageString(gdImagePtr im, gdFontPtr font, int x, int y, unsigned char*s, int color)
void gdImageString16(gdImagePtr im, gdFontPtr font, int x, int y, unsigned short *s, int color)
void gdImageStringUp(gdImagePtr im, gdFontPtr font, int x, int y, unsigned char*s, int color)
void gdImageStringUp16(gdImagePtr im, gdFontPtr font, int x, int y, unsigned short*s, int color)
char *gdImageStringFT(gdImagePtr im, int *brect, int fg, char *fontname, double ptsize, double angle, int x, int y, char *string)
char *gdImageStringFTEx(gdImagePtr im, int *brect, int fg, char *fontname, double ptsize, double angle, int x, int y, gdFFString ExtraPtr strex)
char *gdImageStringFTCircle(gdImagePtr im, int cx, int cy, double radius, double textRadius, double fillPortion, char*font, double ptsize, char*top, char*bottom, int fgcolor)
char *gdImageStringTTF(gdImagePtr im, int *brect, int fg, char *fontname, double ptsize, double angle, int x, int y, char *string)
```

#### 颜色处理函数：
