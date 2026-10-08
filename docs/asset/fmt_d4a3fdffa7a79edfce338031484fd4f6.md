
关闭语句和连接。当你完成语句和连接后，应该关闭它们：

```java
stmt.close();
conn.close();
```

# 预语句 (Prepared Statements)

如果你计划多次使用相同的（或相似的）SQL 语句，可以使用预编译语句。某些数据库服务器可以在服务器上编译或缓存查询，这可能会稍微提高速度。

你还可以使用预语句在 SQL 语句中创建占位符。例如，如果你想向 `contact` 表中插入三行，可以创建一个带有值占位符（问号 `?`）的预 `INSERT` 语句：

```java
String insert = "INSERT INTO userinfo " + 
" (username, userid)" + 
" VALUES(?, ?)";
PreparedStatement pstmt = conn.prepareStatement(insert);
```

然后，你可以使用 `PreparedStatement` 的 `setXXX()` 方法（如 `setString()` 和 `setInt()`）为每个参数设置值，然后执行语句：

- `pstmt.setString(1, "scrotus");`

- `pstmt.setInt(2, 702);`

- `pstmt.executeUpdate();`

# 发送 SQL 示例

让我们来看一个完整的示例，它创建一个表并插入一些数据（为了保持简短，我们将大部分代码放在同一个 `try...catch` 块中）：

```java
import java.sql.*;

public class Statement {

    public static void main(String[] args) {

        try {
            Class.forName("postgresql.Driver");
        } catch (Exception e) {
            System.err.println(e.getMessage());
            System.exit(-1);
        }

        String url = "jdbc:postgresql://localhost/postgres";
        String user = "postgres";
        String pass = "";
        try {
            // 打开连接。
            //
            Connection conn = DriverManager.getConnection(url, user, pass);

            // 创建一个语句对象。
            //
            Statement stmt = conn.createStatement();

            // 使用语句创建表并添加
            // 一些行。
            //
            String sql;
            sql = "CREATE TABLE userInfo " + 
            "username VARCHAR(50), userid INT)";
            stmt.execute(sql);

            // 创建一个预语句。
            //
            String insert = "INSERT INTO userinfo " + 
            " (username, userid)" + 
            " VALUES(?, ?)";
            PreparedStatement pstmt = conn.prepareStatement(insert);

            pstmt.setString(1, "scrotus");
            pstmt.setInt(2, 702);
            pstmt.executeUpdate();

            // 关闭语句和连接。
            //
            stmt.close();
            conn.close();
        } catch (SQLException e) {
            System.err.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

# 处理结果集 (Process Result Sets)

某些 SQL 语句（如 `SELECT`）会产生结果集。其他语句（如 `INSERT` 和 `UPDATE`）则不产生结果集。对于许多应用程序，结果集是核心。例如，你可能使用结果集来：

- 格式化值

- 在屏幕上显示值

- 在其他地方使用值

当你拥有 `ResultSet` 时，你需要引用它：

遍历结果集。要遍历结果集，你应该反复调用它的 `next()` 方法，直到返回 `false`。

获取值。在循环中，你可以使用各种 `getXXX()` 函数获取列。`getXXX()` 方法（如 `getString()` 和 `getInt()`）会尽可能解释列值。这是一个获取 `uname` 列为字符串并将 `uid` 列为整数的示例：

```java
String uname = rs.getString("username");
int uid = rs.getInt("userid");
```

# 处理结果集示例

这是一个查询我们在上一节中创建的 `userInfo` 表的完整示例：

```java
import java.sql.*;

public class ProcessResult {

