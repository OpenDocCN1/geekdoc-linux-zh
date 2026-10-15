
```c
gtk_toggle_button_set_state(GTK_TOGGLE_BUTTON (mine->widget), FALSE);
} else {
    /* --- 将按钮置于“按下”状态 --- */
    mine->buttonState = BUTTON_DOWN;
    gtk_toggle_button_set_state(GTK_TOGGLE_BUTTON (mine->widget), TRUE);
    /* --- 如果该位置有炸弹 --- */
    if (mine->bHasBomb) {
        /* --- 在该位置显示炸弹 --- */
        AddImageToMine(mine, xpm_bomb);
    }
    /* --- 没有炸弹，但附近有炸弹 --- */
    else if (mine->nBombsNearby) {
        /* --- 显示附近炸弹的计数。 --- */
        AddImageToMine(mine, digits[mine->nBombsNearby]);
    } else {
        /* --- 点击了这里，但既没有炸弹也没有数字计数。 --- */
        /* --- 打开这里附近的所有方格 - 可能会连锁反应。 --- */
        OpenNearbySquares(mine->nCol, mine->nRow);
    }
}
```

### ResetGame
```c
/*
 * ResetGame
 * 重置游戏以便重新开始。重置炸弹
 * 计数并创建一个漂亮的炸弹分布区域。
 */
void ResetGame(int nGridColumns, int nGridRows, int nBombs, int bNewButtons)
{
  /* --- 重置网格中的炸弹数量 ... */
  nTotalBombs = nBombs;
  /* --- 重置未区域的炸弹数量 ... */
  nBombsLeft = nBombs;
  /* --- 创建扫雷游戏按钮。 ... */
  CreateMineseperButtons(table, nGridRows, bNewButtons);
  /* --- 停止定时器。 ... */
  StopTimer();
  UpdateSeconds(0);
  SetStartIcon((gchar **) xpm_smile);
}
```

### FreeCallback
```c
/*
 * FreeCallback
 * 释放组件。
 */
void FreeChildCallback(GtkWidget *widget) {
  gtk_widget_destroy(widget);
}
```

### SetStartIcon
```c
/*
 * SetStartIcon
 * 根据传入的设置
 * 设置按钮的起始图像。
* 根据传入的 xpm。
 */
void SetStartIcon(gchar **xpm) {
  GtkWidget *widget;
  /* --- 创建组件 --- */
  widget = CreateWidgetFromXpm(xpm);
  /* --- 将其添加到容器 --- */
  gtk_container_add(GTK_CONTAINER (start_window), widget);
  /* --- 显示组件 --- */
  gtk_widget_show(widget);
}
```

### start_clicked
```c
/*
 * start_clicked
 * 处理点击开始的
 * 按钮。
 */
void start_clicked(GtkWidget *widget, gpointer *data) {
    typeMinesweeperButton *mine;
    GtkWidget *label;
    mine = (typeMinesweeperButton *) data;
    /* --- 如果游戏已经结束 --- */
    if (bGameOver) {
        printf("game over = %d\n", bGameOver);
        return;
    }
    /* --- 如果是点击了按钮 --- */
    if (mine->buttonState == 1) {
        /* --- 重置游戏 --- */
        ResetGame(nCols, nRows, nBombs, FALSE);
    }
}
```

### mine_button_clicked
```c
/*
 * mine_button_clicked
 * 处理点击按钮的
 * 事件。
 */
void mine_button_clicked(GtkWidget *widget, gpointer *data) {
    typeMinesweeperButton *mine;
    GtkWidget *label;
    mine = (typeMinesweeperButton *) data;
    /* --- 如果游戏已经结束 --- */
    if (bGameOver) {
        printf("game over = %d\n", bGameOver);
        return;
    }
    /* --- 如果是点击了按钮 --- */
    if (mine->buttonState == 0) {
        /* --- 如果点击了炸弹 --- */
        if (mine->bHasBomb) {
            /* --- 游戏结束，哥们！ --- */
            bGameOver = TRUE;
            /* --- 设置哭脸 --- */
            SetStartIcon((gchar **) xpm_frown);
            /* --- 显示所有炸弹 --- */
            StopTimer();
            ShowBombs(mine);
        } else {
            /* --- 创建一个标签并将附近的炸弹数量放入其中 --- */
            DisplayHiddenInfo(mine);
            CheckForWin();
        }
    } else if (mine->buttonState == 2) {
        /* --- 如果是标记了旗帜 --- */
        /* --- 释放旗帜 --- */
        FreeChild(widget);
        mine->buttonState = 0;
        AddImageToMine(mine, xpm_flag);
        nBombsLeft++;
    }
    DisplayBombCount();
    CheckForWin();
}
```

```c
{
  int row,
  int column)
  GtkWidget *button;
  /* * 创建按钮 ... */
  button = gtk_toggle_button_new ();
  /* * 初始化按钮字段 ... */
  mine->buttonState = BUTTON_UNKNOWN;
  mine->nRow = row;
  mine->nCol = column;
  /* * 我们关注按钮是否被点击了 ... */
  gtk_signal_connect(GTK_OBJECT (button), "clicked",
      GTK_SIGNAL_FUNC (mine_button_clicked), mine);
  /* * 我们关注其他鼠标事件。 ... */
  gtk_signal_connect(GTK_OBJECT (button), "button_press_event",
      GTK_SIGNAL_FUNC (button_press), mine);
  /* * 将按钮放在表格的正确位置。 ... */
  gtk_table_attach(GTK_TABLE (table), button,
      column, column+1,
      row + 1, row + 2,
      GTK_FILL | GTK_EXPAND,
      GTK_FILL | GTK_EXPAND,
      0, 0);
  /* * 设置按钮为统一尺寸 ... */
```
