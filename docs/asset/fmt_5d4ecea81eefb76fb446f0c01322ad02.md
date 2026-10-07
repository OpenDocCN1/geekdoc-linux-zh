
另一个是图形原语不同：Quartz 使用填充和描边的贝塞尔曲线路径，这些路径通过昂贵的细分（tessellated）转换为图形硬件使用并通过 API 暴露的三角形。如果它们是形状，这种转换成本将更容易分摊到多次使用中，但 API 并没有真正提供这种支持。

## 频繁通信会减慢安装速度

一项产生意外结果的调查是研究了新 Mac OS 版本中安装程序神秘变慢的问题。该安装程序正在安装数千个小文件，并且之前的表现符合预期。在新版本中，安装程序变慢了七倍，几乎增加了一个数量级。I/O 速率远低于磁盘子系统所支持的，CPU 占用率可以忽略不计，因此似乎没有实际瓶颈可以解释性能的下降。

## 显示限制（The Display Throttle）

在反复苦思和使用工具之后，发现罪祸首首是安装程序提供的状态更新。它显示所安装的每一个文件的名称，为了确保用户有机会看到这每一个文件名，它在显示每个名称后都会刷新屏幕。这种让用户随时了解进度的热忱触碰了 Mac OS X 图形子系统内部的节流机制，该机制将图形更新限制在接近刷新率的水平（现在是某种任意的 60 Hz）。尝试更频繁地刷新屏幕只会阻塞你的程序，如示例 16.1 所示。

## 第 16 章 图形与 UI：陷阱与技巧

### 示例 16.1 以 60 Hz 运行

```swift
import Cocoa

class AppController: NSObject, NSApplicationDelegate {
    var mainWindow: NSWindow?

    func applicationDidFinishLaunching(n: NSNotification) {
        let window = NSWindow(CGRect(0, 0, 320, 200),
                              styleMask: NSTitledWindowMask,
                              backing: NSBackingStoreType.Buffered,
                              defer: false)

        window.orderFrontRegardless()
        self.mainWindow = window
    }

    NSApp.activateIgnoringOtherApps(true)
    dispatch_async(dispatch_get_main_queue() {
        for i in 1...60 {
            self.drawSomething(i)
        }
        NSApp.terminate(true)
    })

    func drawSomething(i: Int) {
        let window=self.mainWindow!
        window.contentView?.lockFocus()
        NSColor.redColor().fill(CGRect(10, 10, 200, 120))
        let labels=NSString(i)
        let label=NSString=labels
        NSColor.blackColor().set()
        label.drawAt(CGPoint(x:20,y:20), withAttributes:nil)
        window.contentView?.unlockFocus()
        window.flushWindow()
    }
}

let app = NSApplication.sharedApplication()
let controller = AppController()
app.delegate = controller

NSApp.run()
```

在我的 8 核 Mac 上运行这个带有 600 次显示循环的程序，耗时恰好是 10.0 秒，与我的 MacBook Pro 上的情况相同，且两个系统的 CPU 空闲率都在 90% 以上。

注意 Quartz 足够智能，可以判断是否存在任何绘制操作，因此在紧凑循环中调用 `flushWindow()` 会立即返回，因为在那种情况下它并没有尝试刷新。不过，你确实需要画一些东西，尽管它并不非得是不同的。

### 处理显示限制

虽然有绕过显示限制的方法，但使用 OpenGL 的游戏可以获得更高的刷新率，可能将这一教训记在心子里更好：状态更新发生的频率可以比用户关心的频率要高得多。例如，我通过其方法测量了一个 `NSUrlSessionDataObject`，当通过 G-bit/s 的 DSL 线路下载时，它每秒给了我 273 次状态更新。

我不仅确信用户不在乎每秒多知道 273 次下载状态——显然不关——你实际上能够读取到一个刷新如此频繁的字节计数。对于字节计数，一秒可能足够了，而进度条如果以更高的频率（大约每秒 10 次）更新，可能会稍微平滑一些。

