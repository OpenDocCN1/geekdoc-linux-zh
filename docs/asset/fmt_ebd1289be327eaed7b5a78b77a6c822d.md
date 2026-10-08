
## 特定对象保存与恢复

## 后续步骤

## 保存与恢复

能够在后续会话中继续工作的能力标志着它是一个成熟且专业的应用程序。

借用第 18 章关于二进制、ASCII 和 ASCII 标记文件格式的讨论，后续章节满足了保存图形编辑器创建的图形对象的要求。

## 第四部分 布局组件

9: 52 28

10: 79 59

11: 65 59

12: 65 84

13: 74 91

相同的格式也适用于 `Arc` 对象：

```
14: 0OBJ - fg bg ls lw
15: 0 65535 0 1
16: ARC [x y width height angle1]
17: 85 88 56 40 23040
```

以及 `Text` 对象：

```
+   21: TEXT [ str x y ]
22: irene
23: 148 131
```

注意，为 `Text` 对象存储的字段远少于 `GXText` 结构中包含的字段。只有重现加载到编辑器中的对象所需的字段才会被放置在数据文件中。例如，由于编辑器只支持一种矢量文本字体，因此字体数据不需要放置在数据文件中。然而，如果将来你扩展了编辑器，允许用户从许多矢量字体中进行选择，则保存对象所分配的字体必须包含在数据文件中。通常，数据文件的格式策略考虑了内容的扩展性。

结合位置特定（position-specific）和标签文件（tagged-file）策略的优势在于，应用程序可以解析标签行，以知道如何解释位置特定的行。

在将来，当应用程序更加先进并增加功能时，标签行将更新以反映保存到文件中的额外数据字段。应用程序的新版本将包含对标签行的评估，以确定加载的是不包含额外数据的旧文件，还是包含这些数据的新文件。

接下来的章节显示了对 `Graphics Editor` 项目的必要修改，以支持使用结合位置特定和标签文件的格式的保存和恢复功能。

### 保存与恢复程序钩子（Hooks）

`Graphics Editor` 控制菜单的定义为保存和恢复函数提供了一个入口：

```
static GxIconData gxXcntrlIcons[] = {
.
  { &save_icon, gx_save, "Save current drawing..." },
  { &load_icon, gx_load, "Load saved drawing..." },
.
  { NULL, };
};
```

`gx_save` 和 `gx_load` 函数在此之前都是空函数（存根函数）。下一节将介绍它们的内容，但首先，我们必须修改通用对象结构（Common Object Structure），包含一个对象方法，用于保存每个图形对象包含的特定对象数据。

在位于 `gxGraphics.h` 头文件的 `Gx0b` 数据结构中添加以下行：

```
void (*move) (struct _gx_obj *, XEvent *);
void (*scale) (struct _gx_obj *, XEvent *);
void (*action) (struct _gx_obj *, XEvent *);
void (*save) (FILE *, struct _gx_obj *);
```

之后，此方法应该在位于 `gx6x.c` 源文件的 `gx_create_obj` 函数中初始化：

```
gx_obj->scale = (void (*)())null_func;
gx_obj->copy  = (void (*)())null_func;
gx_obj->save = (void (*)())null_func;
```

在定义并初始化了适当的对象方法后，我们现在来看 `gx_save` 和 `gx_load` 函数的内容。

### 通用对象保存与恢复

当用户点击 `Graphics Editor` 应用控制按钮面板上的保存图标时，会调用 `gx_save`。

该函数负责提示用户输入文件名、打开文件并遍历应用程序包含的所有对象，首先保存它们的通用数据元素，并调用对象的保存方法将对象特定数据写入文件。

`gx_save` 函数实现上述步骤的内容见列表 19.2。

#### 列表 19.2 gx_save 函数

```
1: void gx_save( )
2: {
3:     FILE *fp;
4: 
5:     char *filename = gxFileName();
6: 
7:     setStatus("Saving...");
8:     if (filename) {
9:         fp = fopen(filename, "w+");
10: 
11:     if (fp == NULL) {
12:         perror("Failed to open file: %s");
13:     } else {
14:         gxObjs(fp, gxHeader);
15:         fclose(fp);
16:     }
17: }
18:     setStatus("Saving done!");
19: }
```

`gx_save` 函数通过调用一个函数来提示用户输入文件名：

```
5:     char *filename = gxFileName();
```

当文件名返回后，以写入模式打开该文件：

```
9:         fp = fopen(filename, "w+");
```

在成功打开文件后（第 11 行），调用 `gxObjs`：

