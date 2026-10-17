
```cpp
class CursorPlugin : public QImageIOPlugin
public:
    QStringList keys() const;
    Capabilities capabilities(QIODevice *device,
                             const QByteArray &format) const;
    QImageIOHandler *create(QIODevice *device,
                            const QByteArray &format) const;
```

`keys()`函数返回插件支持的图像格式列表。`capabilities()`和`create()`函数的`format`参数假设具有该列表中的值。

## 使用插件扩展 Qt

```cpp
QString CursorPlugin::keys() const
{
    return QString() << "cur";
}
```

我们的插件只支持一种图像格式，因此它返回一个只包含一个名称的列表。理想情况下，该名称应该是该格式使用的文件扩展名。在处理具有多个扩展名的格式（例如 JPEG 的 `.jpg` 和 `.jpeg`）时，我们可以为同一个格式返回一个包含多个条目的列表，每个目的对应一个扩展名。

```cpp
QImagePlugin::Capabilities
CursorPlugin::capabilities(QIODevice *device,
    const QByteArray &format) const
{
    if (format == "cur")
        return CanRead;

    if (format.isEmpty()) {
        CursorHandler handler;
        handler.setDevice(device);
        if (handler.canRead())
            return CanRead;
    }

    return 0;
}
```

`capabilities()`函数返回图像处理器针对给定图像格式的能力。共有三种能力（`CanRead`、`CanReadIncremental`），返回值是这些适用能力的位或运算结果。

如果格式是 `"cur"`，我们的实现返回`CanRead`。如果没有给出格式，我们创建一个光标处理器并检查它是否有能力从给定的设备读取数据。`canRead()`函数仅查看数据，检查它是否能识别该格式，而不改变指针。能力为 0 表示该处理器无法读取或写入该文件。

```cpp
QHandler *CursorPlugin::create(QIODevice *device,
    const QByteArray &format) const
{
    CursorHandler *handler = new CursorHandler;
    handler->setDevice(device);
    handler->setFormat(format);
    return handler;
}
```

当文件被打开时（例如通过`QImageReader`），插件封装器的`create()`函数将带有设备指针和作为格式的 `"cur"` 被被调用。我们创建了一个`CursorHandler`实例，并使用指定的设备和格式对其进行设置。调用者将拥有该处理器的所有权，并在不再需要时将其删除。如果需要读取多个文件，则会为每个文件创建一个新的处理器。

## 19. 创建插件

```cpp
Q_EXPORT_PLUGIN2(cursorplugin, CursorPlugin)
```

在 `.cpp` 文件的末尾，我们使用`Q_EXPORT_PLUGIN2()`宏来确保插件被 Qt 识别。第一个参数是我们想要给插件的任意名称。第二个参数是插件的名称。

继承`QImagePlugin`是简单的。插件的实际工作在处理器（handler）中完成。图像格式处理器必须继承`QImageIOHandler`并实现其部分或全部公共函数。让我们从头文件开始：

```cpp
class CursorHandler : public QImageIOHandler
{
public:
    CursorHandler();
    bool canRead() const;
    bool read(QImage *image);
    bool jumpToNextImage();
    int currentImageNumber() const;
    int itemCount() const;

private:
    enum State { BeforeHeader, BeforeImage, AfterImage, Error };

    void readHeaderNecessary() const;
    void QArray readBitmap(int width, int height, QDataStream &stream) const;
    void enterErrorState() const;

    mutable State state;
    mutable int currentImageNo;
    mutable int numImages;
};
```

所有公共函数的签名都是固定的。我们省略了只读处理器不需要实现的几个函数，特别是`write()`。成员变量使用`mutable`关键字声明，因为它们在 const 函数内部被修改了。

```cpp
CursorHandler::CursorHandler()
{
    state = BeforeHeader;
    currentImageNo = 0;
    numImages = 0;
}
```

当处理器构造时，我们首先设置它的状态。我们将当前图像编号设置为第一个。由于我们将`numImages`设置为 0，这很清楚还没有图像。

