
我们只展示了第一个操作的创建，因为大多数操作都遵循相同的模式。异常是静音`jingle`操作，它是可更改的且初始化为未取消。

我们首先确定查找`jingle`和图像的目录。当我们使用路径时（这些路径作为私有变量供其他方法使用），使用Unix风格的路径分隔符，在所有平台上都有效。

`jingle`文件必须位于文件系统中——在本书编写此时它们不能是Qt资源。由于这个原因，我们将应用程序的`jingle`以及为了一致性将图像也存储在文件系统中，而不是将其编译进资源。（我们早些讨论过`QApplication::applicationof()`，33）考虑到此，我们确保应用程序在运行时可以找到`jingle`。

现在我们将查看应用程序提供的支持其打开、播放和停止视频文件、截取和保存以及切换`jingle`静音状态的方法实现。

# 58 第 2 章 音频与视频

```cpp
statusBar()->showMessage(tr("Loaded %1").arg(filename), StatusTimeout());
```

```cpp
movieState = Stopped;
startOrStop(DontReload);
}
```

`QMovie::supportedFormats()`静态方法返回一个`QList<QByteArray>`类型的文件后缀列表——例如`"gif"`，`"png"`。`aqp`(hpp, cpp)模块`AQP::fileNameFilter()`返回一个基于此类列表的`QString`——例如`"Movies (*.gif, *.png)"`——这适合作为过滤器传递给`QFileDialog::getFileName()`函数。

如果用户选择了一个文件，我们设置电影文件名来更新状态栏。然后我们设置电影状态，并调用`startOrStop()`槽立即开始播放电影。`startOrStop()`方法的参数有一个默认值`Reload`，但在这里我们显式设置了`DontReload`，因为我们已经加载了电影。

```cpp
void MainWindow::startOrStop(ReloadMode reloadMode) {
    if (movieState == Stopped) {
        if (reloadMode == Reload) {
            movie->setFileName(movie->fileName());
        }
        movie->start();
        movieState = Playing;
    } else {
        movie->stop();
        movieState = Stopped;
    }
    updateUI();
}
```

如果我们想重放已经加载并播放过的电影，就必须调用`QMovie::fileName()`，因此不需要为新加载的电影调用它。电影根据电影状态的值启动或停止，并在`updateUI()`方法中更新用户界面以反映当前状况。

```cpp
void MainWindow::updateUI() {
    if (movieState == Playing) {
        startOrStopAction->setText(tr("&Stop"));
        startOrStopAction->setIcon(QIcon(imagePath + "/editstop.png"));
    }
    startOrStopAction->setJingleFile(jinglePath + "/editstop.wav");
}
```

### 使用 QSound 和 QMovie

```cpp
else {
    startOrStopAction->setText(tr("&Start"));
    startOrStopAction->setIcon(QIcon(imagePath + "/editstart.png"));
    startOrStopAction->setJingleFile(jingleFile + "/editstart.wav"));
    startOrStopAction->setEnabled(movieState != NoMovie);
    takeSnapshotAction->setEnabled(movieState != NoMovie);
}
```

在此方法中，我们更新`startOrStopAction`提示音的文本、图标和提示音文件，使其成为启动动作；例如，如果应用程序启动——那么启动或停止动作以及快照动作都将被禁用。

```cpp
void MainWindow::takeSnapshot() {
    snapshot = movie->currentPixmap();
    fileSaveAction->setEnabled(!snapshot.isNull());
    snapshotLabel->setPixmap(snapshot);
}
```

当电影加载后（无论是在播放还是停止），用户可以使用`QMovie::currentPixmap()`方法获取当前帧的快照。如果这产生了一个非空`pixmap`（理应如此），则启用保存操作，在任何情况下，我们都会设置快照标签来显示该`pixmap`。

```cpp
void MainWindow::saveFile() {
    if (snapshot.isNull())
        return;
    QString fileFormats = AQP::filenameFilter(tr("Images"),
        QImageWriter::supportedImageFormats());
    QString filename = QFileDialog::getSaveName(this,
        tr("%1 - Save Snapshot"),
        .arg(Application::applicationName()),
        QFileInfo(movie->filename()).absolutePath(), fileFormats);
    if (filename.isEmpty())
        return;
    if (!snapshot.save(filename))
        QMessageBox::warning(this, tr("Error"),
        tr("Failed to save snapshot image"));
    statusBar()->showMessage(tr("Saved %1").arg(filename));
}
```

# 60
# 第 2 章 音频与视频

`StatusTimeout()`