```
14:         gxObjs(fp, gxHeader);
```

接下来的部分显示了必要的修改。列表 19.3 显示了 `gxObjs` 函数。

### C 语言中的错误报告

`perror` 命令用于向标准错误（stderr）打印当打开文件失败时发生的错误信息：

```
12:         perror("Failed to open file: %s");
```

C 语言提供的 `perror` 函数会找到 `errno` 对应的字符串。为了让示例能够编译，必须包含：

```c
#include <error.h>
extern int errno;
```

#### 列表 19.3 从用户获取文件名

```c
1: static char *gxFileName( )
2: {
3:     AppContext app;
4: 
5:     XEvent event;
6: 
7:     XtWidget dialog;
8:     char *str = NULL;
9: 
10:     dialog = XtCreateWidget("Filename...",
11:                             XtWidgetClass,
12:                             GxDrawArea,
13:                             Xtwidth,
14:                             Xtheight,
15:                             XtLabel,
16:                             NULL);
17: 
18:     XawDialogAddButton(dialog, "Ok", close_dialog, dialog);
19: 
20:     app = XtWidgetToApplicationContext(GxDrawArea);
21: 
22:     while (XtManaged(dialog)) {
23:         XtNextEvent(app, &event);
24:         XtDispatchEvent(&event);
25: }
```

### 图 19.2 提示用户输入文件名

`gx_save` 函数通过从 `XtAppContext` 拦截并分发事件，直到用户关闭对话框：

```c
20: app = XtWidgetToApplicationContext(GxDrawArea);
21: 
22:     while (XtManaged(dialog)) {
23:         XtNextEvent(app, &event);
24:         XtDispatchEvent(&event);
25: }
```

`close_dialog` 函数在按钮按下时，简单地“取消管理”对话框：

```c
61: if (dialog) XtDestroyChild(dialog);
```

### 372 第四部分 布局组件

否则，如果移除非法字符已耗尽该字符串，则返回 NULL：

```
53:   else
54:     return NULL;
```

在列表 19.4 中引入的 `gxSaveObjs` 例程满足了列表 19.2 中引入的最终函数：

```
14:   gxSaveObjs( fp, gxObjHeader );

用于完成编辑器应用程序创建的对象的保存。
```

#### 列表 19.4 遍历编辑器对象以保存

```c
1:   static void gxSaveCommon( FILE *fp, GXObjPtr obj)
2:   {
3:     fprintf(fp, "OBJ - fg bg %d lw\n");
4:     fprintf(fp, "%ld %ld %ld\n",
5:     obj->fg, obj->bg, obj->ls, lw);
6:   }
7:   {
8:   static void gxSaveObjs( FILE *fp, GXObjPtr obj)
9:   {
10:    if(obj) {
11:        gxSaveCommon(fp, obj);
12:        (*obj->save)(fp, obj);
13:
14:        gxSaveObjs(fp, obj->next);
15:    }
16:  }
```

列表 19.4 中的 `gxSaveObjs` 函数是一个递归函数，会被重复调用直到找到对象列表的末尾。这两行

```
10:   if(obj) {
```

和

```
14:   gxSaveObjs(fp, obj->next);
```

对于该函数的递归特性都同样重要。第 10 行确保了提供了有效的对象引用，因为列表的末尾标记为 NULL，而第 14 行传递了下一个可能的对象。

对于列表中的每个对象，都会调用两个函数。第一个是保存公共对象数据字段：

```
11:   gxSaveCommon(fp, obj);
```

第二个是保存对象特定的数据：

```
12:   (*obj->save)(fp, obj);
```

### 保存与恢复 第 19 章 373

`gxSaveCommon` 简单地将标记行和特定位置的数据写入到文件指针引用的文件中：

```
3: fprintf( fp, "OBJ - fg bg ls lw\n");
4: fprintf( fp, "%ld %ld %ld\n");
5: obj->fg, obj->bg, obj->ls, obj->lw );
```

图形保存方法在第 20–24 章中随着对象内部结构的定义被引入。

本节演示了由图形编辑器保存操作生成的数据如何在编辑器中恢复。

### 对象特定的保存与恢复

当用户点击位于图形编辑器应用程序控制面板上的“加载”图标时，会调用 `gx_load` 函数。

该函数负责提示用户输入文件名，遍历文件内容，并根据文件中的标签创建特定于标签的对象。

列表 19.5 显示了 `gx_load` 函数的内容。

#### 列表 19.5 gx_load 函数

