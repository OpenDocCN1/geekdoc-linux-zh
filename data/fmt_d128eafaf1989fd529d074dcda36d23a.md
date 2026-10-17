
`gtk_widget_set_usesize(button, BUTTON_WIDTH, BUTTON_HEIGHT);`

/* * 让按钮可见 ... */

`gtk_widget_show(button);`

/* * 返回按钮。 ... */

`return (button);`

}

### CountNearbyBombs
* 统计该方格相邻的雷弹数量。

```c
int CountNearbyBombs (int col, int row)
{
    int i, j;
    int nCount = 0;
    /* 每一个距离最多 1 个方格的方格 -- **/
    for (i = MAX (col-1, 0); i <= MIN (col+1, nCols-1); i++) {
        for (j = MAX (row-1, 0); j <= MIN (row+1, nRows-1); j++) {
            /* 如果它有雷弹 -- */
            if (mines[i][j].bHasBomb) {
                /* 记录计数。 -- */
                nCount++;
            }
        }
    }
    return (nCount);
}
```

### CreateMinesweeperButtons
* 根据程序开头定义的表格，在扫雷游戏中创建按钮。按钮指针（句柄）被存储回表格中，以便稍后引用。

```c
void CreateMinesweeperButtons (GtkWidget *table,
    int nGridColumns,
    int nRows,
    int bNewButtons)
{
    int ci;
    int ri;
    GtkWidget *button;
    int nBombs;
    typMinesweeperButton *mine;
    /* 更新全局变量 -- */
    nCols = nGridColumns;
    nRows = nGridRows;
    bGameOver = FALSE;
    bGame = TRUE;
```

```c
/* --- 更新雷弹数量。 --- */
DisplayBombCount();
```

```c
/* --- 检查每个按钮 --- */
for (ci = 0; ci < nCols; ci++) {
for (ri = 0; ri < nRows; ri++) {
```

```c
/* --- 单元完全没有任何内容。 --- */
mine = &mines[ci];
mine->bHasBomb = 0;
mine->buttonState = BUTTON_UNKNOWN;
```

```c
/* --- 单元格关联了雷弹？ --- */
if (bNewButtons) {
```

```c
/* --- 创建一个按钮 --- */
mine->widget = CreateButton(table, mine, ri, ci);
```

```c
} else {
/* --- 复用现有按钮 --- */
```

```c
/* --- 释放任何 xpm/标签 --- */
FreeChild(mine->widget);
```

```c
/* --- 弹出按钮。 --- */
tgtk_toggle_button_set_state(
GTK_TOGGLE_BUTTON(mine->widget),
FALSE);
```

```c
}
}
```

```c
/* --- 放置雷弹。 --- */
nBombs = nTotalBombs;
```

```c
/* --- 只要我们还有要放置的雷弹 --- */
while (nBombs > 0) {
```

```c
/* --- 计算行/列位置 --- */
ci = rand() % nCols;
ri = rand() % nRows;
```

```c
/* --- 如果不存在雷弹，就创建一个！ --- */
if (mines[ci][ri].bHasBomb == 0) {
mines[ci][ri].bHasBomb = 1;
nBombs--;
```

```c
}
n/* ... 一旦所有雷弹分布完毕，计算
 * 每个按钮相邻的雷弹数量。
 */
/* --- 检查每个按钮 --- */
for (c1 = 0; c1 < nCols; c1++) {
    for (ri = 0; ri < nRows; ri++) {
    mine = &bombs[ci][ri];
    /* --- 有多少按钮？ --- */
    mine->nNearby = CountNearbyBombs(ci, ri);
    }
}
bResetGame = FALSE;
}
```

### SetGrid
* 设置游戏网格的大小为指定的尺寸以及雷弹数量。

```c
void SetGrid(int nGridColumns, int nGridRows, int Bombs) {
    int row, col;
    /* --- 如果表格存在。 --- */
    if (table) {
        /* --- 销毁它。 --- */
        gtk_widget_destroy(table);
    }
    /* 为按钮创建表格 --- */
    table = gtk_table_new(nGridColumns, nGridRows, FALSE);
    /* 将其加入 vbox --- */
    gtk_box_pack_start(vbox, table, FALSE, 0);
    /* 显示表格。 --- */
    gtk_widget_realize(table);
```

```c
/* --- 用数字重置游戏 --- */
ResetGame(nGridColumns, nGridRows, TRUE);
/* --- 显示表格。 --- */
gtk_widget_show(table);
}
```

### main
* 程序从这里开始

```c
int main (int argc, char *argv[])
{
    GtkWidget *window;
    GdkBitmap *mask;
    GtkStyle *style;
    GtkWidget *smile;
    GtkWidget *hbox;
    /* --- GTK 初始化 ... */
    gtk_init (&argc, &argv);
    /* --- 创建顶层窗口 ... */
    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    /* --- 不允许窗口调整大小。 ... */
    gtk_window_set_policy (window, FALSE, TRUE);
    /* --- 给窗口设置标题。 ... */
    gtk_window_set_title (window, "minesweeper");
    /*
 * 你应该始终将销毁事件
* 绑定到主窗口。
*/
    gtk_signal_connect (GTK_OBJECT (window), "delete_event",
    GTK_SIGNAL_FUNC (delete_event), NULL);
    vbox = gtk_vbox_new (FALSE, 1);
    gtk_widget_show(vbox);
    /* --- 创建应用程序菜单 ... */
    CreateMenu (window, vbox);
```

```c
/* --- 分/开始按钮的水平布局 --- */
hbox = gtk_hbox_new (TRUE, 1);
gtk_widget_show(hbox);
gtk_box_pack_start (vbox), hbox, FALSE, 0);
```

```c
/* 页面上剩余雷弹的标签 * */
```

```c
/* --- 创建带有笑脸的开始按钮 * */
button_start = gtk_button_new ();

/* --- 我们关注按钮是否被点击 --- * */
gtk_signal_connect(GTK_OBJECT (button_start),
  "clicked",
