
```java
195 //变量声明
196 private javax.swing.JLabel blueLabel;
197 private javax.swing.JSlider blueSlider;
198 private javax.swing.JTextField blueJTextField;
```

图 F.9 | 使用 GroupLayout 进行 GUI 布局的 ColorChooser 类。（6 部分中的第 5 部分）

# 录 F GroupLayout

```java
private javax.swing.JPanel colorJPanel;

private javax.swing.JLabel greenJLabel;

private javax.swing.JSlider greenJSlider;

private javax.swing.JTextField greenJTextField;

private javax.swing.JLabel redJLabel;

private javax.swing.JSlider redJSlider;

private javax.swing.JTextField redJTextField;

// 变量声明结束
}
```

![](img/1df0d1e8ac6007b95647eb8ea38390af_1567_0.png)

![](img/1df0d1e8ac6007b95647eb8ea38390af_1567_1.png)

![](img/1df0d1e8ac6007b95647eb8ea38390af_1567_2.png)

![](img/1df0d1e8ac6007b95647eb8ea38390af_1567_3.png)

**图 F.9** 使用 GroupLayout 进行 GUI 布局的 ColorChooser 类。（6 部分中的第 6 部分。）

`initComponents`方法（36–161 行）完全是由 NetBeans 根据你与 GUI 设计器的交互生成的。该方法创建并格式化了 GUI。38–93 行构造 GUI 组件。95–161 行使用 GroupLayout 指定这些组件的布局。108–153 行指定水平组，我们手动在第 18 行添加了更改 `colorJPanel` 背景颜色的语句，以及第 23–28 行的 `setColor` 方法。当用户将鼠标移动到一个 `JSlider` 上时，`JSlider` 的事件处理器会将相应的 `JTextField` 中的文本 设置为 `JSlider` 的值（166、171 和 177 行），然后调用 `changeColor` 方法（166、172 和 178 行）来更新 `JPanel` 的背景颜色。`changeColor` 方法获取每个 `JSlider` 的当前值（26–27 行），并将这些值作为 `Color` 构造函数创建一个新的 `Color`。

# GroupLayout 网络资源

- `weblogs.net/blog/tpavek/archive/2006/02/getting_to_know_1.html` Tomas Pavek 的 GroupLayout 博客第 1 部分解释了 GroupLayout 理论。
- `weblogs.net/blog/tpavek/archive/2006/03/getting_to_know.html` Tomas Pavek 的 GroupLayout 博客第 2 部分。

# F.4 GroupLayout 网络资源 1523

- `weblogs.net/blog/tpavek/archive/2006/02/getting_to_know_1.html` 提供了一个使用 GroupLayout 构建的通讯录 GUI 示例。
- `java.sun.com/javase/jdk6/api/javax/swing/GroupLayout.html` GroupLayout 类的 API 文档。
- `java.sun.com/developer/technicalArticles/violet_qa.html` 文章：“新的一波 GUI”，Roman Strobl 编写。
- `www.netbeans.org/kb/50/quickstart.html` NetBeans 中的 GUI 构建，Talley Mulligan 编写。在 Netbeans 中构建 GUI 的指南。
- `www.netbeans.org/kb/41/flash-matisse.html` Matisse 设计器的 Flash 演示，它使用 GroupLayout 排版组件。
- `weblogs.net/blog/claudio/archive/nb-1-layouts.html` 基于 Flash 的 Group 教程。
- `www.developer.com/java/ent/article.php/358996` 教程：“使用 Matisse 构建 Java GUI：入门介绍”，Dick Wall 编写。
- `mclipse.com/enterpriseworkbench/help/index.jsp topic=/com.genuite.eclipse.dkory.doc/quickstart.html` MyEclipse 教程：“Matisse4MyEclipse—Swing RCP 快速上手”。介绍了适用于 Eclipse IDE 的 Matisse 设计器版本。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1569_0.png)

# Java 桌面集成组件

## G.1 引言
Java 桌面集成组件 (`JDIC`) 是一个开源项目的一部分，旨在允许 Java 应用程序与其运行的平台进行更好的集成。`JDIC` 功能包括：

- 与底层平台交互以启动原生应用程序（如网络浏览器和电子邮件客户端）
- 在应用程序开始执行时显示启动屏，告知用户应用程序正在加载
- 在系统托（也称为任务栏状态区域或通知区域）中创建图标，以便访问后台运行的 Java 应用程序
- 注册类型关联，使指定类型的文件可以使用相应的 Java 应用程序打开
- 创建安装包等。

`JDIC` (`jdic.dev.java.net/`) 包含了 `JDIC` 介绍、下载、文档、常见问题、演示、文章、博客、公告、孵化项目、开发者页面、邮件列表等。Java SE 6 包含了上述部分功能。我们在这里讨论了其中的几个功能。

## G.2 启动屏
Java 应用程序用户经常会感知性能问题，因为当你首次启动应用程序时，屏幕上什么都没有出现。显示程序正在加载的一种方法是显示启动屏——一种在应用程序加载时临时出现的无边框窗口。Java 6 提供了新的命令行选项 `-splash` 用于

用于完成此任务的 `java` 命令。此选项允许你指定一个 PNG、GIF 或 JPG 图像，该图像将在你的应用程序开始加载时显示。为了演示这一新选项，我们创建了一个程序（图 G.1），该程序会睡眠 5 秒（以便你可以查看启动屏），然后在命令行中显示一条消息。该示例目录包含一个用于 PNG 格式的图像作为启动屏。要在此应用程序加载时显示启动屏，请使用命令：

`java -splash:DeitelBug.png SplashDemo`

```java
// Fig. G.1: SplashDemo.java
// 启动屏演示。
public class SplashDemo {
    public static void main( String[] args ) {
        try {
            Thread.sleep( 5000);
        } // end try
    } catch ( InterruptedException e ) {
            e.printStackTrace();
        } // end catch
        System.out.println("This was the splash screen demo.");
    } // end method main
} // end class SplashDemo
```

![](img/1df0d1e8ac6007b95647eb8ea38390af_1570_0.png)

图 G.1 | 使用 `java` 命令的 `-splash` 选项显示的启动屏。

## 附录 G Java 桌面集成组件 (JDIC)

一旦你启动了启动屏显示，就可以通过 `java.awt` 包中的 `SplashScreen` 类以程序方式与其进行交互。你可能可以使用它为启动屏添加一些动态内容。有关有关启动屏的更多信息，请参考以下网站：

```
java.sun.com/developer/technicalArticles/J2SE/Desktop/javase6/splashscreen/
java.sun.com/javase6/docs/api/java/awt/SplashScreen.html
```
