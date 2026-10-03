
## RadioGroup 示例

```xml
<RadioGroup
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <RadioButton
        android:id="@id/radio_male"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Male"
        android:textSize="30dp"/>

    <RadioButton
        android:id="@id/radio_female"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Female"
        android:textSize="30dp"/>

</RadioGroup>
```

在前面的代码段中，定义了一个包含两个 `RadioButton` 视图的 `RadioGroup`，即 `radio_male` 和 `radio_female`。为了在点击任一按钮时执行某些操作，可以使用以下代码段：

```java
protected void onCreate(savedInstanceState) {
    super.setContentView(R.layout.activity_main);
    RadioButton radio_male = (RadioButton) findViewById(R.id.radio_male);
    RadioButton radio_female = (RadioButton) findViewById(R.id.radio_female);
    radio_male.setOnClickListener(radiolistener);
    radio_female.setOnClickListener(radiolistener);
}

OnClickListener radiolistener = new OnClickListener() {
    public void onClick(View view) {
        RadioButton radiobutton = (RadioButton) view;
        Toast.makeText(MainActivity.this, radiobutton.getText(), Toast.LENGTH_SHORT).show();
    }
};
```

## 第 7 章

在 `InputControl` 应用中，`buttonview_layout.xml` 文件创建在 `/res/layout` 目录下，显示了 `<Button>` 元素的使用。列表 29 显示了 `buttonview_layout.xml` 文件的代码：

### 列表 29：在 InputControl 应用中显示 buttonview_layout.xml 文件的代码

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical">

    <Button
        android:id="@id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#0000aa"
        android:text="Click Me"
        android:textSize="30dp" />
</LinearLayout>
```

在列表 29 中，`<Button>` 标签用于显示带有“Click Me”文本的按钮。对应 `buttonview_layout.xml` 文件，在 `InputControl` 应用中创建了 `ButtonView` Java 类，以显示按钮视图的使用。列表 30 显示了 `ButtonView.java` 文件的代码。

> 注：提供的文本包含大量重复和重叠页面，我已根据提供的内容提供了逻辑流。

```java
else {
    Toast.makeText(FormDisplayActivity.this, "This CheckBox has not been selected");
    Toast.LENGTH_LONG.show();
}
```

在 `InputControl` 应用程序中，`checkboxview.xml` 文件创建在 `/res/layout` 目录下，它展示了 `<Checkbox>` 元素的使用。列表 33 显示了 `checkboxview_layout.xml` 文件的代码：

### 列表 33：checkboxview_layout.xml 文件的代码设计

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical">

    <Checkbox
        android:id="id/checkbox1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Qualification"
        android:textSize="30dp" />
</LinearLayout>
```

在列表 33 中，添加了一个 `CheckBox`，它显示文本“Qualification”。对应 `checkbox_layout.xml` 文件，在 `InputControl` 应用程序中创建了 `CheckBox` Java 类以显示复选框视图的使用。列表 34 显示了 `CheckContentView.java` 文件的代码：

### 列表 34：InputControl 中 CheckContentView.java 文件的代码设计

```java
package com.kogogent;

import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.CheckBox;
import android.widget.Toast;

public class CheckContentView extends Activity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.checkboxview);
        Checkbox checkbox1 = (Checkbox) findViewById(R.id.checkbox1);
        checkbox1.setOnClickListener(new OnClickListener() {
            public void onClick(View view) {
                if (((Checkbox) view).isChecked()) {
                    Toast.makeText(Checkbox.this,
                        "This Checkbox has been selected",
                        Toast.LENGTH_LONG).show();
                } else {
                    Toast.makeText(Checkbox.this,
                        "This Checkbox has not been selected",
                        Toast.LENGTH_LONG).show();
                }
            }
        });
    }
}
```