到目前为止我有三种避免过度 UI 刷新的技巧，其中两种实际上是有效的。第一种技术对于本质上持续的进度监控（例如进度监控）非常好，即使用一个运行在 10 Hz 左右的定时器来查询进度并更新显示。第二种技术是更新批处理（update-request batching），它避免了显式的定时器但难以管理。实现批处理的一种方法是存储更新并在稍后时间发送，例如 0.1 秒。

第三种技术我曾认为使用 `performSelector:afterDelay:` 并取消之前的请求是聪明的，事实上我见过很多这种技术。遗憾的是，它无效。

### 今天的安装程序与进度报告

考虑到这个问题的严重性，你可能认为它是罕见的，且不再发生了。你一直认为——2016 年有报道称，开启进度条时节点管理器被减慢了 50%，微软的自动更新程序仍在使用 150% 的 CPU（在双核机器上测量），并显示其进度条。

在 OS 10.9 和 iOS 7 中，Apple 引入了使用 `NSProgress` 类和 `NSReporting` 协议报告长时间运行任务的式支持。基本思想是让对象报告各个活动的进度，并结合这些单独的报告以获得整体进度。我在世纪 90 年代后期实现过非常类似的系统，可以说这样做非常好。

然而，Apple 在实际向 UI 报告进度方面完全掉链了，或者说推卸了责任。向 UI 报告进度的推荐技术是观察顶层 `NSProgress` 对象的 `percentCompleted` 属性。这并没有解决我们看到的任何问题，并且增加了一个问题：KVO 通知将在更改进度状态的后台线程递递。

事实上，Apple 告诫：“不要在紧凑循环中更新 `completedUnitCount`”，他们意识到了这个问题，并意识到他们并没有真正解决它。

### 让 iPhone 负载过载

症状是 UI 会冻结很长时间，应用程序才能再次使用。这在首次启动应用程序时尤为明显，因为它必须对所有订阅中的所有项目进行初始获取/更新。随后的启动往往没有那么大的问题，因为数据已经缓存，但仍有糟糕的用户体验需要解决。

性能分析（Profiling）显示时间被消耗在 UIKit 绘制代码中（文本绘制、表格布局）。Apple 提倡的 Cell 复用机制正在使用并运行符合预期，没有特殊的 Apple 创建开销。没什么可做的，对吧？

错！问题被证明在示例 16.2 的代码中。

### 示例 16.2 视图通知模型代码

```objc
- (void) notifyChanged
{
  [NSNotificationCenter defaultCenter
      postNotificationName: @"UserChanged"
      object:nil];
}
```

尽管这段代码看起来没问题，并且与许多发布的关于 `NSNotificationCenter` 的示例相符，但它实际上存在两个问题。首先是缺乏上一节讨论过的更新节流（update-throttling），其次是它太不明确了：它只是说某些东西发生了变化，而没有说明发生了什么变化。缺少了这一重要的上下文信息，接收通知的 UI 元素（在本例中为表格视图）别无选择只能更新所有的 UI。这不仅对于（可见）元素的数量来说是二次方增长，而且还更新了那些甚至不可见且可能不在当前列表中的项目的显示！

解决这个问题的简单方法当然是在通知中包含当前对象，幸运的是 `NSNotification` 天生就设计为可以处理这种情况。示例 16.3 显示了这一改进。

### 示例 16.3 带有上下文的视图通知模型代码

```objc
- (void) notifyChanged
{
  [NSNotificationCenter defaultCenter
      postNotificationName: @"UserChanged"
      object:self];
}
```

接收端代码随后能够从通知中检索相关对象，确定它是否相关（是否包含在当前表格中），然后只更新那一行。示例 16.4 中的代码将这种依赖于上下文的刷新与上一节中的批量刷新结合起来。它假设表格视图正在管理一个“项目”列表。客户端调用 `refreshItemsFromBackground`（例如通过 `NSNotification` 调用），然后该方法会确定该项目的索引并随之使用该索引。

