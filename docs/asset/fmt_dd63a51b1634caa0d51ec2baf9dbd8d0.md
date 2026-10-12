
```cpp
KTMainWindow *KPenguin = new KMainWindow();

KPenguin->setGeometry(100, 20, 150, 100);

KIntegerLine *KLine = new KIntegerLine(KPenguin);

KLine->setGeometry(10, 10, 70, 50);

App.setMainWidget(KPenguin);

KPenguin->show();

return App.exec();

}
```

10-24 显示了该程序的输出。

![](img/859df50987094e32dd2f5bb576f82bce_354_0.png)

## 编辑框发出的信号

`QLineEdit` 和 `QMultiLineEdit` 输出两个信号：

- `returnPressed()`
- `textChanged()`

`returnPressed()` 信号在按下 `Enter` 或 `Return` 键时由 `QLineEdit` 和 `QMultiLineEdit` 发出。对于 `QMultiLineEdit`，会发出 `returnPressed()` 信号。`textChanged()` 信号在文本更改时发出。

# 334 第 10 章 + 图形用户界面设计

`QDoubleValidator` 接受 `Bottom` 和 `Top` 作为有效浮点数的范围。`decimals` 决定了小数点后数字的位数。这对于 `QIntValidator` 也是如此。`Bottom` 和 `Top` 定义了有效整数的范围。这两个类都定义了设置范围并返回这些值的方法：

```cpp
setRange() // 设置验证器的范围
bottom() // 返回范围的下限
top() // 返回范围的上限
decimals() // 返回小数点后的数字位数
decimals() // QDoubleValidator 的小数位数
```

列表 10-6 显示了将 `QIntValidator` 用于单行编辑框的示例。

> 列表 10-6：一个为 `QLineEdit` 对象使用 `QIntValidator` 的程序

```cpp
// 列表 10-6
// 为 QLineEdit 对象使用 QIntValidator 
#include <application.h>
#include <widget.h>
#include <qlineedit.h>
#include <qvalidator.h>

int main(int argc, char *argv[]) {
  QApplication App(argc, argv);

  QWidget *Window = new QWidget();

  QIntValidator *Validator = new QIntValidator(0, 9, Window);

  Window->setGeometry(100, 200, 100, 100);

  QLineEdit *LineEdit = new QLineEdit(Window);

  LineEdit->setGeometry(10, 20, 100, 30);

  LineEdit->setValidator(Validator);

  App.setMainWindow(Window);

  Window->show();

  return App.exec();

}
```

创建了一个范围为 0–9 的 `QIntValidator` 对象 `Validator`。它被传递给 `QLineEdit` 对象 `LineEdit`。用户无法在编辑框中输入任何字符。

# 第 10 章 ♦ 图形用户界面设计 335

验证器只会过滤字符，但它不会验证接受的数据。你必须根据想要输入该框的类型来确定什么是接受的。`QValidator` 有两个可以由派生类重新实现的虚方法：

```cpp
virtual QValidator::State QValidator::validate(QString &Input, int &Pos)
virtual void QValidator::fixup(QString &Input, int &Pos)
```
