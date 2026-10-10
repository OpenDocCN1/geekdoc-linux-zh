

tview mainview;
int x, y, key, quit = 0, height = -1;
float angle = 0, speed = 0;

printf("Use the '+' and '-' keys to change speed\n");
printf("and the mouse to fly around.\n");
getchar();

CreateMaps();

vga_init();

vga_setmousesupport(1);
vga_setmode(6320x200x256);
gl_setcontextvga(6320x200x256);

MakePalette();

while (!quit) {
    mouse_update();
    x = mouse_getx();
    y = mouse_gety();

    angle += (float)(x - (RENDERWIDTH / 2)) / 1024.0f;
    height += ((RENDERHEIGHT / 2) - (int)(y))*16;

    if (height > 1000*256)
        height = 1000*256;

    if (height < ((int)heightmap[INDEX(mainview.cx,
        mainview.cy)] << 8))
        height = ((int)heightmap[INDEX(mainview.cx,
            mainview.cy)] << 8);

    mainview.z = height;

    if ((key = vga_getkey()) > 0)
    {
        switch (key)
        {
        case '+': speed += 1.0 / 4.0;
            if (speed > 16) speed = 16;
            break;
        case '-': speed -= 1.0 / 4.0;
            if (speed < 0) speed = 0;
            break;
        case 27:
            if ((key = vga_getkey()) == 0) quit = 1;
            break;
        }
    }

    SetRenderView(speed, angle, &mainview);

    DrawScreen(&mainview);

    vga_waitretrace();
    gl_putbox(0, 0, RENDERWIDTH, RENDERHEIGHT, vpage);
    memset(vpage, 0, RENDERWIDTH * RENDERHEIGHT);
}

vga_setmode(TEXT);

return 0;
}

/********************************************
SetRenderView - 根据移动速度和
移动角度分配视图值
********************************************/
void SetRenderView(float speed, float moveangle, tview *v)
{
v->cx += speed * cos(moveangle);
v->cy += speed * sin(moveangle);

v->angle = moveangle;
}

/********************************************
DrawScreen - 给定一个视图结构，将屏幕渲染到
虚拟缓冲区
********************************************/
void DrawScreen(tview *v)
{
int i_x;
float angle;
float target_x, target_y;

for (i_x = 0; i_x < RENDERWIDTH; i_x++)
{
angle = FIELD_OF_VIEW * ((float)i_x /
(float)(RENDERWIDTH - 1)) - (FIELD_OF_VIEW / 2);
target_x = v->cx + FARDEPTH *
cos(v->angle + DEG2RAD(angle));
target_y = v->cy + FARDEPTH *
sin(v->angle + DEG2RAD(angle));

Casteray(v->cx, v->cy, target_x, target_y,
(v->z+(20<<8))<<8, i_x);
}
/*
*
* Casteray - 向景观投射光线并绘制
* 高度条
*
*/
void Casteray(float x1, float y1, float x2, float y2,
int viewer, int scr_x)
{
int c0,c1,c2,c3,c1l,c22;
/* 用于双线性插值的变量 */
int fxdx, fxddx;
int fxddy, fxdoy;
int miny;
int depth;
int per;
int start_h, start_c;
int end_h, end_c;
int scryl, scry2;
int i_c, i_dc;
int i_y;
/* 将遍历变量存储为 16.16 定点数 */
fxdx = FLT2FXD(x1);
fxdy = FLT2FXD(y1);

txd_dx = FLT2FXD((x2 - x1) / FARDEPTH);
fxd_dy = FLT2FXD((y2 - y1) / FARDEPTH);
miny = RENDERHEIGHT;

/* 创建起始高度和颜色 */
start_h = 199;
BLEND(colormap, fxdx, fxdy, start_c);
for (depth = 1; depth < FARDEPTH; depth++)
{
per = (HEIGHTMUL << 16) / depth;
/* 计算地图空间中的颜色和高度 */
BLEND(heightmap, fxd_x, fxd_y, end_h);
BLEND(colormap, fxd_x, fxd_y, end_c);
/* 将高度转换为屏幕空间 */
end_h = (RENDERHEIGHT / 2) -
       ((long long)(end_h - viewer) * per) >> 32);
/* 仅当新高度小于
   旧高度时才绘制 */
if (end_h < start_h)
{
    /* 仅当新高度小于
       最小达到高度时才绘制 */
    if (end_h < miny)
    {
        scr_y1 = end_h;
        scr_y2 = miny - 1;
        i_c = end_c;
        i_dc = (start_c - end_c) / (start_h - end_h);
        miny = end_h; /* 将最小 y 值重置为
                         新的最高值 */
    }
    if (scr_y1 < 0)  /* 执行一些裁剪，以免
                       超出屏幕顶部 */
    {
        i_c += i_dc * (-scr_y1);
        scr_y1 = 0;
    }
    scr_y1 -= ((int)(vpage) + scr_y1 * RENDERWIDTH + scr_x);
    scr_y2 = ((int)(vpage) + scr_y2 * RENDERWIDTH + scr_x);
    for (i_y = scr_y1; i_y <= scr_y2;
         i_y += RENDERWIDTH, i_c += i_dc)
        *(char *) (i_y = i_c >> 16);
}
fxd_x += fxd_dx;
fxd_y += fxd_dy;
start_h = end_h;
start_c = end_c;
}
}

