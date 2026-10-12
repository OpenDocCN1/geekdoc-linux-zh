
## 预定义对话框

Qt 为文件、字体和颜色选择等常见功能提供了一系列静态对话框。由于这些对话框是静态的，因此无需实例化它们。

### QColorDialog

顾名思义，该部件是一个允许用户选择或指定颜色值的对话框。（图 3.7 是 QColorDialog 的灰度屏幕截图。）

![](img/64220583cb3d8a303f33ac97f5433b04_90_0.png)

图 3.7 QColorDialog 部件（灰度显示）

#### 使用示例

```cpp
// Always start the dialog with red as default
QColor face = QColor( "#ff0000" );
// Get a user-defined color
QColor newface = QColorDialog( face, qApp );
// Make sure user didn't cancel-use default if so
if( newface.isValid() == false) newface = face;
```

您不需要实例化此对话框，因为它是模态的并且提供静态方法。典型用法如下：

```cpp
QColor userColor = QColorDialog::getColor();
myLabel->setPalette( QPalette( userColor ) );
```

### QDialog

QDialog 是所有 Qt 对话框的基类。您可以对 QDialog 进行子类化，从而提供几乎任何可以想到的弹出窗口形式，从弹出表单到启动画面。当然，您可以使用 QWidget 实现相同的功能，但 QDialog 增加了适合典型对话框行为的一些方便功能。

QDialog 部件（以及下文讨论的 QSemaphoreDialog）的父子关系会影响对话框在屏幕上的外观。向对话框传递有效的部件父级会使对话框位于父级部件上方居中，而没有父级的对话框会在屏幕本身居中。

以下示例是一个基于 QDialog 的“启动画面”部件。（我不赞同使用启动画面，但承认它们*有时*是必要的。）

```cpp
// Splash.h

#ifndef _SPLASH_H
#define _SPLASH_H

#include <qdialog.h>
#include <qpixmap.h>
#include <qstring.h>
#include <qprogressbar.h>
#include <qlabel.h>

class Splash : public QDialog
{
    Q_OBJECT
public:
    Splash( const QPixmap &p, const char *title,
            const char *cpry, bool pbar=false );

    bool             isProgressSplash( )  { return( isps ); }
    int              progressValue( )      { return( progr ); }

public slots:
    void         setProgressValue( int );
    void         setProgressText( const QString & );

private:
    bool             isps;
    int              progr;
    QProgressBar *pbar;
    QLabel       *plabel;
};

#endif // _SPLASH_H
```

```cpp
// splash.cpp

#include <Splash.h>
#include <qlayout.h>
#include <qlabel.h>
#include <qprogressbar.h>

Splash::Splash( const QPixmap &pix,
                const char *mssg, const char *cpry, bool isp )
: QDialog( 0, "Splash", false,
           WStyle_DialogBorder|WStyle_Customize )
{
    isps = isp;
    progr = 0;

    QVBoxLayout *top = new QVBoxLayout( this, 10 );
    QHBoxLayout *hb = new QHBoxLayout();
    top->addLayout( hb, 5 );
    hb->addSpacing( 10 );

    // Add Pix
    QLabel *l = new QLabel( this );
    l->setPixmap( pix );
    hb->addSpacing( 10 );

    // Add Product name/Main message
    QVBoxLayout *vb = new QVBoxLayout();
    hb->addLayout( vb );
    if(mssg != 0) {
        l = new QLabel( this );
        l->setAlignment( AlignVCenter|AlignHCenter );
        l->setFont( QFont( "helvetica", 18,
                           QFont::Bold,QFont::Italic ) );
        l->setText( mssg );
        vb->addWidget( l, 2 );
    }

    // Add copyright info
    if( cpry != 0) {
        l = new QLabel( this );
        l->setAlignment( AlignVCenter|AlignHCenter );
        l->setText( cpry );
        vb->addWidget( l, 3 );
    }

    // Maybe add progressbar
    if( isps == true) {
        hb = new QHBoxLayout();
        top->addLayout( hb );

        // A text label
        plabel = new QLabel( this );
        plabel->setAlignment( AlignVCenter|AlignRight );
        plabel->setFixedHeight( fontMetrics().height()
                                + 6 );
        hb->addWidget( plabel );

        // A progress bar
        pbar = new QProgressBar( 100, this );
        pbar->setFixedHeight( fontMetrics().height()
                              + 6 );
        pbar->setValue( 0 );
        hb->addWidget( pbar );
    }
    top->activate();
    show();
}

void
Splash::setProgressValue( int v )
{
    if( isps == false) return;
    pbar->setValue( v );
    progr = v;
}

void
Splash::setProgressText( const QString &s )
{
    if( isps == false) return;
    plabel->setText( s );
}

#include <Splash.moc>
```

