
## 缩放线条对象

对象的 `scale` 方法在第16章“处理对象导航”部分（第334页）中引入，当用户选择其中一个活动句柄时被分配为活动操作。列表 20.13 中引入的 `line_scale` 方法管理着 `Line` 对象的缩放操作。

### 列表 20.13 缩放线条对象

```
1: static void line_scale( GXObjPtr line, XEvent *event )
2: {
3: static GXLinePtr tmp_data = NULL;
4: GXLinePtr line_data = (GXLinePtr)line->data;
5:
6: if (tmp_data) {
7:     DrawLines(XtDisplay(GxDrawArea),
8:             XtWindow(GxDrawArea), rubberGC,
9:             tmp_data->pts, tmp_data->num_pts,
10:         CoordModeOrigin);
11: } else {
12:     /* 我们的第一次... */
13:     (*line->erase)( line );
14:     
15:     tmp_data = (GXLinePtr)XtNew(GX);
16:     tmp_data->num_pts = line_data->num_pts;
17:     tmp_data->pts = (XPoint *)
18:     XtMalloc(sizeof(XPoint) * tmp_data->num_pts);
19:
20:     get_bounds(line_data->pts, line_data->num_pts,
21:         &OrgX, &OrgY, &ExtntX, &ExtntY);
22:     }
23: }
24: if (event) {
25:     memcpy((char*)tmp_data->pts, (char*)line_data->pts,
26:             sizeof(XPoint) * tmp_data->num_pts);
27:
28:
29:     apply_delta(tmp_data->pts, tmp_data->num_pts,
30:         FixedX - event->button.x,
31:         FixedY - event->button.y);
32:
33:
34:     DrawLines (XtDisplay(GxDrawArea),
35:         XtWindow(GxDrawArea), rubberGC,
36:         tmp_data->pts, tmp_data->num_pts,
37:         CoordModeOrigin);
38: } else {
39:     if (tmp_data) {
40:         memcpy((char*)line_data->pts,
41:             (char*)tmp_data->pts,
42:             sizeof(XPoint) * line_data->num_pts );
43:     }
44:     XtFree((char *)tmp_data->pts);
45:     XtFree((char *)tmp_data);
46:     tmp_data = NULL;
47:     }
48: }
```

`line_scale` 模型考虑到由于 `line_data->pts` 中包含点的浮点计算容易产生累积舍入误差，因此在每次调用该函数时都会创建点的副本。然后将 `FixedX` 和 `FixedY` 当前事件分量的增量加到原始的 `line_data->pts` 中。这种数据管理确保了浮点计算引入的误差范围降至最低。

> 如需查看 `apply_delta` 函数执行的计算，请参见第11章“缩放线条”（第234页）。

```c
static void line_copy(GXObjPtr line)
{
  int i;
  GXLinePtr temp_data;
  GXLinePtr line_data = (GXLinePtr)line->data;

  (*->deselect(line));

  temp_data = (GXLine*)XtNew(GXLine);
  temp_data->num_pts = line_data->num_pts;

  temp_data->pts = (XPoint *)XtMalloc(sizeof(XPoint) * temp_data->num_pts);
  for(i = 0; i < temp_data->num_pts; i++) {
    temp_data->pts[i].x = line_data[i].x + OFFSET;
    temp_data->pts[i].y = line_data[i].y + OFFSET;
  }

  create_line(NULL, temp_data);
  XtFree((char *)temp_data);
}
```

`line_scale` 函数要求创建 `GXLine` 结构体的临时副本，而 `line_move` 函数需要一个较小的步骤来理解。具体来说，是确保活动对象的句柄从屏幕上移除：

```c
(*->deselect(line));
```

在第 9 到 13 行创建了一个临时的 `GXLine` 结构，并将原始对象的点拷贝到新结构中，但增加了 `OFFSET` 偏移，这样新对象就不会与原始对象完全重叠：

```c
temp_data->pts[i].x = line_data[i].x + OFFSET;
temp_data->pts[i].y = line_data[i].y + OFFSET;
```

这个临时的 `GXLine` 结构被用于创建一个全新的 `Line` 对象，该对象包含原始对象点的偏移：

```c
create_line(NULL, temp_data);
```

接下来的章节介绍了 `Line` 对象所需的最后一个功能区域：保存和恢复对象特定数据。

## 保存和恢复 Line 对象

在第 19 节引入的保存和恢复图形编辑器中包含的对象的功能，为我们的应用程序提供了成熟的能力。

在列表 20.15 中找到 `line_save` 方法遵循了之前介绍的保存策略。

### 402 第 V 部分 向编辑器添加对象

### 列表 20.15 保存线到文件对象

```c
static void line_save(FILE *fp, GXObjPtr obj)
{
  int i;
  GXLinePtr line = (GXLinePtr)obj->data;

  fprintf(fp, "LINE [numpts x y y ...]\n");
  fprintf(fp, "%d\n", line->num_pts);

  for(i = 0; i < line->num_pts; i++) {
    fprintf(fp, "%d %d\n", line->pts[i].x, line->pts[i].y);
  }
}
```

`line_save` 函数从对象的公共位置提取 `GXLine` 数据：

`GXLinePtr line = (GXLinePtr)obj->data;`

并通过写入反映后续数据格式的带标签行，为保存其包含的数据做准备：

`fprintf(fp, "LINE [numpts x y y ...]\n");`

以及将要写入的点数：

`fprintf(fp, "%d\n", line->num_pts);`

最后，它将点逐行写入由 `fp` 指向的目标文件：

```c
for(i = 0; i < line->num_pts; i++) {
  fprintf(fp, "%d %d\n", line->pts[i].x, line->pts[i].y);
}
```

列表 20.16 中的 `GXLineLoad` 函数显示了如何将 `line_save` 方法写入的数据恢复到编辑器中。

### 列表 20.16 从文件对象恢复线

```c
void lineLoad(FILE *fp, GXObjPtr obj)
{
  int i;
  GXLine line;

  fscanf(fp, "%d\n", &line.num_pts);

  line.pts = (XPoint *)Xtmalloc(sizeof(XPoint) * line.num_pts);

  for(i = 0; i < line.num_pts; i++) {
    fscanf(fp, "%hd %hd\n", &line.pts[i].x, &line.pts[i].y);
  }

  create_line(obj, &line);
}
```
