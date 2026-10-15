

gcc47 -Wall input_file.c -o output_file -lxcb

你也可以使用以下编译器命令：

```
gcc47 -Wall input_file.c -o output_file 'pkg_config -cflags -libs xcb'
```

## 22.4.2 示例 XCB 客户端应用程序

以下是三个基础的示例 XCB 程序。每个程序前面都有一个说明该程序功能的陈述。

### 22.4.2.1 XCB 示例程序 xcb_simple.c 目标：在屏幕上放置一个简单窗口。通过输入 xcb_simple & 启动它并注意发生了什么。

代码：

```c
#include <unistd.h> /* pause() */
#include <xcb/xcb.h>
int 
main ()
{
	xcb_connection_t *c;
	xcb_screen_t *screen;
	xcb_window_t win;

/* Initialization */

/* Open the connection to the X server */
c = xcb_connect (NULL, NULL);

/* Get the first screen */
screen = xcb_setup_roots_iterator (xcb_get_setup (c)).data;

/* Ask for our window's Id */
win = xcb_generate_id(c);

/* Create the window */
xcb_create_window (c,
XCB_COPY_FROM_PARENT,
win,
		screen->root,
		0, 0,
		250, 250,
		10,
		XCB_WINDOW_CLASS_INPUT_OUTPUT,
		screen->root_visual,
		0, NULL);

/* Connection */
xcb_flush (c);

/* depth (same as root) */
/* window Id */
/* parent window */
/* x, y */
/* width, height */
/* border_width */
/* class */
/* visual */
/* masks, not used yet */
```

```
/* Map the window on the screen */
xcb_map_window (c, win);

/* Make sure commands are sent before we pause, so window is shown */
xcb_flush (c);

pause ();   /* hold client */
/* Cleanup */
xcb_disconnect(c);
return 0;
}
```

# 练习 22.21

前述程序缺少 X Windows 客户端应用程序的一个基本组件，特别是该组件的哪个方面或部分？如何在不使用 KDE4 窗口管理器 kill 按钮的情况下关闭窗口？

### 22.4.4.2.2 XCB 示例程序 2ndxcbdraw.c 目标：在窗口中绘制一个矩形框

代码：

```
#include <stdlib.h>
#include <stdio.h>
#include <xcb/xcb.h>
int
main ()
{
    xcb_connection_t    *c;
    xcb_screen_t        *screen;
    xcb_drawable_t      win;
    xcb_gcontext_t      foreground;
    xcb_generic_event_t *e;
    uint32_t            mask = 0;
    uint32_t            values[2];

    /* geometric objects */
    xcb_rectangle_t     rectangles[] = {
        { 10, 50, 40, 20 },
        { 80, 50, 10, 40 }};

    /* Initialization */
    /* Open the connection to the X server */
    c = xcb_connect (NULL, NULL);
```

```
/* Get the first screen */
screen = xcb_setup_roots_iterator (xcb_get_setup (c)).data;

/* Create black (foreground) graphic context */
win = screen->root;

foreground = xcb_generate_id (c);
mask = XCB_GC_FOREGROUND | XCB_GC_GRAPHICS_EXPOSURES;
values[0] = screen->black_pixel;
values[1] = 0;
xcb_create_gc (c, foreground, win, mask, values);

/* Ask for our window's Id */
win = xcb_generate_id(c);

/* Create the window */
mask = XCB_CW_BACK_PIXEL | XCB_CW_EVENT_MASK;
values[0] = screen->white_pixel;
values[1] = XCB_EVENT_MASK_EXPOSURE;
xcb_create_window (
    c,
    XCB_COPY_FROM_PARENT,
    win,
    screen->root,
    0, 0,
    150, 150,
    10,
    XCB_WINDOW_CLASS_INPUT_OUTPUT,
    screen->root_visual,
    mask, values);

/* Map the window on the screen */
xcb_map_window (c, win);

/* Flush the request */
xcb_flush (c);

/* Start the Event-Request loop */
while ((e = xcb_wait_for_event (c))) {
    switch (e->response_type & ~0x80) {
    case XCB_EXPOSE: {
        /* Draw the rectangles */
        xcb_poly_rectangle (c, win, foreground, 2, rectangles);
        /* Flush the request */
        xcb_flush (c);
        break;
    }
    }
}
```

```
default: {
    /* Unknown event type, ignore it */
    break;
}
}
/* Free the Generic Event */
free (e);
}

/* Cleanup */
xcb_disconnect(c);
return 0;
}
```

### 22.4.4.2.3 XCB 示例程序 xcb_example.c 目标：在窗口中绘制一个矩形框

代码：

```
/* Simple XCB application drawing a box in a window */
/* to compile it use: gcc47 -Wall xcb_example.c -o xcb_example -lxcb */
*/
#include <xcb/xcb.h>
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
 xcb_connection_t    *c;
 xcb_screen_t        *s;
 xcb_window_t        w;
 xcb_gcontext_t      g;
 xcb_generic_event_t *e;
 uint32_t            mask;
 uint32_t            values[2];
 int                 done = 0;
 xcb_rectangle_t     r = { 30, 30, 70, 70 };

 /* Initialization*/

 /* open connection with the server */
 c = xcb_connect(NULL,NULL);
 if (xcb_connection_has_error(c)) {
  printf("Cannot open display\n");
  exit(1);
 }
 /* get the first screen */
 s = xcb_setup_roots_iterator (xcb_get_setup(c)).data;
