
`XallocNamedColor` 函数根据与指定颜色表相关的屏幕查找命名颜色。它同时返回精确的数据库定义和屏幕支持的最接近的颜色。分配的颜色是只读的。像素值在 `screen` 中返回。如果颜色名称不在主机可用的字符编码（Hostable Character Encoding）中，结果取决于实现。使用大写或小写均可。如果 `screen_def_return` 和 `exact_def_return` 指向同一个结构，则像素字段将正确设置，但颜色值是未定义的。`XallocNamedColor` 如果分配了颜色，返回非零值；否则返回零。

`XallocNamedColor` 可能会产生 `BadError`。

要使用名称分配只读颜色，并以任意格式返回硬件支持的最接近的颜色，请使用 `XcmsAllocNamedColor`。

| `Status XcmsAllocNamedColor(display, colormap, color_string, color_screen_return, color_exact_return, result_format);` |  |
| :--- | :--- |
| `display` | 指定到 X 服务器的连接。 |
| `colormap` | 指定颜色表。 |
| `color_string` | 指定要返回颜色定义结构的颜色字符串。 |
| `color_screen_return` | 返回实际存储在该单元的颜色单元像素值和颜色规格。 |
| `color_exact_return` | 返回从颜色字符串解析出或从颜色名称数据库中找到的对应字符串解析出的颜色规格。 |
| `result_format` | 指定返回的颜色规格的颜色格式（`color_screen` 和 `color_exact-return` 参数）。如果格式是 `XmsRGBFormat`，则可以跳过不必要的拷贝。相应的颜色表是只读的。如果你的函数返回 `XmsFree`，则颜色或颜色规格将保持不变。 |

`XcmsAllocColor` 可能会产生 `BadError`。

每个掩码都位于对应的像素子字段内。通过将每个像素值的多个掩码子集进行或（OR）操作，可以产生 `ncolors x 2^(nred+ngreen+nblue)` 个不同的像素值。所有这些都由请求分配。然而在调色板（colormap）中，有 `ncolors x 2^nred` 个独立的红色条目、`ncolors x 2^ngreen` 个独立的绿色条目以及 `ncolors x 2^nblue` 个独立的蓝色条目。对于伪彩色（PseudoColor）而言如此。当使用 `XStoreColor`、`XStoreNamedColor` 修改像素值的调色板时，像素将根据掩码进行解码，并更新这些独立条目。`XAllocColorPlanes` 成功时返回非零，失败时返回零。

`XAllocColorPlanes` 可以产生 `BadArgument` 和 `BadValue` 错误。

要释放调色板，请使用 `XFreeColors`。

```
XFreeColors(display, colormap, pixels[], npixels, planes);
```

- `display` 指定与 X 服务的连接。
- `colormap` 指定调色板。
- `pixels` 指定一个像素值数组，这些值映射到指定调色板中的单元。
- `npixels` 指定像素数量。
- `planes` 指定你想要释放的平面。

`XFreeColors` 函数释放由 `pixels` 数组中值为 1 的像素所表示的单元。`planes` 参数不应与 `pixels` 中的任何一个像素具有共同的置为 1 的位。通过将 `planes` 参数的子集与请求进行或（OR）操作产生的所有像素集，将释放由客户端分配的所有这些只读单元（使用 `XAllocColor`、`XAllocNamedColor`、`XAllocColorCells` 和 `XAllocColorPlanes`）。请注意，释放从 `XAllocColorPlanes` 获取的单个像素，在所有相关平面都被释放之前，实际上并不允许其被重用。同样，只读条目在被所有客户端释放之前实际上不会被释放，如果一个客户端多次调用同一个只读条目，该待释放的条目仍然存在。

如果一个或多个像素产生错误，则由客户端分配的所有像素都将被释放。如果指定的像素不是有效索引，则发生 `BadValue` 错误。如果指定的像素未由客户端分配（即未分配或由另一个客户端分配），或者调色板在创建时（通过 `XCreateColormap` 的 `AllocCall`）所有条目均为可写，则会发生 `BadAccess` 错误。如果有多个像素出错，报告的那个是随机的。

`XFreeColors` 可以产生 `BadAccess`、`BadColor` 和 `BadValue` 错误。

## 修改和查询调色板单元

要在单个调色板单元中存储 RGB 值，请使用 `XStoreColor`。

```
XStoreColor(display, colormap, color);
```

- `display` 指定与 X 服务的连接。
- `colormap` 指定调色板。
- `color` 指定像素和 RGB 值。

`XStoreColor` 修改 `XColor` 结构中 `pixel` 成员所指定像素值的调色板条目。你在 `XColor` 结构中 `pixel` 成员中指定此值。该像素值必须是一个可读/写单元，并且是调色板的有效索引。如果指定的像素不是调色板的有效索引，则发生 `BadValue` 错误。`XStoreColor` 同时更改红色、绿色和/或颜色分量。你通过设置 `XColor` 结构中 `flags` 成员的 `DoRed`、`DoGreen` 和/或 `DoBlue` 来指定更改哪些颜色分量。如果调色板是屏幕的安装映射，更改将立即可见。

`XStoreColor` 可以产生 `BadAccess`、`BadColor` 和 `BadValue` 错误。

要在多个调色板单元中存储多个 RGB 值，请使用 `XStoreColors`。

```
XStoreColors(display, colormap, color(i), ncolors);
```

- `display` 指定与 X 服务的连接。
- `colormap` 指定调色板。
- `color` 指定一个要存储的颜色定义结构数组。
- `ncolors` 指定颜色定义数组中 `XColor` 结构的数量。

`XStoreColors` 函数更改 `XColor` 结构中 `pixel` 成员所指定像素值的调色板条目。你通过设置 `XColor` 结构中 `flags` 成员的 `DoRed`、`DoGreen` 和/或 `DoBlue` 来指定更改哪些颜色分量。如果调色板是屏幕的安装映射，更改将立即可见。如果指定的像素由任何客户端分配在调色板中，则 `XStoreColors` 也会更改这些指定的像素，即使其中一个或多个像素产生了错误。如果指定的像素不是调色板的有效索引，则发生 `BadValue` 错误。如果指定的像素未分配或被分配为只读，则会导致 `BadAccess` 错误。如果有多个像素出错，报告的那个是随机的。

`XStoreColors` 可以产生 `BadAccess`、`BadColor` 和 `BadValue` 错误。

要在单个调色板单元中存储任意格式的颜色，请使用 `XcmsStoreColor`。

```
Status XcmsStoreColor(display, colormap, color);
```

- `display` 指定与 X 服务的连接。
- `colormap` 指定调色板。
- `color` 指定要存储的颜色和颜色。在此 `XcmsColor` 结构中指定的值在返回时保持不变。

# 颜色管理函数

`XmsColor` 将 `XmsColor` 结构中指定的颜色转换为 RGB 值。它在 `XColor` 结构中使用此 RGB 规范，其中三个标志（`DoRed`、`DoGreen` 和 `DoBlue`）被设置，并在 `XStoreColor` 中调用以更改由 `XmsColor` 结构中 `pixel` 成员所指定的颜色。此像素值必须是指定调色板的有效索引，且由像素值指定的颜色必须是可读/写的。如果像素值无效，则发生 `BadValue` 错误。如果调色板是屏幕的安装映射，更改将立即可见。注意 `XStoreColor` 没有返回值；因此 `XSuccess` 表示操作成功。