### 示例 16.4 表格视图项目批量刷新的代码

```objc
@property (retain) NSMutableSet *indexesToRefresh;
- (void) refreshAccumulatedItems
```

```objc
{
  NSSet *items=nil;
  @synchronized(self) {
    itemIndexes=[self indexesToRefresh];
    [self setIndexesToRefresh:nil];
  }
  [tableView reloadRowsAtPaths:[itemIndexes allObjects]
       withAnimation:UITableViewRowAnimationNone];
}

-(void) triggerRefresh {
  [self performSelector:@selector(refreshAccumulatedItems)
                withObject:nil afterDelay:0.2];
}
```

```objc
-(void)hideItemFromBackground:item
{
  NSIndexPathPath* index=[self indexPathForItem:item];
  if ( index ) {
    @synchronized(self) {
      if (!indexesToRefresh) {
        [NSMutableSet setObject:@selector(triggerRefresh) index];
        [self performSelectorOnMainThread:@selector(triggerRefresh)
                          withObject:nil waitUntilDone:NO];
      } else {
        [indexesToRefresh addObject:index];
      }
    }
  }
}
```

结果的批处理本质上是由后续代码完成的；如果我们没有一组批量结果，就会创建一个并调度刷新。另一方面，如果我们已经有一个正在进行的批处理，那么只需将其添加到该批次中即可。处理起来非常简单——我们选取该批次，清空它，并刷新表格视图。注意，如果在此期间发生了导致索引失效的任何情况，你需要清除该批次。

### 这仅仅是一种幻觉

我学到的处理 UI 性能问题最重要的技术之一就是隐藏它。实际上执行你应该做的事情太慢了，你通常可以在追赶并完成剩余工作的同时，向用户展示一个仿品。或者你可以使用动画。

使用动画来隐藏延迟是真正天才的举措之一，它让原始 iPhone 看起来如此快速且即时/稳固，尽管其硬件相对较弱，并让它在竞争对手推出更高性能硬件和据称更好的加速图形时，依然保持了这种领先地位。

例如，打开 PDF 文件并渲染第一页（或双页）需要时间。然而，将文件的缩略图动画到全屏意味着用户在系统忙于准备 PDF 时被占据了。由于动画可以由 GPU 处理，这意味着 CPU 资源不会从空闲任务中夺走。

### 图像缩放与裁剪

在 20 世纪 90 年代，我创建了各种驱动不同输出设备的 NeXT ，从用于 NeXT 彩色打印机的高质量变频器到几十美元的高端激光彩色复印机。这些程序之一是 `EXTRASlide`（见图 16.1），它绘制了 Polaroid CL-5000S 数字调色胶片记录仪。

从工程角度来看，这些程序的主要部分是实际的底层驱动程序，它们经常利用 SCSI 端口将由 DisplayScript 渲染的高分辨率位图传输到设备，这些设备使用了自定义且通常实现很差的协议。

![](img/29111a88ed1326b01d04057a653fdbec_352_0.png)

所有这些往往对性能至关重要。例如，Polaroid 记录仪具有 4000 行的分辨率，产生了 48 MB 的图像，并且在交付这些框时有一些实时性要求。由于机器上有 1 GB 的内存，这并不是问题。

现代 UI 设计面临的主要挑战之一是，高分辨率显示器使得视觉化缩放对性能的影响变得困难得多。当你尝试放大一张小图像时，你只会得到一个模糊、低质量的版本。但当你缩小一张高分辨率图像时，你将得到一个清晰、详细的图像。

这是现代性能的关键。Livescribe Smarten 使用红外摄像头在您用非周期性点在纸上书写时精确捕获其位置。桌面应用程序显示并组织了这些捕获的书写/绘图页面。对于每个笔记本，概述模式应该显示捕获的矢量笔画叠加在所用纸张背景上的缩略图，由于明显的原因，背景并没有被笔捕获。两个问题是，这些背景的高分辨率图像渲染非常慢，而且包含笔画的文件格式在读取时有显著的初始化开销。

