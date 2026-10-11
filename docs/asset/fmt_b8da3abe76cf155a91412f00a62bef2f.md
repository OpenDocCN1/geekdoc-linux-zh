
```cpp
63 QGridLayout *grid = new QGridLayout(4,3);
64
65     normal = new QLabel("Normal",this);
66     grid->addWidget(normal,1,0);
67     disabled = new QLabel("Disabled",this);
68     grid->addWidget(disabled,2,0);
69     active = new QLabel("Active",this);
70     grid->addWidget(active,2,0);
71     small = new QLabel("Small",this);
72     grid->addWidget(small,0,1);
73     large = new QLabel("Large",this);
74     grid->addWidget(large,0,2);
75
76     normalSmall = new QLabel("",this);
77     grid->addWidget(normalSmall,1,1);
78     normalLarge = new QLabel("",this);
79     grid->addWidget(normalLarge,1,2);
80     disabledSmall = new QLabel("",this);
81     grid->addWidget(disabledSmall,2,1);
82     disabledLarge = new QLabel("",this);
83     grid->addWidget(disabledLarge,2,2);
84     activeSmall = new QLabel("",this);
85     grid->addWidget(activeSmall,3,1);
86     activeLarge = new QLabel("",this);
87     grid->addWidget(activeLarge,3,2);
88
89
90     return(grid);
90 }
91 void SetSetIcon(const QPixmap *pixmap)
92 {
93     pixLabel->setPixmap(pixmap);
94     nameLabel->setText(pixName);
95
96     QIconSet iconset(pixmap);
97
98     QPixmap p;
99     p = iconset.pixmap(QIconSet::Small,QIconSet::Normal);
100    normal->setPixmap(p);
101    p = iconset.pixmap(QIconSet::Large,QIconSet::Normal);
102    large->setPixmap(p);
104
    p = iconset.pixmap(QIconSet::Small,QIconSet::Disabled);
105    disabledSmall->setPixmap(p);
106    p = iconset.pixmap(QIconSet::Large,QIconSet::Disabled);
107    disabledLarge->setPixmap(p);
108
109    p = iconset.pixmap(QIconSet::Small,QIconSet::Active);
110    activeSmall->setPixmap(p);
111    p = iconset.pixmap(QIconSet::Large,QIconSet::Active);
112    activeLarge->setPixmap(p);
113 }
114 void SetSetIcon(const QPixmap *pixmap)
115 {
116     QString filter = "Icon (*.png *.xpm *.xbm)";
```

```cpp
117   QString name = QFileDialog::getFileName(
118                               filter,this);
119   if(name.isEmpty()) {
120       int length = name.length() - name.findRev('/');
121       pixmapName = name.right(length - 1);
122       pixmap = QPixmap(name);
123       insertNewPixmap();
124   }
```

`SetIcon` 小控件通过其第 15 行的构造函数在第 18 行作为应用程序的顶级窗口，第 19 行指定了初始 `pixmap` 的名称和值。窗口布局为水平的 `hbox`，其中左侧包含一个 `QVBoxLayout` 布局，右侧包含一个 `QGridLayout` 布局。第 22 行和第 25 行的 `makeVerticalBox()` 和 `makeGrid()` 调用在水平框中创建了两个子布局。

第 29 行的 `insertNewPixmap()` 调用将初始 `pixmap` 初始化为当前显示的内容。第 31 行的 `connect()` 调用将槽方法 `newPixmap()` 建立为点击按钮时执行的函数。

第 35 行的 `makeVerticalBox()` 方法创建了选择按钮、用于修改统一图形的显示标签以及用于图形文件命名的标签。该框在第 41 行至 43 行之间被创建并插入。第 47 行至 55 行创建了两个标签并将其添加到垂直框中。这些标签在没有 `pixmap` 时留空，其文件名将在稍后安装。

从第 61 行开始的 `makeGrid()` 方法使用 `QGridLayout` 创建了一个 `QLabel` 对象的表格，用于显示当前 `pixmap` 的各种形态。网格宽 3 个单元格，高 4 个单元格。第一行和第一列用于注释标签，如图 9-7 窗口右侧所示。第 65 行至 74 行创建的标签是注释，因此它们创建时都带有文本。第 76 行至 87 行创建的标签用于显示 `pixmap` 图形，因此创建时没有文本。

第 91 行的 `insertNewPixmap()` 方法使用当前的 `pixmap` 信息来填充显示内容。该方法在程序运行时被调用以安装 `pixmap`，并且每当选择新 `pixmap` 时都会再次调用。

第 96 行的 `QIconSet icon(pixmap)` 从 `pixmap` 创建一组图标。第 99 行的方法用于获取不同尺寸的 `pixmap`。第 100 行和第 102 行的方法分别设置了普通和大型 `pixmap`。第 105 行和第 107 行的方法设置了禁用的小型和大型 `pixmap`。第 110 行和第 112 行的方法设置了激活的小型和大型 `pixmap`。

# 216 第二部分 ♦ 循序渐进

它们本身。这一系列原点被称为基线（baseline）。升高值（ascent）和下降值（descent）是从基线到字符顶部和底部的测量值——升高度和下降值之和即为字符的高度。字符的宽度是从原点到字符右侧的距离。左侧边距（lbearing）是从原点到字符的距离，右侧边距（rbearing）是图形部分的宽度。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_235_0.png)

图 10-1：单个字符的字体测量

从图 10-1 的升高、下降值和高度测量中可以看到，下降值的值可以为零。左侧边距值也可能为零。事实上，当字符的字形绘制在原点的左侧时，该值可以是负数。（例如，这可能发生在斜体字体的部分。）

图 10-2 显示了对字符字符串可以进行的一系列测量。升高度、下降值和高度可以包含一个超出最大范围向上、向下或两向延伸的导引区域。宽度也是如此。字符串周围的边界允许您的程序轻松地将文本段（即使是不同的字体）并在一起，并保持间距正确。字符串的原点——用于绘制字符串的 x 和 y 坐标——是字符串中最左侧字母的原点。其他字母的原点在内部用于在绘制字符串时将每个字母相邻。

### 字体名称

字体存储在磁盘文件中。字体文件是标准 X 分发版的一部分。当应用程序请求字体时，它会从文件加载到 X 服务器，而不是应用程序中。由于字体在服务器中，因此不需要将详细的字体信息从应用程序传递到服务器进行显示。这种流量的减少可以为您节省大量时间，因为通常会由另一台计算机上的应用程序控制一个 X 窗口（带有其本地服务器）。如果有多个用户使用相同的字体，则只需要加载一个副本。
