
- 3. 选择 AVD 模拟器并点击 AVD 对话框中的 Start 按钮。模拟器会首先启动并运行。你也可以导航到 `SDK\tools` 目录并通过执行命令行 `emulator androidAVD` 来启动模拟器。

- 4. 使用命令提示符进入 `D:\AndroidWorkspace\FirstAndroidApp`（项目的根目录）并执行 `ant debug` 命令。此命令用于构建调试包项目以编译必要的依赖项。执行命令后，通过 GUI 导航到项目的 `\bin` 目录。你会找到 `AndroidProject-debug.apk` 文件。在该文件上，我们将执行步骤 5 中给出的下一个命令。

- 5. 构建成功后，执行 `adb install D:\AndroidWorkspace\FirstAndroid\bin\AndroidProject-debug.apk` 命令，如图 30 所示：

![将文件安装到模拟器](img/figure30.png)

> 图 30：将文件安装到模拟器

`adb install` 命令用于将文件安装到 Android 模拟器。

- 6. 在模拟器上找到 `MainActivity` 并点击它。输出屏幕将显示“Hello World, Main Activity”文本。要更改文本，请通过 GUI 导航到目录 `C:\Workspace\FirstAndroid\res\layout`。在这里你会找到 `activity_main.xml` 文件。用记事本打开此文件，并将 `TextView` 属性内的字符串 "Hello World" 替换为 "Hello Android"。保存文件并在根目录（在本例中为 "FirstAndroid"）再次执行两个命令以重新编译项目：

    - a. `ant debug`

    - b. `ant install`

`adb install` 命令用于安装已编译的调试包，仅当 `.apk` 文件位于二进制目录时适用。

通过这种方式，你可以从命令行运行项目。有时可能运行着多个模拟器。在这种情况下，要在特定模拟器上运行，你可以使用以下命令：

```
adb -s emulator:5554 install D:\androidworkspace\FirstAndroid\bin\AndroidProject-debug.apk
```

5554 是模拟器的序列号。

## 7.5 Activities 和 Intents

Activity（活动）是一个允许用户执行操作的组件。通常，activity 是为用户提供界面的窗口。换句话说，应用程序是这些的集合。但需要注意的是，单个应用程序中可以有一个或多个活动。Intent（意图）是另一个重要概念，允许不同应用程序的不同活动通过称为 intents 的消息协同工作。让我们学习活动和意。

## 操作 Activities

Activities 在 Android 中起着至关重要的作用，因为它们用于为用户创建屏幕。因此，学习如何启动、停止、挂起和恢复活动是非常重要的。Activity 由处理布局并提供图形的视图组成。在本节中，你将学习如何通过以下操作来处理活动：

- 创建 activity

- 启动 activity

- 管理 activity 的生命周期

- 为 activity 应用主题和样式

让我们逐一执行这些操作。

## 创建 Activity

你可以通过创建一个扩展 `Activity` 类的 Java 类来创建活动。注意，每个活动都需要创建一个可以加载界面组件的窗口。为此，调用了 `setContentView(View)` 方法。通常，活动作为全屏窗口显示给用户。你也可以将它们设置为其他活动中的不同视图，例如浮动或嵌入。你可以使用具有 `windowIsFloating` 属性的主题设置浮动窗口，可以使用 `ActivityGroup` 类将一个活动嵌入另一个（在 API 13 中弃用）。你应该注意，所有活动（或 `Activity` 基子类）通常实现两个方法，即 `onCreate(Bundle)` 和 `onPause()`。除了这些方法外，`Activity` 类提供了许多其他作为生命周期事件的方法。表 4 描述了管理活动生命期的 `Activity` 类方法：

### 表 4：Activity 生命周期回调方法描述

| 方法 | 说明 |
| --- | --- |
| `onCreate()` | 当首次创建活动时调用。在此方法中，你应该提供基本的静态设置，例如创建视图或将数据绑定到列表。在创建活动期间，此方法带有 null `savedInstanceState` 参数调用。然而，如果活动被用户停止或被系统销毁，则此方法将带有其之前的状态保存的 `Bundle savedInstanceState` 参数调用。即使当你更改设备方向（即横屏或竖屏），活动也会被重建。 |
| `onStart()` | 当 Activity 显示给用户时调用。当 Activity 首次启动或返回前台时，`onStart()` 方法的执行之后是执行 `onResume()` 方法。然而，如果 Activity 变为隐藏，此方法的调用之后是执行 `onStop()` 方法。 |
| `onRestart()` | 当 Activity 停止并重新启动时调用。此方法始终在 `onStart()` 方法之后调用。 |
| `onResume()` | 当 Activity 开始与用户交互时调用。当 Activity 的此方法被调用时，该 Activity 位于 Activity 栈的顶部。该方法的执行之后总是执行 `onPause()` 方法。 |
| `onPause()` | 系统准备恢复上 Activity 时调用。如果 Activity 返回前面，此方法的执行之后是执行 `onResume()` 方法。然而，如果 Activity 对用户不可见，此方法的调用之后是执行 `onStop()` 方法。 |
| `onStop()` | 当 Activity 对用户不可见时调用，这可能是由于两个原因：首先，如果 Activity 被销毁；其次，当其他 Activity 的处理返回时。在第一情况下，此方法的调用之后是执行 `onDestroy()` 方法。在另一种情况下，此方法的调用之后是执行 `onResume()` 方法。 |
| `onDestroy()` | 当 Activity 被销毁时调用。换句话说，此方法在 Activity 上的 `finish()` 方法被调用或 Activity 实例被系统销毁时执行。 |

在概述 `Activity` 基类的方法后，现在让我们继续了解如何创建一个 Activity。以下代码片段显示了如何创建一个扩展 `Activity` 基类的 Java 类：

