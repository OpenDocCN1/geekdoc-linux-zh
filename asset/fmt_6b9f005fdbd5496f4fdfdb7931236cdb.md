
```c
"outline_color", "black",

NULL);
```

44
45 `gtk_widget_show_all(app);`
46 `gtk_main();`
47 `exit(0);`
48 }
49 
50 `GnomeCanvasPoints *makeArrow(gint h, gint v,`
                    `gint h_off, gint v_off)` {
51     `int i;`
52     `GnomeCanvasPoints *points;`
53     `static const gint xy[16] = (`
54         `2.0, 0.2, 1.2, 1.4, 3.4, 3.2, 4.2, 2.0`
     `);`
56 
57     `points = gnome_canvas_points_new(8);`
58     `for(i=0; i<16; i += 2) {`
59         `points->coords[i] = (xy[i] * h) + h_off;`
60         `points->coords[i+1] = (xy[i+1] * v) + v_off;`
61     `}`
62     `return(points);`
63 }
64 
65 `gint eventDelete(GtkWidget *widget,`
66                `GdkEvent *event, gpointer data)` {
67     `return(FALSE);`
68 }
69 `gint eventDestroy(GtkWidget *widget,`
70                `GdkEvent *event, gpointer data)` {
71     `gtk_main_quit();`
72     `return(0);`
73 }

从第 50 行开始的 `makeArrow()` 函数创建了用于创建该项目的 `GnomeCanvasPoints` 对象。`h` 和 `v` 参数是像素计数值，它们决定了箭头的大小。`h_off` 和 `v_off` 参数被加到每个点上，从而决定了箭头在画布中的位置。定义在第 54 行的 `xy` 数组以“单位”形式包含点列表——也就是说，数组中的每个值都乘以 `h` 和 `v` 参数，以调整图形每个部分的大小。

箭头总共由 8 个点组成，因此 `xy` 数组有 16 个条目。偶数下标的条目是 x 轴坐标，奇数下标的条目是 y 轴坐标。这种组织方式与 `GnomeCanvasPoints` 对象内部坐标点的组织方式一致，因此很容易在两者之间进行转换。`GnomeCanvasPoints` 对象在第 58 行创建，计算箭头坐标的循环从第 59 行开始。第 60 行和第 61 行通过用该点每个单位所代表的像素数乘以该点的“单位”值来计算实际的点位置；然后加上偏移量以将该点移动到请求的位置。

第 38 行通过调用 `gnome_canvas_item_new()` 创建多边形项目。调用 `makeArrow()` 函数以返回指向 `GnomeCanvasPoints` 对象的指针。由于所有点都已按比例缩放并正确放置，剩下的工作就是为多边形着色，这在第 41 行和第 42 行完成。结果如图 9-11 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_312_0.png)

## 画布仿射变换

*仿射变换*可用于移动、缩放、旋转或以其他方式操纵显示的项目。以下示例创建三个箭头，并对其中每一个应用仿射变换。本示例仅演示了如何在画布项目上使用仿射变换的基本方法。

如果你不熟悉仿射变换，它们可能看起来神秘且近乎魔法。仿射变换用于调整大小、翻转、旋转、反转、拉伸、倾斜或缩小图形对象。并且有方法可以将一组仿射变换组合起来，以便在单步中执行一系列操作。

```c
/** canvaffine.c **/

#include <gnome.h>

gint eventDelete(GtkWidget *widget,

    GdkEvent *event, gpointer data);

gint eventDestroy(GtkWidget *widget,

    GdkEvent *event, gpointer data);

GnomeCanvasPoints *makeOriginArrow(gint h, gint v);

#define HORIZ 30

#define VERT 30

#define WIDTH (HORIZ * 6)

#define HEIGHT (VERT * 6)

int main(int argc, char *argv[])

{

    GtkWidget *app;

    GtkWidget *canvas;

    GnomeCanvasGroup *rootGroup;

    GnomeCanvasItem *item;

    double affine[6];

    gnome_init("canvasaffine", "1.0", argc, argv);

    app = gnome_app_new("canvasaffine",

        "Canvas Affine");

    gtk_signal_connect(GTK_OBJECT(app), "delete_event",

        GTK_SIGNAL_FUNC(eventDelete), NULL);

    gtk_signal_connect(GTK_OBJECT(app), "destroy",

        GTK_SIGNAL_FUNC(eventDestroy), NULL);

    canvas = gnome_canvas_new();

    gtk_widget_set_usize(canvas, WIDTH, HEIGHT);

    gnome_canvas_set_scroll_region(GNOME_CANVAS(canvas),

        -WIDTH/2, -HEIGHT/2, WIDTH/2, HEIGHT/2);

    rootGroup = gnome_canvas_root(GNOME_CANVAS(canvas));

    gnome_app_set_contents(GNOME_APP(app), canvas);

    item = gnome_canvas_item_new(rootGroup,

        gnome_canvas_polygon_get_type(),

        "points", makeOriginArrow(HORIZ, VERT),

        "fill_color", "white",

        "outline_color", "black",

        NULL);

    art_affine_scale(affine, 1.3, 1.3);

    gnome_canvas_item_affine_relative(item, affine);

    item = gnome_canvas_item_new(rootGroup,

        gnome_canvas_polygon_get_type(),

        "points", makeOriginArrow(HORIZ/2, VERT/2),

        "fill_color", "black",

        "outline_color", "white",

        NULL);

    art_affine_rotate(affine, 45.0);

    gnome_canvas_item_affine_relative(item, affine);

    item = gnome_canvas_item_new(rootGroup,

        gnome_canvas_polygon_get_type(),

        "points", makeOriginArrow(HORIZ/2, VERT/2),

        "fill_color", "green",

        "outline_color", "black",

        NULL);

    art_affine_translate(affine, 60., -50);

    gnome_canvas_item_affine_relative(item, affine);

    gtk_widget_show_all(app);

    gtk_main();

    exit(0);

}
```