如果有需要保存的快照，我们会弹出一个合适的`QFileDialog`，其过滤器会显示Qt可以写入的`pixmap`图像。如果用户选择了文件名，我们尝试按照给定的名称保存快照，`QPixmap::save()`留出文件格式，以便从文件名的后缀中进行解析。如果保存失败，我们会弹出一个消息框；否则，我们在状态栏中注意到保存成功。（参参见“避免 Qt 的静态便利消息框函数”，以了解为什么在向用户展示消息时，除了Qt的静态`QMessageBox`函数外，我们使用`Q::warning()`和类似的函数。）使用Qt便利函数的另一个优点是它们会在标题栏中放入应用程序名称（使用`QApplication::applicationName()`），因此我们只需要解析标题的其余部分。（对比`QFileDialog::getSave()`和`Q::warning()`的调用。）

```cpp
void MainWindow::muteJintles(bool mute) {
  JingleAction::setMute(mute);
}
```

主窗口构造函数中的动作之一是`flipJinglesAction`，这是一个初始状态为未勾选的切换动作。该动作被添加到菜单和工具栏中，并连接到此槽，以便用户控制是否播放提示音。

虽然`QSound`和`QMovie`对于提供听觉和视觉提示非常有用，但它们都不都不提供复杂的多媒体功能。幸运的是，下一节介绍的`Phonon`多媒体库提供了大量的多媒体功能，我们可以在需要时调用它们。

## Phonon 多媒体框架

`Phonon`多媒体库由`KDE`（'K' 桌面环境）开发者创建，以便为`KDE`编写多媒体更加更加。`Phonon`有两个部分——提供通用多媒体`API`的前端和提供实际多媒体服务的后端。`Qt`的`Phonon`模块提供了对许多`Phonon` `API`的`Qt`风格封装。要使模块可用，在任何想要使用它的`.pro`文件中添加`Qt += multimedia`是必要的。

`Phonon`最重要的功能之一是由于它对多种后端的支持，它可以跨平台使用。在`Linux`上它使用`GStreamer`库，在`Mac OS`上使用`QuickTime`，在`Windows`上使用`DirectX`和`DirectShow`库。使用其他后端也是可能的——例如`VLC`和`MPlayer`后端。

## 避免 Qt 的静态便利消息框

`QMessageBox`类提供了几个静态便利函数，用于弹出带有我们需要的消息和按钮的对话框。然而，`Mac OS X`用户期望它们以`sheet`（工作）的形式出现，而不是对话框。

### 表 2.1 主要声子类

| 类 | 描述 |
| --- | --- |
| `Phonon::AudioOutput` | 一种驱动声卡或耳机的音频汇点媒体节点 |
| `Phonon::Effect` | 一种可以转换音频流的处理器类媒体节点 |
| `Phonon::EffectWidget` | 用于控制效果处理器参数的小部件 |
| `Phonon::MediaNode` | 所有媒体节点类型的基类 |
| `Phonon::MediaObject` | 用于控制多媒体对象播放的媒体节点 |
| `Phonon::MediaSource` | 向多媒体对象源节点提供媒体数据的对象 |
| `Phonon::Path` | 从多媒体对象源到汇点节点的数据路径 |
| `Phonon::SeekSlider` | 用于显示和修改多媒体对象在时间播放位置的小部件 |
| `Phonon::VideoPlayer` | 一种可以加载和播放视频媒体的小部件，并且它会在后台自动处理媒体节点和路径的创建 |
| `Phonon::VideoWidget` | 用于播放视频媒体的小部件 |
| `Phonon::VolumeSlider` | 用于显示和修改多媒体对象音量的小部件 |

(`code.google.com/p/phonon-vlc-player`)。在使用`Qt`时必须安装特定平台的后端——相关说明请见`qt.phonon.com/doc/phonon-overview.html`。*

`Phonon`框架有三种媒体数据源、媒体节点和媒体设备。表示这些对象的类列在表 2.1 中。

媒体数据源由`Phonon::MediaSource`对象表示，这些对象接收一个文件、`URL`或`QIODevice`，并从中检索媒体数据。它们本身并不是媒体节点，只有在传递给多媒体对象源节点时才能使用。

媒体节点分为三种：源节点（不要与数据源混淆）、处理器节点和汇点节点。源节点由`Phonon::MediaObject`对象表示，并提供媒体播放接口。

* 在编写本文时，绑定 `Windows DirectShow` 后端仅在在使用商业编译器时受支持。

`Phonon::MediaObjects`有一个当前的`Phonon::MediaSource`对象，还可以持有一个其他媒体源对象的队列，准备在每个对象完成后一个接一个地播放。

