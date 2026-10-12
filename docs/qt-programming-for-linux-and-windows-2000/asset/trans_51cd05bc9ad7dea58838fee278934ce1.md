
## PartNum.cpp

```cpp
PartNum::~PartNum()
{
}

void
PartNum::verify( const QString &s )
{

    static bool busy = false;
    char bp[6];  // OK-range invalid for 118n
    int i;

    if(busy == true) return;
    memset( bp, 0, 6);
    strncpy(bp, s, 5);
    if(strlen(s) > 5) {

        busy = true;
        setText( bp );
        busy = false;
    }
    if(bp[0] >= 'a' && bp[0] <= 'z') {
        bp[0] = toupper(bp[0]);
        busy = true;
        setText( bp );
        busy = false;
    }
    if(bp[0] >= 'A' && bp[0] <= 'Z') {
        for(i=1;i<5;i++) {
            if(!isdigit(bp[i])) break;
        }
        if(i == 5) {
            if(_valid == false) {
                _valid = true;
                emit valid( _valid );
            }
        }
        return;
    } else {
        bp[i] = '\0';
        busy = true;
        setText( bp );
        busy = false;
    }
    }
    if(_valid == true) {
        _valid = false;
        emit valid( _valid );
    }
    return;
}

#include <PartNum.moc>
```

验证例程中的 busy 标志旨在防止递归（以及随之而来的栈溢出）。当您通过调用 set(Text) 方法让插槽调用自身（如验证例程所做的那样）时，就会发生这种情况。

以下是对 QLineEdit 的一个非常有用且可复用的修改，它为鼠标右键提供了一个弹出菜单。该菜单提供了一些常见的剪贴板或剪切缓冲区操作，PC 用户会从像 Office 2000 和其他 Microsoft 产品中熟悉这些操作。提供的功能包括复制、粘贴、剪切、全选、清空、粘贴，以及全选和复制。请注意，相同的修改也可以应用于 QMultiLineEdit 的子类。Qt 2.1 及以上版本已具备此功能，因此这种修改可能不再是必需的。

## LineEdit.h

```cpp
#ifndef _LINEEDIT_H
#define _LINEEDIT_H

#include <qlineedit.h>
#include <qevent.h>
#include <qpopupmenu.h>

class LineEdit : public QLineEdit
{
 Q_OBJECT
public:
 LineEdit( QWidget *p=0, const char *n=0 );

protected slots:
 virtual void mousePressEvent( QMouseEvent * );
 virtual void doCut();
 virtual void doCopy();
 virtual void doPaste();
 virtual void doSelect();
 virtual void doClear();
 virtual void doClearPaste();
 virtual void doSelectCopy();

private:
 int pmid[7];
 QPopupMenu *pop;
};

#endif // _LINEEDIT_H
```

## LineEdit.cpp

```cpp
#include <LineEdit.h>

LineEdit::LineEdit( QWidget *parent,
 const char *name )
 : QLineEdit( parent, name )
{
 pop = new QPopupMenu();
 pmid[0] = pop->insertItem( "Cut", this,
                  SLOT(doCut()) );
pmid[1] = pop->insertItem( "Copy", this,
                  SLOT(doCopy()) );
pmid[2] = pop->insertItem( "Paste", this,
                  SLOT(doPaste()) );
pmid[3] = pop->insertItem( "Clear All", this,
                  SLOT(doClear()) );
pop->insertSeparator();
pmid[4] = pop->insertItem( "Select All",
                  this, SLOT(doSelect()) );
pop->insertSeparator();
pmid[5] = pop->insertItem(
                  "Select All & Copy", this,
                  SLOT(doSelectCopy()) );
pmid[6] = pop->insertItem(
                  "Clear All & Paste", this,
                  SLOT(doClearPaste()) );
}

void
LineEdit::mousePressEvent( QMouseEvent *e )
{
    if(e->button() != RightButton) {
        QLineEdit::mousePressEvent( e );
        return;
    }
    int n = strlen(text());
    pop->setItemEnabled( pmid[0],
                    hasMarkedText() );
    pop->setItemEnabled( pmid[1],
                    hasMarkedText() );
    pop->setItemEnabled( pmid[3],
                    (n > 0) ? true : false );
    pop->popup( e->globalPos() );
}

void
LineEdit::doCopy()
{
    copy();
}

void
LineEdit::doCut()
{
    cut();
}

void
LineEdit::doPaste()
{
    paste();
}

void
LineEdit::doSelect()
{
    selectAll();
}

void
LineEdit::doClear()
{
    setText( "" );
}

void
LineEdit::doClearPaste()
{
    setText( "" );
    paste();
}

void
LineEdit::doSelectCopy()
{
    selectAll();
    copy();
}

#include <LineEdit.moc>
```