在列表 34 中，创建了 `CheckBox` 类的对象。每当用户勾选或取消勾选复选框时，该对象都会通过 `OnClickListener` 接口显示消息。当你运行 `InputControl` 应用程序并点击 `CheckBox View` 按钮时，你会看到一个复选框视图，如图 58 所示。

![](img/889a483c5a60e0806e42b73b2662a855_301_0.png)

▲ 图 58：显示 CheckBox Activity 的输出

如果你勾选了 Qualification `CheckBox` 视图，将显示“此复选框已被选中”的消息。

### 使用 ImageView 视图

`ImageView` 视图与 `Button` 视图类似，但它显示的是图像而不是文本。通常，`ImageView` 视图的背景会在按钮的不同状态下（如点击或聚焦）发生。以下代码片段展示了如何创建一个图像按钮：

```xml
<ImageButton
    android:id="@id/imageButton1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/android_icon"
    android:contentDescription="@string/image_description"/>
```

在前面的代码片段中，`android_icon` 是放置在 `drawable` 文件夹中的图像文件名。`contentDescription` 属性提供了图像的描述。此描述可以通过字符串资源文件来定义。

如果你想在点击按钮时执行某些操作，可以使用 `OnClickListener` 接口，如下所示：

```java
// 逻辑代码示例
imageButton.setOnClickListener(new OnClickListener() {
    @Override
    public void onClick(View v) {
        // 执行操作
    }
});
```

### 使用 ToggleButton 视图

`ToggleButton` 视图显示按钮状态是否发生了变化（勾选或未勾选）。此外，你可以在按钮状态改变时设置文本为“开启”或“关闭”。以下代码片段展示了如何创建 `ToggleButton`：

```xml
<ToggleButton
    android:id="@id/toggle_button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Silent Mode on"
    android:text="Silent Mode off"/>
```

在 `Activity` 类中实现 `OnClickListener` 接口如下：

```java
final Toggle toggleButton = (ToggleButton) findViewById(R.id.toggle_button);
toggleButton.setOnClickListener(new OnClickListener() {
    public void onClick(View v) {
        if (toggleButton.isChecked()) {
            Toast.makeText(context, "ToggleButton is on", Toast.LENGTH_LONG).show();
        } else {
            Toast.makeText(context, "ToggleButton is off", Toast.LENGTH_LONG).show();
        }
    }
});
```

```java
Toast.LENGTH_LONG).show();
}
}
}
));
));
}
}
```

在 `InputControl` 应用中，`togglebuttonview_layout.xml` 文件创建在 `res/layout` 路径下，它显示了 `<ToggleButton>` 元素的使用。列表 37 显示了 `togglebuttonview_layout.xml` 文件的代码：

### 列表 37：显示 InputControl 应用中 togglebuttonview_layout.xml 文件的代码

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical">

    <ToggleButton
        android:id="@id/toggle_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textOff="Silent Off"
        android:text="Silent Mode"
        android:textSize="30dp" />
</LinearLayout>
```

在列表 37 中，添加了一个带有不同属性的 `ToggleButton`。对应 `togglebuttonview_layout.xml` 文件，在 `InputControl` 应用中创建了 `ToggleButton` Java 类，以显示切换按钮视图的使用。列表 38 显示了 `ToggleButton.java` 文件的代码：

### 列表 38：显示 InputControl 应用中 ToggleButtonView.java 文件的代码

```java
package com.intent.android;

import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.view.OnClickListener;
import android.widget.Toast;
import android.widget.ToggleButton;

public class ToggleButtonView extends Activity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.toggleview_layout);
        final ToggleButton toggle_button = (ToggleButton) findViewById(R.id.toggle_button);
        toggle_button.setOnOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if (toggle_button.isChecked()) {
                    Toast.makeText(ToggleButton.this, "ToggleButton is On", Toast.LENGTH_LONG).show();
                } else {
                    Toast.makeText(ToggleButton.this, "ToggleButton is off", Toast.LENGTH_LONG).show();
                }
            }
        });
    }
}
```