```cpp
bool CursorHandler::canRead() const
{
    if (state == BeforeHeader) {
        return device()->peek(4) == QByteArray("0\0\2\0", 4);
    } else {
        return state != Error;
    }
}
```

可以随时判断图像处理器是否可以从设备读取更多数据。如果该函数在读取任何数据之前调用，且我们仍处于`BeforeHeader`状态，我们会检查识别 Windows 文件的特定签名。`QIODevice::peek()`读取前四个字节而不改变设备的文件指针。如果之后调用`canRead()`，除非发生错误否则返回 true。

```cpp
int CursorHandler::currentImageNumber() const
{
    return currentImageNo;
}
```

此函数返回设备指针所在位置的光标编号。

一旦处理器构造完成，用户可以按顺序调用它的任何公共函数。如果我们假设只能顺序读取，就会出现问题，因此我们需要在执行其他操作之前读取文件头。通过在依赖文件头的函数中调用`readHeaderIfNecessary()`函数来解决这个问题。

```cpp
int CursorHandler::imageCount() const
{
    readHeaderIfNecessary();
    return numImages;
}
```

此函数返回文件中的图像数量。对于一个没有发生读取错误的有效文件，它将返回至少一个计数。

| Field | Type | Description |
| :--- | :--- | :--- |
| reserved | uint16 | 预留 (0x00) |
| type | uint16 | 类型 (0x00) |
| size | uint32 | 图像数量 |
| width | uint32 | 图像宽度 |
| height | uint32 | 图像高度 |
| planes | uint16 | 平数 |
| compression | uint16 | 像素位 |

```cpp
bool CursorHandler::read(QImage *image)
{
    readHeaderIfNecessary();
    if (state != BeforeImage)
        return false;
    // 此实现非常复杂，为了代码片段的简洁已省略
    // 但它将处理像素数据的提取。
    return true;
}
```

## 406 19. 创建插件

在不知道原始背景像素颜色的情况下。作为替代，我们使用半透明的灰色（0x7F7F7F7F）。

```cpp
++currentImageNo;
if (currentImageNo == numImages)
    state = AfterLastImage;
return true;
```

一旦我们完成了图像读取，我们就会更新当前图像编号，如果达到了最后一张图像，则更新状态。在函数结束时，设备将定位到下一张图像或位于文件的末尾。

```cpp
bool CursorHandler::jumpToNextImage()
{
    QImage image;
    return read(&image);
}
```

`jumpToNextImage()`函数用于跳过一张图像。为了简单起见，我们调用`read()`并忽略生成的`QImage`。更高效的实现将可以使用存储在`.cur`文件头中的信息，直接跳转到文件中正确的偏移量。

```cpp
void CursorHandler::readIfNecessary() const
{
    if (state != BeforeHeader)
        return;

    quint16 reserved;
    quint16 type;
    quint16 count;

    QDataStream in(device, QDataStream::LittleEndian);

    in >> reserved >> type >> count;
    in.skipRawData(16, count);

    if (in.status() != QDataStream::Ok || reserved != 0
        || type != 2 || count == 0) {
            enterErrorState();
            return;
        }

    state = BeforeImage;
    currentImageNo = 0;
    numImages = int(count);
}
```

`readIfNecessary()`私有函数从`imageCount()`和`read()`调用。如果头已经读取，状态将不是`BeforeHeader`，我们立即返回。否则，我们在设备上打开一个数据流，读取一些通用数据（包括文件中光标的数量），并将状态设置为`BeforeImage`。在结束时，设备的文件指针被定位在第一张图像之前。

```cpp
void CursorHandler::onErrorState() const
{
    state = Error;
    currentImageNo = 0;
    numImages = 0;
}
```

如果发生错误，我们假设没有有效的图像并将状态设置为`Error`。一旦进入`Error`状态，处理器的状态就无法改变。

