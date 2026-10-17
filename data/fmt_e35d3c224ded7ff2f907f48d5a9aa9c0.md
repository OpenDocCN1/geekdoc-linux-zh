
我们省略了始终可见的控件（行编辑、查找按钮等），但展示了根据“更多”按钮状态显示或隐藏的额外控件。我们还维护了一个额外控件的列表，以便我们可以统一处理它们。

# 第 13 章 动画与状态机框架

![](img/74b321c00e6b987639de429f0799cff9_498_0.png)

![](img/74b321c00e6b987639de429f0799cff9_498_1.png)

![](img/74b321c00e6b987639de429f0799cff9_498_2.png)

![](img/74b321c00e6b987639de429f0799cff9_498_3.png)

![](img/74b321c00e6b987639de429f0799cff9_498_4.png)

![](img/74b321c00e6b987639de429f0799cff9_498_5.png)

![](img/74b321c00e6b987639de429f0799cff9_498_6.png)

![](img/74b321c00e6b987639de429f0799cff9_498_7.png)

查找对话框点击“更多”按钮

这两个状态机只有两个状态，它们的名称应该清晰易懂。

构造函数遵循熟悉的模式：创建控件、布局和连接，然后创建状态机和转换。这里是 `createWidgets()` 方法的提取：

```cpp
wholeWordsCheckBox = new CheckBox(tr("Whole Words Only"), this);

wholeWordsCheckBox->setChecked(false);

syntaxLabel = new QLabel(tr("Syntax:"), this);

syntaxComboBox = new QComboBox(this);

syntaxLabel->setBuddy(syntaxComboBox);

syntaxComboBox->addItem(tr("Literal"));

syntaxComboBox->addItem(tr("Regex"));

syntaxComboBox->addItem(tr("Wildcard"));

syntaxComboBox->setCurrentIndex(0);

extraWidgets << wholeWordsCheckBox << syntaxLabel << syntaxComboBox;

foreach (QWidget *widget, extraWidgets) {
  QGraphicsOpacityEffect *effect = new QGraphicsOpacityEffect;

  effect->setOpacity(1.0);

  widget->setGraphicsEffect(effect);
}
```

我们为额外的控件都添加了透明度效果，将其初始透明度设置为 1.0（完全不透明）。

```cpp
void Dialog::stateMachines() {
  findStateMachine = new QStateMachine(this);

  createFindStates();

  createFindTransitions();

  findStateMachine->setInitialState(nothingToFindState);

  findStateMachine->start();

  extraStateMachine = new QStateMachine(this);

  createShowExtraWidgetsState();

  createHideExtraWidgetsState();

  createShowExtraWidgetsTransitions();

  createHideExtraWidgetsTransitions();

  extraStateMachine->setInitialState(hideExtraWidgetsState);

  extraStateMachine->start();
}
```

该方法用于创建、设置并启动状态机。对于额外的状态机，我们在独立的辅助方法中设置显示和隐藏状态及其转换，以保持每个方法的规模适中。

```cpp
void Dialog::findStates() {
  nothingToFindState = new QState(findStateMachine);

  nothingToFindState->assignProperty(findButton, "enabled", false);

  somethingToFindState = new QState(findStateMachine);

  somethingToFindState->assignProperty(findButton, "enabled", true);
}
```

```cpp
void Dialog::findTransitions() {
  nothingToFindState->addTransition(findButton, &QPushButton::clicked, somethingToFindState);
}
```

```cpp
void Dialog::createShowExtraWidgetsTransitions() {
  showExtraWidgetsState->addTransition(moreButton, &QPushButton::toggled, hideExtraWidgetsState);
}

void Dialog::createHideExtraWidgetsTransitions() {
  hideExtraWidgetsState->addTransition(moreButton, &QPushButton::toggled, showExtraWidgetsState);
}
```

对于额外组件状态（`extra widgets state`），我们需要为每个额外组件提供一个几何形状（位置和大小）以及一个字体，并将它们的透明度效果设置为 1.0（完全不透明）。我们还需要设置对话框的最小尺寸，使其足够大以容纳额外组件。所有这一切都在这个方法中实现。

首先，我们计算显示额外组件所需的额外宽度和高度，并创建一个 `QSize` 对象，该对象考虑了这些因素并代表对话框应具有的最小尺寸。我们创建一个 `QRects` 列表，存储每个额外组件的几何形状。一旦完成计算，我们就创建了额外组件状态。然后，对于该状态中的每个额外组件，我们将相应的矩形分配给组件的 `geometry` 属性，并将对话框的 `opacity` 属性 1.0 分配给组件的 `font` 属性。（一如既常，此时不会设置任何属性；它们只在进入相关状态时才会被设置。）最后，我们将对话框的最小尺寸设置为我们计算出的尺寸，以便显示带有所有额外组件的对话框。

```cpp
QSize findDialog::extraSize() const
{
    const Int Width = syntaxLabel->sizeHint().width() +
    syntaxComboBox->sizeHint().width() + (2 * margin);

    const Int Height = wholeWordsCheckbox->sizeHint().height() +
    qMax(syntaxLabel->sizeHint().height(),
    syntaxComboBox->sizeHint().height()) + (2 * margin);

    return QSize(Width, Height);
}
```

此辅助函数通过使用语法标签和语法组合框宽度之和加上某些边距来计算所需的额外宽度，并通过使用全词复选框以及语法标签与语法组合框中较高的者之和（同样加上某些边距）来计算额外高度。

