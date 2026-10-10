
# 设置电影剪属性

## 应用

你可以使用此脚本在用户每次点击时增加电影剪的高度。该脚本获取名为 `block` 的电影剪的高度，并将该值赋值给名为 `height` 的变量。然后，它将 `block` 电影剪的高度设置为 `height` 的值加 10。你可以使用 `setProperty` 动作来设置电影剪的高度。有关 `setProperty` 动作的更多信息，请参阅第 64 页。

## 输入此：

```
on (release) {
  heightV = block._height;
  setProperty("block._height", heightV + 10);
}
```

## 结果：

每当用户点击按钮时，电影剪的高度就会增加 10 像素。

| 对象动作 |
| --- |
| 25 个对象动作 |
| + 对象动作 |
| - 基础动作 |
| - 动作 |
| on (release) {_height=200;} |
| - 运算符 |
| - 函数 |
| 属性 |
| - mc |
| _myinstance |
| _dropzone |
| _framestate |
| _height |
| _highquality |