    public static void main(String[] args) {

        try {
            Class.forName("postgresql.Driver");
        } catch (Exception e) {
            System.err.println(e.getMessage());
            System.exit(-1);
        }

        String url = "jdbc:postgresql://localhost/postgres";
        String user = "postgres";
        String pass = "";
        try {
            // 打开连接。
            //
            Connection conn = DriverManager.getConnection(url, user, pass);

            // 创建一个语句对象。
            //
            Statement stmt = conn.createStatement();

            // 获取 userInfo 表中的所有行。
            //
            String sql = "SELECT * FROM userInfo";
            ResultSet rs = stmt.executeQuery(sql);

            // 遍历结果集
            while (rs.next()) {

                // 获取当前行的列值。
                //
                String uname = rs.getString("username");
                int uid = rs.getInt("userid");

                System.out.print("Name: " + uname);
                System.out.println("ID: " + uid);
            }

            // 关闭语句和连接。
            //
            stmt.close();
            conn.close();
        } catch (SQLException e) {
            System.err.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

## Swing

`Swing` 是 Java 基础类（JFC）的一部分组件集。你可以使用 `Swing` 从零开始构建图形化用户界面。通过 `Swing`，你构建了一个层次化的组件系统。例如，一个窗口可以包含一个或多个面板，而面板又包含按钮和文本字段。`Swing` 包含了许多组件，并且存在许多可能的组合。图 11.2 显示了其中一种可能的分解视图。

## 窗口、字段和按钮

让我们来看一个非常 `Swing` 应用程序。这个应用程序包含一个 `Frame`（主窗口）、一个文本输入字段和一个按钮。我们先看简单的情况（不包含事件处理），然后向示例中添加事件处理。在那个阶段，我们将使用事件处理来响应按钮点击和关闭窗口请求。

要创建这个简单的应用程序，我们需要执行以下步骤，这些步骤对于大多数简单的 `Swing` 应用程序都是必要的：

- 1. 导入 `Swing` 和 `AWT` 类：

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
```

![](img/be9d6408fd1e74bd8b833ec2a75bea98_324_0.png)

图 11.2 组件层次结构。

- 2. 创建一个 `JFrame`，它是你的顶层窗口（参数 `"Simple Swing Demo"` 是窗口的标题）：

- 3. 不要直接将所有组件放入 `JFrame` 中，你必须创建一个容器（例如 `JPanel`）来容纳你想要创建的组件：

```java
JPanel contents = new JPanel();
```

- 4. 使用布局管理器来控制容器的布局方式。这个 2x2 的网格布局将每个后续元素放入下一个网格单元中，从左上角单元开始：

```java
contents.setLayout(new GridLayout(2, 2));
```

- 5. 创建组件。在这里，我们创建了一个标签、一个字段和一个按钮：

```java
JLabel label = new JLabel("Name");
JTextField textField = new JTextField(10);
JButton button = new JButton("OK");
```

- 6. 尽可能增加可访问性。在例例中，我们告诉标签它属于该文本字段。这可以帮助使用非视觉用户界面的用户，例如使用语音驱动的用户界面：

```java
label.setLabelFor(textField);
```

- 7. 将组件添加到你在步骤 3 中创建的容器中。注意，我们使用空白标签来填充左下角的网格单元，这强制按钮进入右下角的单元：

```java
contents.add(label);
contents.add(textField);
contents.add(new JLabel("*"));
contents.add(button);
```

- 8. 添加容器。我们不直接将其添加到面板中，而是将其添加到它的内容面板（content pane）：

```java
Container content_pane = demo_frame.getContentPane();
content_pane.add(contents);
```

- 9. 封装（紧凑排列的布局）并显示（显示）框架：

```java
demo_frame.pack();
demo_frame.show();
```

## 事件处理

虽然这九个步骤足以在屏幕上显示一个简单的用户界面，但它们不足以构建真正实用的东西。如果你仅按照这些步骤编写程序，当你点击“关闭”按钮时，它会变得很讨厌。窗口会消失，但程序不会退出。这是因为系统在窗口关闭时会生成一个事件。`JFrame` 接收到事件并执行正确的操作，但到此为止。

由你决定在窗口关闭时做什么。这是一件好事，因为你可以在允许窗口关闭之前检查你的程序是否已准备好退出。

Java 使用类似于观察者模式的机制处理事件（例如按钮点击）。在这种模式中，事件的主体是一个 `Swing` 组件，例如 `JButton` 或 `JFrame`。观察者是类，例如 `WindowAdapter`，你将这些类注册到主体上。当某些事件发生时（例如窗口关闭时），主体会向所有注册的观察者发送消息。图 11.3 显示了 `JFrame` 和 `WindowAdapter` 对象的一些方法。当你编写自己的自定义事件处理器时，你会创建一个 `WindowAdapter` 的子类，并重写它的部分或所有方法。图 11.3 显示了其中一个子类 `MyAdapter`。

要向 `Frame` 添加窗口监听器，请遵循以下步骤（这些步骤也作为显示在图 11.4 的协作图中）：

- 1. 创建一个 `JFrame` 对象。

- 2. 定义 `WindowAdapter` 的子类，并重写你需要的方法，例如 `windowClosing()`，然后创建该类的实例。

- 3. 使用 `addActionListener()` 将该类注册到 `JFrame`。

![](img/be9d6408fd1e74bd8b833ec2a75bea98_326_0.png)

图 11.3 `Swing` 中的观察者模式。

![](img/be9d6408fd1e74bd8b833ec2a75bea98_327_0.png)

图 11.4 添加窗口监听器。

当用户关闭窗口时，`JFrame` 会调用你通过 `addWindowListener()` 注册的所有类的 `windowClosing()` 事件，正如图 11.5 中的协作图所示。以下是你如何在 Java 中实现这些概念的：

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

// 处理窗口关闭事件
class MyAdapter extends WindowAdapter {
    @Override
    public void windowClosing(WindowEvent e) {
        System.out.println("Exiting...");
        System.exit(0);
    }
}

// 在 main 方法中
public static void main(String[] args) {
    JFrame demo_frame = new JFrame("Simple Swing Demo");
    demo_frame.addWindowListener(new MyAdapter());
    // ... 其余设置
}
```

```java
// Step 3. 创建一个面板来容载组件。
//
JPanel contents = new JPanel();
```

```java
// Step 4. 在 JPanel 中布局组件，使用
// 两列、两行。
contents.setLayout(new GridLayout(2, 2));
```

```java
// Step 5. 创建一个标签、文本字段和按钮。
//
JLabel label = new JLabel("Name:");
final JTextField textField = new JTextField(10);
JButton button = new JButton("OK");
```

```java
// Step 6. 将标签与其对应的
// 组件关联起来。
label.setLabelFor(textField);
```

```java
// Step 7. 将组件添加到面板中。
//
contents.add(label);
contents.add(textField);
contents.add(new JLabel(""));
contents.add(button);
```

```java
// Step 8. 将你在步骤 3 中创建的容器
// 添加到 JFrame 的内容面板。
Container content_pane = demo_frame.getContentPane();
content_pane.add(contents);
```

```java
// Step 9. 创建一个 WindowAdapter 来处理
// 窗口关闭事件，并将其添加到 Frame。
//
WindowAdapter wa = new WindowAdapter() {
    public void windowClosing(WindowEvent e) {
        System.out.println("Exiting...");
        System.exit(0);
    }
}
demo_frame.addActionListener(wa);
```