```cpp
void findDialog::createHideExtraWidgetsState()
{
    QRect rect = QRect(buttonBox->x() + (moreButton->width() / 2),
        buttonBox->height() - (moreButton->height() / 2), 1, 1);

    QFont smallFont(font());

    smallFont.setPointSize(1.0);

    hideExtraWidgetsState = new QState(extraStateMachine);

    foreach (QWidget *widget, extraWidgets)
        hideExtraWidgetsState->assignProperty(
            widget, "geometry", rect);
```

# 结合动画与状态机

```cpp
hideExtraWidgetsState->assignProperty(
widget, "font", smallFont);

hideExtraWidgetsState->assignProperty(
widget->graphicsEffect(), "opacity", 0.0);
}

hideExtraWidgetsState->assignProperty(
this, "minimumSize", minimumSizeHint());
```

额外组件状态比显示额外组件简单一点，因为每个额外组件都获得相同的属性值。我们将每个额外组件的 `geometry` 属性设置为位于“更多”按钮中间位置的 1×1 矩形，将 `font` 属性设置为较小字体，并将图形效果的 `opacity` 属性设置为 0.0（完全透明）。最后，我们将对话框的 `minimumSize` 属性设置为其最小尺寸提示值（这正确地没有考虑到额外组件）。

```cpp
const int Duration = 1500;

void findDialog::createExtraWidgetsTransitions()
{
    QSignal *transition =
        hideExtraWidgetsState->addTransition(this,
        SIGNAL(showExtraWidgets()), showExtraWidgetsState);

    createCommonTransitions(transition);

    QPropertyAnimation *animation;

    animation = new QPropertyAnimation(this, "minimumSize");

    animation->setDuration(Duration / 3);

    transition->addAnimation(animation);

    animation = new QPropertyAnimation(this, "size");

    animation->setDuration(Duration / 3);

    QSize size = extraSize();

    size = QSize(qMax(size.width(), width()), height());

    size.setHint(height() + size.height());

    animation->setEndValue(size);

    transition->addAnimation(animation);
}
```

我们创建一个从隐藏额外组件状态到显示额外组件状态的转换，该转换由 `showExtra()` 信号触发。我们还保留了该转换的指针，以便可以使用它来添加动画。

对于这个转换，我们想要控制五个属性：对话框的 `minimumSize` 和 `size`，以及每个额外组件的 `geometry`、`font` 和透明度效果的 `opacity`。

# 第 13 章 动画与状态机框架

对于额外组件，我们将工作交由一个辅助方法处理，因为显示和隐藏额外组件使用了相同的对话框动画。

对于对话框的 `minimumSize` 和 `size` 属性，我们设置了动画，其耗时为执行属性动画所需时间的三分之一（即发生得会更快）。对于 `size` 属性，我们设置了一个足够大的结束值尺寸，以容纳额外组件。

```cpp
void FindDialog::createCommonTransitions(
  QSignal *transition)
{
  QPropertyAnimation *animation;

  foreach (QWidget *widget, extraWidgets) {
    animation = new QPropertyAnimation(widget, "geometry");

    animation->setDuration(Duration);

    transition->addAnimation(animation);

    animation = new QPropertyAnimation(widget, "font");

    animation->setDuration(Duration);

    transition->addAnimation(animation);

    if (QGraphicsEffect *effect =
      static_cast<QGraphicsEffect*>(widget->graphicsEffect())) {
      animation = new QPropertyAnimation(effect, "opacity");

      animation->setDuration(Duration);

      animation->setEasingCurve(QEasingCurve::InOutQuad);

      transition->addAnimation(animation);
    }
  }

  animation = new QPropertyAnimation(this, "minimumSize");

  animation->setDuration(Duration / 3);

  transition->addAnimation(animation);

  animation = new QPropertyAnimation(this, "size");

  animation->setDuration(Duration / 3);

  QSize size = extraSize();

  size = QSize(qMax(size.width(), width()), height());

  size.setHint(height() + size.height());

  animation->setEndValue(size);

  transition->addAnimation(animation);
}
```

无论是显示还是隐藏额外组件，我们使用相同的动画。对于 `geometry` 和 `font` 属性我们使用线性缓（因为我们没有显式设置缓曲线），但对于透明度我们使用 `InOutQuad`，它在开始时缓慢，然后加快，最后再次变慢。

# 结合动画与状态机

```cpp
void FindDialog::hideExtraWidgetsTransitions()
{
    QSignalTransition *transition =
        showExtraWidgetsState->addTransition(this,
        SIGNAL(hideExtraWidgets()), hideExtraWidgetsState);

    createCommonTransitions(transition);

    QPropertyAnimation *animation = new QPropertyAnimation(this,
        "minimumSize");

    animation->setDuration(Duration);

    animation->setEndValue(sizeHint());

    transition->addAnimation(animation);
}
```

从显示额外组件状态到隐藏额外组件状态的转换使用了与相反方向对话框相同的动画。在这里，我们对对话框的 `size` 属性进行动画处理——其时间与组件转换同步，以免尺寸缩小得过快。

正如我们之前提到的，所有属性动画都作用于 `QVariant`，并且相关的属性必须是可写的。对于目前没有支持的 `Variant` 类型，也可以提供自定义插值器。一种方法是子化 `QAnimation(QPropertyAnimation)`；另一种方法是实现一个插值函数，接收类型的开始和结束值并返回插值后的 `Variant`。然后必须使用全局函数 `qRegisterInterpolator` 注册函数。

你可能注意到 Qt 不支持 `QFont` 的插值，但我们仍然成功地将额外组件的属性从一种插值到了默认字体大小。这是通过在 `finddialog.cpp` 文件中放置一个 `fontInterpolator()` 函数，并在 `FindDialog` 的构造函数中注册该函数实现的。