来自`Phonon::MediaObject`的输出必须通过一个或多个路径传输到汇点。路径由`Phonon::Path`对象表示，并且必须有一个源节点（一个`Phonon::MediaObject`）和一个汇点节点（例如`Phonon::AudioOutput`或`Phonon::VideoWidget`）。路径可以是定向的，也可以包含中间处理器节点以提供特殊效果。

`Phonon`模块不支持直接操作媒体流中的数据。然而，它提供了一种间接操作音频流的手段：效果处理器。这些处理器（`Phonon::Effect`）可以被添加到源节点和汇点之间的路径上，它们在那里转换从一个流向另一个流的数据。可用的效果取决于`Phonon`后端，并可以通过`Phonon::BackendCapabilities::availableAudioEffects()`函数获取。效果可能包括放大、在立体声声场中定位流、均衡化或重采样。

要应用效果，我们为想要的效果创建一个新的`Phonon::Effect`实例。然后，假设我们保留了`Phonon::createPath()`函数返回的`Phonon::Path`指针，我们调用`Phonon::Path::insertEffect()`，并将我们创建的`Phonon::Effect`传递通过。

![](img/74b321c00e6b987639de429f0799cff9_80_0.png)

> 图 2.2 Phonon 架构

汇点节点是数据最终发送到物理输出设备的地方，例如声卡、耳机或视频小部件，它们由`Phonon::AudioOutput`媒体节点表示，或者由同样作为媒体节点的`Phonon::VideoPlayer`或`Phonon::VideoWidget`小部件表示。这些关系如图 2.2 所示。

现在我们已经熟悉了`Phonon`框架在理论上是如何工作的，我们将看看如何在实践中使用它。在接下来的两个小节中，我们将回顾两个示例，一个是播放音乐，另一个是播放视频（包括如果有音轨的话）。

## 播放音乐

本小节回顾并在图 2.3 中所示的“播放音乐”示例 (`playmusic`) 展示了如何创建一个音乐播放应用程序。此类应用程序

![](img/74b321c00e6b987639de429f0799cff9_81_0.png)

**图 2.3** 启动时的播放音乐应用程序和音乐目录

通常使用播放列表、数据库或文件系统来组织曲目；当程序启动时，它有一个空白的中央区域并邀请用户选择音乐目录。一旦选择了目录，程序将遍历目录中的所有音乐文件，递归进入任何子目录，并填充一个`QTreeWidgetItem`，包含艺术家、专辑和曲目名称，以及每个曲目的时长。

用户可以使用鼠标或键盘导航到特定曲目，或者使用播放/暂停按钮或按下空格键来播放或暂停曲目。当曲目结束时，会自动播放下一个曲目。

```cpp
const int name = Qt::UserRole;
const int OneSecond = 1000;

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent), nextItem(0)
{
    playIcon = QIcon(":/play.png");
    pauseIcon = QIcon(":pause.png");
    mediaObject = new Phonon::MediaObject(this);
    mediaObject->setTimeInterval(OneSecond);
    audioOutput = new Phonon::AudioOutput(Phonon::MusicCategory, this);
    Phonon::createPath(mediaObject, audioOutput);
    createActions();
    createToolbar();
    createWidgets();
    createLayout();
    createConnections();
    setWindowTitle(QApplication::applicationName());
}
```

`nextItem`是代表下一个播放曲目的`QTreeWidgetItem`。在用户选择曲目时触发。树部件项可以有多个列数据，每列都可以持有`QVariant`列表作为数据。稍后我们将看到，我们使用此特性为代表曲目的的小部件在第一列的用户数据（即列 0）中存储文件名，使用`Filename`常量作为项的索引。

私有的`mediaObject`用于播放用户选择的任何曲目，声音数据发送到音频输出汇点。对于音频输出，我们必须指定使用的声音类别。该类别用于标识音频输出应该去哪里。例如，对于使用`VoIP`（IP）的电话应用程序，声音将发送到用户的耳机，而音乐播放器的声音将发送到声卡。

一旦有了媒体对象和输出汇点，我们可以创建一个路径将它们连接，由于我们不在路径上添加任何处理器来实现特殊效果，因此我们不保留创建的路径引用。此外，我们告诉媒体对象每秒发射一次`tick()`信号——我们将使用此来更新显示当前时间位置的`LCD`数字部件。

我们将不会查看`createActions()`、`createToolbar()`和`createLayout()`方法，因为它们不包含意外的内容。但我们将通过调用`createWidgets()`方法查看如何创建`Phonon`小部件，还将查看`createConnections()`。

```cpp
void MainWindow::createWidgets() {
  seekSlider = new Phonon::SeekSlider(this);
  seekSlider->setToolTip(tr("Playback Position"));
}
```

## Phonon 多媒体框架

```cpp
```
