
```cpp
    LineEdit->setMinimumSize(LineEdit->sizeHint());

    LineEditLabel->setMinimumSize(LineEditLabel->sizeHint());

    Count->setMinimumSize(Count->sizeHint());

    QGridLayout *GridLayout = new QGridLayout(this,2,3);

    GridLayout->addWidget(LineEdit,0,1);

    GridLayout->addWidget(LineEditLabel,0,0);

    GridLayout->addWidget(OkButton,1,2);

    GridLayout->addWidget(CancelButton,1,1);

    GridLayout->addWidget(Count,0,2);

    GridLayout->activate();

}

int main(int argc, char *argv[])

{

QApplication PenguinApp(argc, argv);

window_layout *LMWindow = new window_layout();

LMWindow->show();

PenguinApp.setMainWidget(LMWindow);

return PenguinApp.exec();

}
```

代码列表 10-2 的输出如图 10-16 所示。

![](img/859df50987094e32dd2f5bb576f82bce_336_0.png)

图 10-16：代码列表 10-2 的输出。

创建了一个 `QGridLayout` 对象：

```cpp
QGridLayout *GridLayout = new QGridLayout(this,2,3);
```

该对象创建了一个具有两行三列的 `QGridLayout` 对象。通过调用 `addWidget()` 方法将每个控件添加到布局管理器：

```cpp
GridLayout->addWidget(LineEdit,0,1);
GridLayout->addWidget(LineEditLabel,0,0);
GridLayout->addWidget(OkButton,1,2);
GridLayout->addWidget(CancelButton,1,1);
GridLayout->addWidget(Count,0,2);
```

图 10-16 显示了控件的位置。`LineEdit` 控件被添加到第 0 行第 1 列的单元格。`LineEditLabel` 被添加到第 0 行第 0 列的单元格。`OkButton` 控件被添加到第 1 行第 2 列的单元格。`CancelButton` 控件被添加到第 1 行第 1 列的单元格，而 `Count` 控件被添加到第 0 行第 2 列的单元格。

通过布局管理器，你可以确保你的对话框无论出于什么原因都能正确布局。给用户提供父可能有所帮助

## 337 第10章：图形用户界面设计

通过布局管理器，你可以确保你的对话框无论出于什么原因都能正确布局。给用户提供父可能有所帮助

## 相对位置

通过布局管理器，你可以确保你的对话框无论出于什么原因都能正确布局。给用户提供父可能有所帮助

## 绝对坐标

通过布局管理器，你可以确保你的对话框无论出于什么原因都能正确布局。给用户提供父可能有所帮助

## 布局系统

通过布局管理器，你可以确保你的对话框无论出于什么原因都能正确布局。给用户提供父可能有所帮助

## 338 第10章：图形用户界面设计

通过布局管理器，你可以确保你的对话框无论出于什么原因都能正确布局。给用户提供父可能有所帮助

![](img/859df50987094e32dd2f5bb576f82bce_338_0.png)

![](img/859df50987094e32dd2f5bb576f82bce_338_1.png)

图 10-16：代码列表 10-2 的输出。

## 339 第10章：图形用户界面设计

# 表 10-6 控件的坐标转换方法

| 坐标转换方法 | 说明 |
| --- | --- |
| `QPoint::mapToGlobal(const QPoint &Pos)` | 将控件坐标 `Pos` 转换为全局屏幕坐标。 |
| `QPoint::mapToParent(const QPoint &Pos)` | 将控件坐标 `Pos` 转换为父坐标。如果控件没有父级，则与调用 `mapToGlobal()`相同。 |
| `QPoint::mapFromParent(const QPoint &Pos)` | 将父坐标 `Pos` 转换为控件坐标。如果没有父控件，则与调用 `mapToGlobal()`相同。 |
| `QPoint::mapFromGlobal(const QPoint &Pos)` | 将全局屏幕坐标 `Pos` 转换为控件坐标。 |

```cpp
Label = new QLabel(this);
Label->setGeometry(10,10,100,30);
setGeometry(200,200,150,100);
void moved_window::moveEvent(QMouseEvent *event) {
stringstream X;
QPoint Point;
Point = mapToGlobal(QPoint(0,0));
X << "" << Point.x() << "," << Point.y() << "" << endl;
Label->clear();
Text.assign(X.str());
Label->setText(Text.c_str());
}
```

```cpp
int main(int argc, char *argv[]) {
Application App(argc, argv);
moved_window *Window = new moved_window();
App.setMainWindow(Window);
Window->show();
return App.exec();
}
```
