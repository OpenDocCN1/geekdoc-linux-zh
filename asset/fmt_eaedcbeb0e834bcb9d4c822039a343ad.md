
```cpp
    QDropSitePrivate *d;

};
```

每个选择成为投放点的对象都必须指定当用户在一定范围内拖动对象时应该如何表现。例如，当对象进入投放点时系统会蜂鸣吗？当对象进入投放点时什么图标会发生变化？当用户在投放点释放对象时会发生什么？文件会被复制、删除、压缩、打印、排序等等？列表 3-1 包含了 `QDropSite` 方法实现的源码。

## 列表 3-1：`QDropSite` 方法实现的源码

```cpp
// 列表 3-1
// QDropSite 方法实现
QDropSite::QDropSite(QWidget *parent)
{
    d = new QDropSitePrivate(parent, this);
    parent->setAcceptDrops(TRUE);
}

QDropSite::~QDropSite()
{
    delete d; // 并不需要
}

void QDropSite::dragEnterEvent(QDragEnterEvent*)
{
}

void QDropSite::dragMoveEvent(QDragMoveEvent*)
{
}

void QDropSite::dragLeaveEvent(QDragLeaveEvent*)
{
}

void QDropSite::dropEvent(QDropEvent*)
{}
```

注意列表 3.1，`dragLeaveEvent()`、`dragEnterEvent()` 和 `dragMoveEvent()` 不包含任何代码。如果你声明了一个 `QDropSite` 的对象并调用其中任何一个方法，什么都不会发生，因为你必须使用继承来定义这些方法。

你声明如下类类：

```cpp
class penguin_dropsite : public QDropSite {
public:
    penguin_dropsite(QWidget *X);
    void dragEnterEvent(QDragEnterEvent*);
    void dragMoveEvent(QDragMoveEvent*);
    void dragLeaveEvent(QDragLeaveEvent*);
    void dropEvent(QDropEvent*);
};
```

## 第 3 章 面向对象编程预备

当你在类中重写 `drag()` 和 `drop()` 方法时。`QDropSite` 类仅为派生类提供模式。有时，这些模式包含空方法，你必须在派生类中定义它们。在其他情况下，类声明包含如下方法：

```cpp
virtual void dragEnterEvent(QEvent*) = 0;
```

这种方法被称为纯虚函数。任何包含纯虚函数的类都是抽象类。要使用抽象类，你必须从它派生出一个新类，并为任何纯虚方法提供定义。抽象类强制要求你重写虚方法。在 `QDropSite` 类中，虚方法不是纯的。你可以声明一个 `QDropSite` 实例而不产生编译错误。然而，该实例将无法正常工作，因为重要的成员没有实现。如果 `QDropSite` 类声明为：

```cpp
class Q_EXPORT QDropSite {
public:
    QDropSite(QWidget *parent = nullptr);
    virtual ~QDropSite();
    virtual void dragEnterEvent(QDragEvent*) = 0;
    virtual void dragMoveEvent(QDragEvent*) = 0;
    virtual void dragLeaveEvent(QDragEvent*) = 0;
    virtual void dropEvent(QDropEvent*) = 0;
private:
    QDropSitePrivate *d;
};
```