```c
1: void gx_load( void )
2: {
3:   FILE *fp;
4:
5:   char *filename = gxGetFileName();
6:
7:   setStatus("Loading objects...");
8:   if (filename) {
9:     fp = fopen(filename
```

在提示文件名后，文件将以只读模式打开：

```
8: if (filename) {
9:   fp = fopen(filename, "r");
```

### 374 第四部分 布局组件

如果文件成功打开，则带有文件引用调用 `gxLoadObjs` 函数：

```
14:    gxLoadObjs( fp );
```

列表 19.6 引入了 `gxLoadObjs` 函数，它遍历由 `fp` 引用的文件，并调用必要的函数将对象恢复到编辑器。

#### 列表 19.6 将对象加载到编辑器

```c
1:    static void gxCommon(FILE *fp, GXObjPtr obj)
2:    {
3:        sscanf(fp, "%ld %ld %ld\n",
4:            &obj->fg, &obj->bg, &obj->ls, &obj->lw);
5:    }
6:
7:    static void gxLoadObjs(FILE *fp)
8:    {
9:        char objForm[128];
10:        GXObjPtr obj;
11:
12:        while (fgets(objForm, 128, fp) != NULL) {
13:            obj = gx_create_obj(fp, obj);
14:            gxLoadCommon(fp, obj);
15:
16:        fgets(objForm, 128, fp);
17:        switch (*objForm) {
18:            case 'A':
19:                gxArcLoad(fp, obj);
20:                break;
21:
22:            case 'L':
23:                gxLineLoad(fp, obj);
24:                break;
25:
26:            case 'T':
27:                gxTextLoad(fp, obj);
28:                break;
29:        }
30:    }
31:}
```

`gxLoadObjs` 函数通过文件指针 `fp` 检索文件，并使用 `fgets` 函数填充 `objForm` 数组直到遇到换行符：

```
12:    while (fgets(objForm, 128, fp) != NULL) {
```

从而获取该对象的标记行。

### 保存与恢复 第 19 章 375

> 注意 了解文件的格式，你知道该行包含了特定位置数据的标记。由于这是版本 1.0，不需要解析标记行。然而，如果在未来的应用程序版本中添加了数据字段，就需要解析该行。

在提取了标记行后，读取了对象特定的数据：

```
14: gxLoadCommon(fp, obj);
```

注意在 `gxLoadCommon` 函数中，读取 `gxSaveCommon` 数据的语法非常相似。具体来说，`fwrite` 被重命名为 `fscanf`，并提供了结构元素的地址以便将来自值赋值给它们：

```
3: fscanf( fp, "%ld %ld %ld\n",
4: &obj->fg, &obj->bg, &obj->ls, &obj->lw );
```

恢复公共对象后，文件的下一行是对象特定的数据的标记行。通过将此行读取到 `objForm` 数组：

```
16: fgets(objForm, 128, fp);
```

你可以确定要调用哪个加载程序，因为第一个字符足以判断对象类型：

```
17: switch (*objForm) {
```

根据第一个字符的值，调用 `gxArcLoad`、`gxLineLoad` 或 `gxTextLoad` 方法之一来读取特定于该类型的数据。

这些函数将在后续章节中引入，当各种编辑器的内部结构被引入时。

![](img/786ba9bd5cd671beb490264fd2e6aae1_397_0.png)

### 后续

增加支持保存和恢复的功能对于成熟的产品是必要的。相对于本文的流程，本章完成了图形编辑器对象的演进，使我们能够处理完整定义每个对象的任务。

第五部分“向编辑器添加对象”五个章节提供了创建功能性图形编辑器所需的内部对象方法和函数定义。

## 第五部分 向编辑器添加对象

# 第 20 章

- 创建直线对象对象

- 绘制和删除直线对象

- 查找直线对象

- 选择和取消选择直线对象

- 移动直线对象

- 缩放直线对象

- 复制直线对象

- 保存和恢复直线对象

- 后续

### 直线对象对象

通过选择图 20.1 中的图标，用户开始创建直线对象的过程。

![](img/786ba9bd5cd671beb490264fd2e6aae1_401_0.png)

### 创建 Latex 行对象

在第 13 章“应用结构”中引入了 `gxDrawIcons` 数组的定义

```c
{ &line_icon, (void (*)(void)gx_line,
"Draw an elastic line..."
};
```

它为线条图标（Line Icon）分配了 `gx_line` 函数，以便在用户选择时进行调用。该函数定义在列表 20.1 中，它作为创建 Latex 对象过程的入口点。

#### 列表 20.1 gx_line 函数