这最后一个修改提供了在 QLineEdit 控件获得键盘焦点时，选择并高亮显示其现有内容的功能：

## LineEdit.h

```cpp
#ifndef LINEEDIT_H
#define LINEEDIT_H
#include <qevent.h>
#include <qlineedit.h>

class LineEdit : public QLineEdit
{
    Q_OBJECT
public:
    LineEdit( QWidget *parent=0,
        const char *name=0 );

protected slots:
    void    focusInEvent( QFocusEvent * );
    void    focusOutEvent( QFocusEvent * );
}

#endif
```

## LineEdit.cpp

```cpp
#include <LineEdit.h>

LineEdit::LineEdit( QWidget *parent,
		 const char *name )
	: QLineEdit( parent, name )
{
}

void
LineEdit::focusInEvent( QFocusEvent *e )
{
	QLineEdit::focusInEvent( e );
	selectAll();
	repaint( false );
}

void
LineEdit::focusOutEvent( QFocusEvent *e )
{
	QLineEdit::focusOutEvent( e );
	setSelection( 0, 0 );
	repaint( false );
}

#include <LineEdit.moc>
```

# 第 3 章 用户交互对象

**QMultiLineEdit** 这是一个非常基本的文本编辑器控件。虽然它提供了最简单文本编辑所需的大多数底层功能，但它缺乏大多数编辑任务所需的高级功能。图 3.28 展示了一个带有 QLabel 的 QMultiLineEdit 控件示例。

![](img/64220583cb3d8a303f33ac97f5433b04_122_0.png)

图 3.28 一个 QLabel 控件和一个 QMultiLineEdit 控件

### 可能的实例化

```cpp
QMultiLineEdit *me = new QMultiLineEdit( this );
```

### 使用示例

```cpp
me->setText( "The quick brown fox\njumped over the"
"slow lazy dog" );
```

一个非常简单的增强功能是添加在 QLineEdit 讨论中描述的剪切和粘贴菜单。

# 数值输入

有时应用程序需要从用户处获取数值。您可以提供一个标准的行编辑框并分配一个验证器，使其仅接受数字，但即使有工具提示帮助，这也不总是直观的。多年来，人们已经设计并测试了其他方法，将来还会有更多。以下是 Qt 提供的控件。

## QSlider

QSlider（图 3.29）提供了一种直观的方式来获取用户数值输入。边界检查通过 QSlider 的 QRangControl 父类提供。

![](img/64220583cb3d8a303f33ac97f5433b04_123_0.png)

图 3.29 QSlider 控件

### 可能的实例化

```cpp
QSlider *s = new QSlider( QSlider::Horizontal, this );
```

### 使用示例

```cpp
QSlider *s = new QSlider( QSlider::Horizontal, this );
s->setRange( -180, 180 );
s->setValue( 0 );
```

## QSpinBox

旋转框（图 3.30）是一个接受（通常）整数数据的文本字段。它包含一对按钮，允许用户增加或减少显示的值。步长和范围是可以编程的。

![](img/64220583cb3d8a303f33ac97f5433b04_123_1.png)

图 3.30 QSpinBox 控件

### 可能的实例化

```cpp
QSpinBox *sb = new QSpinBox( this );
```

### 使用示例

```cpp
// Create a spinbox for invoice payment
// period allowance.
// Minimum = 10, Maximum = 90, step = 10
// Default to COD, (-1 from sb->value())
QSpinBox *sb = new QSpinBox( 10, 90, 10, this );
sb->setSuffix( " days net" );
sb->setSpecialText( "C.O.D." );
```

提供了方法来重新解释非整数值的值类型，但最终值必须被评估为整数。要对 QSpinBox 的功能进行重大更改，通常需要重新实现该控件。光盘上包含了一个基于时间 t 值工作的旋转框示例。

# 滚动

与其他所有 GUI 工具包一样，Qt 提供了滚动条。它们比其他工具包实现更容易使用。

## QScrollBar

滚动条（图 3.31）是一种常见的图形控件，允许用户滚动或平移一个可能被裁剪的视图，该视图可能是一个非常大的视觉组件。QScrollBar 控件提供了一个功能丰富的实现。

![](img/64220583cb3d8a303f33ac97f5433b04_124_0.png)

**图 3.31** 带有垂直和水平 QScrollBar 控件的 QLineEdit 控件