### QFileDialog

QFileDialog（参见图 3.8）用于允许终端用户选择文件以执行打开或保存功能，或者选择或创建子目录。

![](img/64220583cb3d8a303f33ac97f5433b04_94_0.png)

图 3.8 QFileDialog 部件

这是另一个静态对话框，因此通常以以下方式使用：

#### 使用示例

```cpp
// Get a filename from the user to save to
QString s = QFileDialog::getSaveFileName( "*.txt" );
if(!s.isNull()) { // Save it
    // ...
} // else user cancelled
// ...
```

### QFontDialog

字体对话框（参见图 3.9）用于提示用户选择文本字体和样式。与大多数 Qt 对话框一样，QFontDialog 没有构造函数。典型用法如下：

#### 使用示例

```cpp
// ...
bool ret;
QLabel *l = new QLabel( "Altered Font", this );
QFont f = QFontDialog::getFont( &ret, this );

![](img/64220583cb3d8a303f33ac97f5433b04_95_0.png)

图 3.9 QFontDialog 部件

if ( ret == true ) {
    l->setFont( f );
}
// ...
```

### QInputDialog

此对话框是 Qt 2 中的新增功能。它提供了一系列方便的方法，用于输入单个值，无论是文本字符串、整数、浮点值还是来自组合框的值。图 3.10 是 QInputDialog 的 getText() 对话框示例。

![](img/64220583cb3d8a303f33ac97f5433b04_95_1.png)

图 3.10 QInputDialog::getText() 对话框

以下示例生成了图 3.10 中显示的对话框：

#### 使用示例

```cpp
bool retry = FALSE;
QString svr = QInputDialog::getText( "Enter Hostname",
                                     "Hostname or IP Address:",
                                     "ftp.kahuna-surf.org",
                                     &retry, this );
if( retry == true && !svr.isEmpty() )
    // Deal with a retry attempt
else
    // No hostname or user pressed cancel
```

### QMessageBox

这是 Qt 的标准消息框部件。它由一个对话框框、一个可选的图标、一个对话框标题、一个用于某些文本的标签以及最多三个可自定义标签的按钮组成。

![](img/64220583cb3d8a303f33ac97f5433b04_96_0.png)

它提供了通常的 `warning()`（示例见图 3.11）、`critical()` 和 `information()` 方法，这些方法决定了与您提供的消息框文本一起显示的图标，并且它们非常易于使用：

#### 使用示例

```cpp
QMessageBox::information( this, "Info", "Details" );
```

### QProgressDialog

QProgressDialog（图 3.12）为终端用户提供进度反馈。（参见图 3.12。）您可能希望为耗时较长的操作实现这些反馈。

![](img/64220583cb3d8a303f33ac97f5433b04_97_0.png)

图 3.12 QProgressDialog 部件

#### 使用示例

```cpp
QProgressDialog progress("Copying...", "Cancel", 0, 100);
for (int a=0; a<100; a++)
{
    progress.setProgress(a);
    if (progress.wasCanceled() == true)
        break;
    // Make one copy
    myCopy(a);
}
progress.setProgress(100);
```

### QSemaphoreDialog

这是所有半模态对话框的基类。使用该部件创建的对话框与使用 QDialog 创建的对话框不同，它们没有事件循环，也没有默认按钮的概念。

QSemaphoreDialog 提供的功能远少于 QDialog。因此，子类（如 QProgressDialog）必须提供所有定期更新对话框内容的代码。

### QTabDialog

选项卡对话框（参见图 3.13）提供了一组选项卡式部件。这些部件通常用于在配置对话框中展示一组易于导航的属性页，但它们也可以同样有效地用于其他目的。

通常，您会对 QTabDialog 进行子类化，如下例所示：

```cpp
class SDialog : public QTabDialog
{
    Q_OBJECT
public:
    SDialog(QWidget *p=0, const char *n=0)
    {
    }
protected slots:
    void ok();
    void cancel();
};
```