/*-------------------------------
MakePalette - 创建从深红色到红色的沙色调色板
*-------------------------------*/
void MakePalette()
{
int i;

for (i = 1; i < 64; i++)
{
gl_setpalettecolor(i, 16 + (i/4), i/8, 0);
}

for (i = 64; i < 128; i++)
{
gl_setpalettecolor(i, 32 + ((i-64)/2), i/8, 0);
}

/* gl_setpalettecolor(255, 63, 63, 63); */
}

/*-------------------------------
CreateMaps - 计算高度图和颜色图。分配绘制缓冲区
*-------------------------------*/
void CreateMaps()
{
int i;

srand(getpid());

/* 初始化部分内存 */
memset(heightmap, 0, MAPSIZE*MAPSIZE);
memset(vpage, 0, RENDERWIDTH * RENDERHEIGHT);

printf("Creating %dx%d fractal terrain\n", MAPSIZE, MAPSIZE);
heightmap[0] = (rand() % 128) % 64;
/* 初始化地图上的起始点 */
CreateFractalMap(0, 0, MAPSIZE, MAPSIZE);

printf("Smooting terrain\n");
for (i = 0; i < 5; i++)
SmoothMap();

MakeColorMap();
}

/*------------------------------------------------------------*
* CreateFractalMap - 构建分形景观
------------------------------------------------------------*/
void CreateFractalMap(int x1, int y1, int x2, int y2)
{
int x, y, c;

if (((x2-x1) < 2) && ((y2-y1) < 2))
return;

x = (x1 + x2) >> 1;
y = (y1 + y2) >> 1;

NewColor(x1, y1, x, y1, x2, y1);
NewColor(x2, y1, x2, y, x2, y2);
NewColor(x1, y2, x, y, x2, y2);
NewColor(x1, y1, x1, y, x1, y2);

c = (heightmap[INDEX(x1,y1)] + heightmap[INDEX(x1,y2)] +
heightmap[INDEX(x2,y1)] + heightmap[INDEX(x2,y2)]) >> 2;

if (heightmap[INDEX(x, y)] == 0)
heightmap[INDEX(x, y)] = c;

CreateFractalMap(x1, y1, x, y);
CreateFractalMap(x, y1, x2, y2);
CreateFractalMap(x, y, x2, y2);
CreateFractalMap(x1, y, x, y2);
}

/*------------------------------------------------------------*/
* NewColor - 新颜色评估
* (分形景观函数)
------------------------------------------------------------*/
void NewColor(int xa, int ya, int x, int y, int xb, int yb)
{
int color;

color = abs(xa - xb) + abs(ya - yb);
color = RANDOM(color << 1) - color;
color = color + ((heightmap[INDEX(xa, ya)] +
		heightmap[INDEX(xb, yb)] + 1) >> 1);

if (color < 1)	color = 1;
if (color > 255) color = 255;

if (heightmap[INDEX(x, y)] == 0)
	heightmap[INDEX(x, y)] = color;
}

/*-----------------------------------------
SmoothMap - 通过 3x3 箱式滤波器平滑景观
-----------------------------------------------*/
void SmoothMap()
{
	int x,y;

	for (x = 0; x < MAPSIZE; x++)
		for (y = 0; y < MAPSIZE; y++)
		heightmap[INDEX(x,y)] = (heightmap[INDEX(x-1,(y-1))] +
				heightmap[INDEX(x-1),(y+1)] +
				heightmap[INDEX(x+1),(y-1)] +
				heightmap[INDEX(x+1),(y+1)] +
				heightmap[INDEX(x,			(y-1)] +
				heightmap[INDEX(x,		(y+1)] +
				heightmap[INDEX(x-1, y		)] +
				heightmap[INDEX( x,		 y		)] +
				heightmap[INDEX(x+1, y)]) / 9;
}

/*-----------------------------------------
MakeColorMap - 尝试为景观构建一个富有创意的颜色图
--------------------------------------------*/
void MakeColorMap()
{
	int x,y,temp;

	for (x = 0; x < MAPSIZE; x++)
		for (y = 0; y < MAPSIZE; y++)
		{
			temp = heightmap[INDEX(x,y)] >> 1;
			if (heightmap[INDEX(x-1),y] > heightmap[INDEX(x,y)])
			{
				temp -= 8*(heightmap[INDEX(x,y)] -
					heightmap[INDEX(x-1),y]));

if (temp < 2)
	temp = 2;
}
else
{
	if (heightmap[INDEX((x-1),y)] >
		heightmap[INDEX(x,y)])
	{
		temp += 3*(heightmap[INDEX((x-1),y)]
			- heightmap[INDEX(x,y)]);
		if (temp > 127)
			temp = 127;
	}
}
colormap[INDEX(x,y)] = temp;
}
}

![](img/2e475714ef8969ed272622c46473d334_344_0.png)

**图 16.12**
亚历克斯·查尔芬的光线投射高度场引擎。

### 使用 ppmforge

还有另一个程序可以帮助你绘制云朵、星空，甚至行星。它被称为*ppmforge*，是**netpbm** 软件包的扩展，该包在其他章节中有所提及（换句话说，你需要**netpbm**来编译*ppmforge*）。自然，我已将其包含在随附的光盘中。

像下面这样的简单命令将创建一个包含图像数据的 PPM 文件：

```
ppmforge -clouds > outfile
```

接下来，使用**ppmtogif**（它是**netpbm**的一部分）将你的 PPM 文件转换为标准的 GIF 图像。

有若干命令行选项可供使用，以帮助你自定义生成的图像，这些命令在手册页中有详细文档说明。*ppmforge* 生成的示例图像如图 16.13 所示。