```java
// defining the activity in the com.kogent.android package
package com.kogent.android;

// importing the required packages
import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;

public class MainActivity extends Activity {
    // Invoked when the activity is created for the first time
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }
}
```

在前面的代码片段中，`SampleActivity` 类定义在 `com.kogent.android` 包中。此外，`SampleActivity` 类扩展了 `Activity` 类并提供了 `onCreate()` 和 `onCreateOptionsMenu()` 方法的实现。你应该注意，在前面的代码片段中，调用了 `setContentView()` 方法，以便 `Activity` 类可以从 `activity_main.xml` 文件加载其用户界面。

Android 应用程序中声明的每个 Activity 都应该在 `AndroidManifest.xml` 文件中声明。以下代码片段显示了如何在 `AndroidManifest.xml` 文件中声明 `SampleActivity` 类：

```xml
<application
    android:backup="true"
    android:icon="@drawable/ic_launcher"
    android:label="@string/app_name"
    android:theme="@style/Apptheme">
    <activity
        android:name="com.kogent.android.MainActivity"
        android:label="@string/app_name">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
```

在前面的代码片段中，可以看到使用 `<activity>` 标签声明了 `SampleActivity` 类。

## 启动 Activity

Android API 提供了 `startActivity(Intent)` 方法来启动一个新的 Activity。当调用一个新的 Activity 时，该 Activity 会通过推入其他 Activity 放置在 Activity 栈的顶部。`startActivity()` 方法接受一个 `Intent` 参数，该参数描述了要执行的 Activity。有时，你可能需要从现有的 Activity 调用一个 Activity 并返回之前的 Activity。在这种情况下，会调用 `startActivityForResult(Intent, int)`，结果将返回给 `onActivityResult(int, Intent)` 方法。

让我们使用 Eclipse IDE 创建一个简单的 Android 应用程序 `StartActivityDemo`。在这个 Activity 中，我们将使用 `MainActivity` 类，它将调用另一个内置 Activity——Contacts。换句话说，在 `MainActivity` 类的执行期间，当你触摸手机时，内置的 Contacts Activity 将调用；显示存储在设备中的联系人列表。你可以选择一个合适的联系人并按下设备上的 OK 按钮，这将带你回到 `MainActivity` Activity。

执行以下步骤创建 `StartActivityDemo` 应用程序：

- 1. 打开 Eclipse IDE。Android-ADT 窗口打开（图 31）。

- 2. 选择 File→New→Android Application Project，如图 31 所示：

- 3. 点击 Next 按钮。

- 4. 输入 Application Name、Package Name 和 Minimum SDK 版本。

- 5. 点击 Next 按钮。

- 6. 确保选中了 Create Activity 复选框。

- 7. 选择 Blank Activity。

- 8. 点击 Next 按钮。

- 9. 在 Activity Name、Layout Name 和 Layout Name 字段中输入值。

- 10. 将 `MainActivity.java` 的代码替换为列表 1 所示的代码。

## 第7章

```java
}
return false;

}
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
  if (requestCode == PICK_CONTACT_REQUEST) {
    if (resultCode == RESULT_OK) {
      // 将所选的联系人显示给用户。
      Uri uri = data.getData();
      Intent intent = new Intent(Intent.ACTION_VIEW, uri);
      startActivity(intent);
    }
  }
}
```

- 当用户触摸屏幕上的任何位置时，会触发 `onTouch` 事件。此事件会调用 `startActivityForResult()` 方法，该方法接受三个参数，即 `Intent`、联系人活动的 `URI` 以及 `int` 类型的值。如果用户执行了适当的操作，`startActivityForResult()` 返回 `true`；否则返回 `false`。此外，会调用 `onActivityResult()` 方法，它会显示用户选择的联系人详情。

创建 `StartActivityDemo` 应用程序后，你可以运行该程序以查看其输出。为此，在 Package Explorer 中右键点击 `StartActivityDemo` 应用程序，并选择 `Run As->Android Application`。`StartActivityDemo` 应用程序的输出如图 35 所示：

![](img/889a483c5a60e0806e42b73b2662a855_245_0.png)

图 35：显示 StartActivityDemo 应用程序的输出

触摸手机屏幕以调用联系人活动（Contacts activity），如图 36 所示：

![](img/889a483c5a60e0806e42b73b2662a855_245_1.png)

图 36：显示联系人活动

选择一个你想在屏幕上显示的联系人。在我们的案例中，我们选择了 Zane，相应的联系人详情显示如图 37 所示：

## 开源移动编程

![](img/889a483c5a60e0806e42b73b2662a855_246_0.png)

## 图 37：显示联系人的详情

现在让我们学习如何管理 Activity 的生命周期。

## 管理 Activity 的生命周期

你已经学习过 Activity 具有各种生命周期回调方法。当你创建一个 Activity 时，默认会提供 `onCreate()` 方法。该方法提供了用于显示应用程序用户界面元素的代码。

图 38 显示了 Activity 经历的各个阶段：

![](img/889a483c5a60e0806e42b73b2662a855_246_1.png)

### 图 38：显示 Activity 的生命周期

你可以通过创建一个简单的 Android 应用程序并注意触发的事件来理解图 39 中的流程图。

让我们创建一个名为 `ManageActivityCycle` 的应用程序，它将根据触发的事件显示相应的消息。

按照以下步骤创建并运行 `ManageActivityCycle` 应用程序：

1. 在 Eclipse IDE 的 `com.kogent.android` 包下创建 `ManageActivityCycle` 应用程序。

2. 替换位于 `/src/com/kogent/android` 文件夹下的 `MainActivity.java` 文件中的代码，使用如列表 2 所示的代码：

**列表 2**：显示 ManageActivityCycle 应用程序中 MainActivity.java 文件的代码