```cpp
QByteArray CursorHandler::readBitmap(int width, int height, QDataStream &in) const
{
    QByteArray bitmap(width * height);
    uint8 byte;
    uint32 word;

    for (int i = 0; i < height; ++i) {
        for (int j = 0; j < width; ++j) {
            if ((j % 2) == 0) {
                word = 0;
                for (int k = 0; k < 4; ++k) {
                    in >> byte;
                    word = (word << 8) | byte;
                }
            }
            bitmap.setBit((height - i - 1) * width + j, word & 0x80000000);
        }
    }
    return bitmap;
}
```

`readBitmap()`函数用于读取光标的 AND 和 XOR 掩码。这些掩码具有不的特征。首先，它们从下到上存储行，而不是更常见的从上到下方法。其次，数据的端序似乎与 `.cur` 文件中其他地方使用的相反。鉴于此，我们必须在`setBit()`调用中反转 y 坐标，并且逐个读取掩码值，通过位移和掩码操作来提取它们的正确值。

这标志着`CursorHandler`图像格式插件的实现。其他图像格式的插件将遵循相同的模式，尽管某些插件可能会实现更多的`QImageHandler` API，特别是用于写入图像的函数。其他类型的插件（例如编码器或数据库驱动程序）遵循相同的模式，即有一个插件包装器来提供应用程序可以使用的通用 API，以及一个处理程序来提供底层功能。

## 408 19. 创建插件

应用程序插件的 `.pro` 文件不同，因此我们以它结尾：

```pro
TEMPLATE      = lib
CONFIG        += plugin
HEADERS       = cursorhandler.h \
               cursorplugin.h
SOURCES       = cursorhandler.cpp \
               cursorplugin.cpp
DESTDIR       = $(QTDIR)/plugins/imageformats
```

默认情况下，`.pro`文件使用 app 模板，但在这里我们必须指定`lib`，因为插件是一个库，而不是一个独立的应用程序。`DESTDIR`指定了插件应该存放的目录。Qt 插件必须放在 Qt 安装的相应子目录中，如果你的插件提供了新的图像格式，我们将其放在`plugins/imageformats`。目录名称和插件类型的列表可以在 http://doc.qt.com/4/plugins.html 获取。对于此示例，`QTDIR`环境变量设置为 Qt 安装的目录。发布模式和调试模式下的 Qt 插件是不同的，因此在 `.pro` 文件中指定使用哪一个是明智的——通过添加行：

```pro
CONFIG        += release
```

使用 Qt 插件的应用程序必须与其想要使用的插件一起部署。Qt 插件必须放在特定的子目录下，例如`imageformats`。Qt 应用程序在应用程序可执行文件所在的目录搜索插件，因此如果我们想在不同的目录部署插件，可以使用`QCoreApplication::addLibraryPath()`扩展插件搜索路径。

## 使应用程序感知插件

应用程序是一个动态库，包含一个或多个接口。接口是一个由纯虚定义的类。应用程序与插件之间的通信通过其接口完成。在本节中，我们将关注如何使用插件，并在下一节中展示如何实现插件。插件是由插件提供的，我们可以认为这个列表是键。

**图 19.3.** 应用程序定义了接口：

```cpp
class TextArtInterface {
public:
    virtual TextArtInterface() = 0;
    virtual QStringList listEffects() const = 0;
    virtual QPixmap applyEffect(const QString &font,
                                 const QSize &size,
                                 const QPen &pen,
                                 const QBrush &brush) = 0;
};

Q_DECLARE_INTERFACE(TextArtInterface, "com.qt.TextArt/1.0")
```

接口通常声明一个虚析构函数、一个返回`QStringList`的函数。每当我们更改接口（例如通过添加虚函数或更改现有函数的签名），必须记住增加版本号；否则应用程序在访问过时的插件可能会崩溃。

## 410 19. 创建插件

应用程序实现在名为`TextArtDialog`的类中。我们将只显示与插件相关的代码。让我们从构造函数开始：
