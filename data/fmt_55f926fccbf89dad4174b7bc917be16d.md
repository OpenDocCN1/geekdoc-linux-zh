
## 使用 ToggleButton 视图

在 InputControl 应用中，`togglebuttonview_layout.xml` 文件创建在 `res/layout` 路径下，它显示了 `<ToggleButton>` 元素的使用。列表 37 显示了 `togglebuttonview_layout.xml` 文件的代码：

+ 列表 37：显示 InputControl 应用中 togglebuttonview_layout.xml 文件的代码

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

在列表 37 中，添加了一个带有不同属性的 `ToggleButton`。对应 `togglebuttonview_layout.xml` 文件，在 InputControl 应用中创建了 `ToggleButton` Java 类，以显示切换按钮视图的使用。列表 38 显示了 `ToggleButtonView.java` 文件的代码：

+ 列表 38：显示 InputControl 应用中 ToggleButtonView.java 文件的代码

```java
package com.intent.android;

import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Toast;
import android.widget.ToggleButton;

public class ToggleButtonView extends Activity {

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.toggleview_layout);
        final ToggleButton toggle_button = (ToggleButton) findViewById(R.id.toggle_button);
        toggle_button.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if (toggle_button.isChecked()) {
                    Toast.makeText(ToggleButtonView.this, "ToggleButton is On", Toast.LENGTH_LONG).show();
                } else {
                    Toast.makeText(ToggleButtonView.this, "ToggleButton is off", Toast.LENGTH_LONG).show();
                }
            }
        });
    }
}
```

在列表 38 中，创建了一个 `ToggleButton`，它根据是否被勾选来显示文本。

当你运行 InputControl 应用并点击 ToggleButton View 按钮时，你会看到一个切换按钮，显示“Silent Mode off”文本，如图 60 所示：

![](img/889a483c5a60e0806e42b73b2662a855_306_0.png)

图 60：显示切换按钮

现在，当你点击切换按钮时，随着视图状态变为选中，文本会发生变化。图 61 显示了被选中的 `ToggleButton` 视图：

![](img/889a483c5a60e0806e42b73b2662a855_307_0.png)

图 61：开启切换按钮

## 使用 RatingBar 视图

`RatingBar` 视图用于以星级的形式显示评分条组件，用户可以使用方向键进行设置。你可以通过使用 Activity 类中的 `setNumStars(int)` 方法或通过在 XML 布局中使用 `android:numStars` XML 属性来设置显示的星级数量。你必须确保 `RatingBar` 视图的 `layout_width` 属性设置为 `wrap_content` 以显示评分星级。

你可以使用以下代码段在 XML 布局文件中定义 `RatingBar` 视图：

```xml
<RatingBar
    android:id="@id/ratingbar"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:numStars="7"
    android:stepSize="1.0"/>
```

接下来，你需要在 Activity 类中为 `RatingBar` 视图实现 `setOnRatingBarChangeListener()` 方法，如下代码所示：

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    RatingBar rating_bar = (RatingBar) findViewById(R.id.ratingbar);
    rating_bar.setOnRatingBarChangeListener(new OnRatingBarChangeListener() {
        public void onRatingChanged(RatingBar ratingBar, float rating, boolean fromUser) {
            Toast.makeText(FormDisplayActivity.this, "User Rating is: " + rating, Toast.LENGTH_LONG).show();
        }
    });
}
```

在 InputControl 应用中，`ratingbarview_layout.xml` 文件创建在 `/res/layout` 路径下，显示了 `<RatingBar>` 元素的使用。列表 39 显示了 `ratingbarview_layout.xml` 文件的代码：

+ 列表 39：显示 InputControl 应用中 ratingbarview_layout.xml 文件的代码

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical">

    <RatingBar
        android:id="@id/ratingbar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:numStars="7"
        android:stepSize="1.0"/>
</LinearLayout>
```

在列表 39 中，添加了一个带有不同属性的 `RatingBar`。对应 `ratingbarview_layout.xml` 文件，在 InputControl 应用中创建了 `RatingBar` Java 类，以显示评分条视图的使用。列表 40 显示了 `RatingBarView.java` 文件的代码：

+ 列表 40：显示 InputControl 应用中 RatingBarView.java 文件的代码

```java
package com.intent.android;

import android.app.Activity;
import android.os.Bundle;
import android.widget.RatingBar;
import android.widget.RatingBar.OnRatingBarChangeListener;
import android.widget.Toast;

public class RatingBarView extends Activity {

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.ratingbarview_layout);
        RatingBar rating_bar = (RatingBar) findViewById(R.id.ratingbar);
        rating_bar.setOnRatingBarChangeListener(new OnRatingBarChangeListener() {
            @Override
            public void onRatingChanged(RatingBar ratingBar, float rating, boolean fromUser) {
                Toast.makeText(RatingBarView.this, "User Rating is: " + rating, Toast.LENGTH_LONG).show();
            }
        });
    }
}
```
