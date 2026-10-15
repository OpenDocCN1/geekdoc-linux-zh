
### `XBell(display, percent);`

指定与 X 器的连接。

`display`

指定铃声的音量，范围从 -100 到 100（包含）。

`percent`

如果指定的值相对于键盘的基础音量，则 `XBell` 函数会在指定的显示器键盘上响响铃声。如果 `percent` 参数的值不在 -100 到 100 的包含范围内，将产生 `BadValue` 错误。当 `percent` 参数为非负时，铃声响响的音量为：

- `base - [* base percent*) / 100] + percent`

当 `percent` 参数为负时，铃声响响的音量为：

- `base + [* base percent*) / 100`

要更改基础音量，请使用 `XKeyboardControl`。

`XKeyboardControl` 可以产生 `BadMatch` 和 `BadValue` 错误。

要获取键盘的状态，请使用 `XQuerymap`。

### `XQuerymap(display, keys_return);`

指定与 X 器的连接。

`display`

返回键盘的状态。

`keys_return`

`XQuerymap` 函数返回键盘的状态。数组中的每个位表示相应的键是否启用自动重复。

要设置映射，请使用 `SetPointerMapping`。

```c
int SetPointerMapping(display, map[]);
```

指定与 X 器的连接。

`display`

指定映射列表。

`map`

指定映射中的元素数量。

`nmap`

`SetPointerMapping` 函数设置指针映射。按钮从1开始编号，`SetPointerMapping` 返回按钮的数量。指针的映射为 `map[i]+=1`。`nmap` 参数指定返回指针映射的数组长度，并在 `map_return` 中返回前 `nmap` 个元素。要获取指针映射，请使用 `SetPointerMapping`。

```c
int SetPointerMapping(display, map_return, nmap);
```

`display` 指定与 X 器的连接。

`map_return` 返回映射列表。

`nmap` 指定映射列表中的元素数量。

要控制指针的交互感，请使用 `XChangePointerControl`.

### `XChangePointerControl(display, do_accel, do_threshold, accel_numerator, accel_denominator, threshold);`

`display` 指定与 X 器的连接。

`do_accel` 是一个布尔值，控制使用 `accel_numerator` 还是 `accel_denominator`。

`do_threshold` 是一个布尔值，控制使用 `threshold` 值。

`accel_numerator` 指定加速系数的分子。

`accel_denominator` 指定加速系数的分母。

`threshold` 指定加速阈值。

`XChangePointerControl` 函数定义指针设备的移动方式。加速以分数形式表示，是移动的系数。例如，指定 3/1 表示指针移动比正常快三倍。由 X 服务器任意舍入。只有当指针移动超过阈值像素时，加速才会生效，且仅适用于超过阈值的部分。将值设置为 -1 可恢复默认值。`do_accel` 和 `do_threshold` 参数必须为 True 才能设置指针值，否则参数保持不变。负值（-1 除外）产生 `BadValue` 错误，即 `accel_denominator` 参数。

`XChangePointerControl` 可能会产生 `BadValue` 错误。

要获取当前指针参数，请使用 `XGetPointerControl`.

### `XGetPointerControl(display, accel_numerator_return, accel_denominator_return, threshold_return);`