### 这仅仅是一种幻觉 333

……问题，因为图像正在移动，人眼根本无法辨别细节。一旦缩放完成（释放按钮），我们就切换回原始的 `NSImage`，它将重新创建屏幕。我学到的教训是，对于交互式程序，我们是被允许“作弊”的，只要不被发现即可。在这个示例中，我们在缩放时使用低分辨率位图。虽然没有缩放源文件好，但由于图像在移动，差异并不明显，而且比移动矩形真实得多。

### 缩略图绘制

在开发获奖的 Livescribe Desktop 时，图像，特别是缩略图绘制的问题再次出现，而不被发现作弊再次证明是正确答案。Livescribe Smarten 使用红外摄像头在您用非周期性点在纸上书写时精确捕获其位置。桌面应用程序显示并组织了这些捕获的书写/绘图页面。对于每个笔记本，概述模式应该显示捕获的矢量笔画叠加在所用纸张背景上的缩略图，由于明显的原因，背景并没有被笔捕获。两个问题是，这些背景的高分辨率图像渲染非常慢，而且包含笔画的文件格式在读取时有显著的初始化开销。

### 绝对不要绘制缩略图的方法

绘制缩略图的第一种方法如图 16.3 所示，是字面意思理解“缩略图”。缩略图通常是从较大的图形或文档生成的小图像。我们的 Windows 客户端非常理解这一点并为保存的每个页面创建了缩略图。我们的 Mac 团队认为他们这样做但做得更好，因为 OS X 支持高质量 PDF，且 Apple 刚刚引入了 `CGImageSourceCreateThumbnailAtIndex()` 函数专门用于从磁盘加载缩略图。可能会出什么问题呢？

这种方法存在的所有问题：由于 PDF 是分辨率无关的格式，每个 PDF “缩略图”都包含了全分辨率

![](img/29111a88ed1326b01d04057a653fdbec_353_0.png)

图 16.3 如何不绘制缩略图

对于 PNG，将其绘制到 PDF 中需要对 PNG 进行解压缩，然后为了生成 PDF 进行重新压缩。这些 PDF “缩略图”的渲染速度也非常慢，因为它们包含的细节比人们需要的得多。为了应对这种过程固有的缓慢问题，我们为每个 PDF 都开启了一个新线程来生成。

事实证明，这曾导致过一次机器强制重启，因为 200 个线程占满了 CPU，且内存消耗导致了持续的内存交换（swapping）。

### 如何不真正绘制缩略图

虽然将 PDF 写入磁盘并渲染它们显然是一个经典的*坏主意*，但我们仍然固执于缩略图是一个特定图像的观点，尽管我们现在愿意接受在低分辨率下，位图图像可能就足够了这一想法。Apple 的 ImageKit（也是新的）特别是 `IKImageBrowserView` 似乎可以提供……

这个 API 足够简单，我们只需要[提供]一个数据源，它可以返回几乎可以想象的任何格式的单个图像。

遗憾，结果仍然远不如人，如图 16.4 所示：一旦所有缩略图都生成，一切都非常快，但初始加载非常慢，而且由于缩略图是一个接一个渲染的，视觉上非常突兀。更糟糕的是，在打开文件开销导致的延迟期间，我们无法绘制任何内容。

![](img/29111a88ed1326b01d04057a653fdbec_355_0.png)

图 16.4 原子化缩略图绘制

### 这只是幻象

这让我们没有得到亚马逊客户评论的好评：

如果你有几百页笔记，软件在每次加载打开的文件时都需要重新加载缩略图，这很奇怪。如果你等足够的时间，只要软件处于打开状态，缩略图就会在内存中。这需要太长时间了！如果你关闭程序并重新打开桌面软件，猜怎么着？你必须重新开始等待缩略图再次出现。我不知道 Windows 版本是否也是如此，但在 Mac 上确实发生了这种情况。
