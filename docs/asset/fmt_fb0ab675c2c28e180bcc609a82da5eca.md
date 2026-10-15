
## Status XmsCIELuvQueryMinL

`Status XmsCIELuvQueryMinL(ccc, hue_angle, chroma, color_return)`:

- `ccc`: 指定 CCC。忽略 CCC 的客户端白点和白点调整程序。
- `hue_angle`: 指定用于寻找最小亮度的色角（单位：度）。
- `chroma`: 指定用于寻找最小亮度的色度。
- `color_return`: 返回在给定角度和色度下，屏幕可显示的最小亮度 CIE L*a*b* 坐标。与返回的颜色规范相关的白点是屏幕白点。`pixel` 成员中返回的值是未定义的。

`XmsCIELuvQueryMin` 函数在色角和色度的情况下，寻找屏幕可显示的最小亮度 (L*) 点。它以 CIE L*a*b* 坐标返回。`XmsFailure` 返回值通常表示给定的色度超过了给定色角的最大值。

L*u*v* 坐标。返回 `XcmsFailure` 返回值通常表示给定的色度（Chroma）超过了最大色角。

### TeKHVC 查询

要获取给定色相（Hue）和亮度（Value）的最大色度，请使用 `XcmsTekHVCQueryMax`。

`Status XcmsTekHVCQueryMax(ccc, hue, value, color_return);`

- `ccc`: 指定 CCC。忽略该 CCC 的客户端白点和白点调整程序。
- `hue`: 指定要查找最大色度的色相。
- `value`: 指定要查找最大色度的亮度。
- `color_return`: 返回最大色度以及找到最大色度时的实际色相和亮度。与返回的颜色规格关联的白点是屏幕白点。像素米（pixel meter）中返回的值未定义。

`XcmsTekHVCQueryMax` 函数在给定色相和亮度的情况下，确定 TeKHVC 色空间中屏幕可显示的最大色度。它返回最大色度以及找到最大色度时的实际色相和亮度。

要获取给定色相和色度的最大亮度，请使用 `XcmsTekHVCQueryMaxV(ccc, hue, chroma, color_return);`

`Status XcmsTekHVCQueryMaxV(ccc, hue, chroma, color_return);`

- `ccc`: 指定 CCC。忽略该 CCC 的客户端白点和白点调整程序。
- `hue`: 指定要查找最大亮度的色相。
- `chroma`: 指定要查找最大亮度的色度。

`XcmsTekHVCQueryMaxV` 函数在给定色相和色度的情况下，确定 TeKHVC 色空间中屏幕可显示的最大亮度。它返回最大亮度以及找到最大亮度时的实际色相和色度。

要获取指定色相的最大色度以及达到该色度的亮度，请使用 `XcmsTekHVCQueryMaxV`。

## 颜色管理函数

`Status XcmsTekhHVCQueryMaxVC(ccc, hue, color_return);`

`ccc`: 指定 CCC。忽略该 CCC 的客户端点和白点调整程序。

`hue`: 指定最大色度所在的色相。

`color_return`: 返回 `XcmsTekhHVC` 中最大色度的颜色规格、达到最大色度的亮度，以及找到最大色度的实际色相。与返回的颜色规格关联的白点是屏幕白点。像素成员（pixel member）中返回的值未定义。

`XcmsTekhHVCQueryMaxVC` 函数在给定色相的情况下，确定 TehVC 色空间中屏幕可显示的最大色度以及达到最大色度的亮度。它返回最大色度、达到该最大色度的亮度以及找到最大色度的实际色相。

要获取包含指定色相的最大亮度以及达到该最大亮度的色度的指定数量 TehVC 规格，请使用 `XcmsTekhHVCQueryMaxVSamples`。

`Status XcmsTekhHVCQueryMaxVSamples(ccc, hue, colors_return(), namples);`

`ccc`: 指定 CCC。忽略该 CCC 的客户端点和白点调整程序。

`hue`: 指定最大色度/亮度样本的色相。

`namples`: 指定样本数量。

`colors_return`: 返回 `namples` 个 `XcmsTekhHVC` 颜色规格，使得色度对于该色相是可实现的最大值。与返回的颜色规格关联的白点是屏幕白点。像素成员（pixel member）中返回的值未定义。

`XcmsTekhHVCQueryMaxVSamples` 返回 `namples` 个最大亮度、达到该亮度的色度以及找到最大色度的实际色相。这些样本点随后可以绘制 TehVC 空间中屏幕色域的最大亮度/色度边界。

要获取给定色相和色度的最小亮度，请使用 `XcmsTekhHVCQueryMinV`。

`Status XcmsTekhHVCQueryMinV(ccc, hue, chroma, color_return);`

`ccc`: 指定 CCC。忽略该 CCC 的客户端点和白点调整程序。

`hue` 指定要查找最小亮度的色相。

`value` 指定要查找最小亮度的亮度。

`color_return` 这里的最小亮度以及找到最小亮度的实际色度。与返回的颜色规格关联的白点是屏幕白点。像素米（pixel meter）中返回的值未定义。

`XcmsTekHVCQueryMinV` 函数在给定色相和色度的情况下，确定 TekHVC 色空间中屏幕可显示的最小亮度。它返回最小亮度以及找到最小亮度的实际色相和色度。

## 颜色管理扩展

Xlib 颜色管理设施可以通过两种方式扩展：

- 设备无关色空间
- 可以使用 `XcmsAddColorSpace` 函数添加可以导出到 CIE XYZ 空间的设备无关色空间。

- 颜色特性化函数集
- 颜色特性化函数集由设备相关色空间以及在这些色空间与 CIE XYZ 颜色空间之间转换的函数组成，针对特定类的输出设备封装在一起。可以使用 `XcmsAddFunctionSet` 添加函数集。

## 色空间

XYZ 色空间作为设备无关色空间和设备相关色空间之间所有转换的枢纽。因此，将 Xcms 颜色转换为 CIE XYZ 格式的知识与每个色空间相关。例如，从 CIE L*u*v* 转换为 RGB 需要将 Xcms 颜色转换为 CIE XYZ 格式的知识。

## 添加设备无关色空间

要添加设备无关色空间，请使用 `XcmsAddColorSpace`。

## 颜色管理函数

`Status XcmsAddColorSpace(color_space);`

`color_space` 指定要添加的设备无关色空间。

`XcmsAddColorSpace` 函数使设备无关色空间（实际上是 `XcmsColorSpace` 结构）可供颜色系统访问。由于未注册色空间的格式是在运行时分配的，因此应视为私有。对未注册色空间的引用必须在客户端外部进行（例如，将颜色规格存储在文件中），然后使用 `XcmsFormatOfPrefix` 和 `XcmsPrefixOfFormat`。

如果 `XcmsColorSpace` 结构已经在颜色系统中可用，`XcmsAddColorSpace` 返回 `XcmsSuccess`。

注意，Xlib 必须保留 `XcmsColorSpaces`。

### 查询色空间格式和前缀

要获取与指定颜色字符串前缀关联的格式，请使用 `XcmsFormatOfPrefix`。

`XcmsColorFormat XcmsFormatOfPrefix(prefix);`

`prefix` 指定包含色空间前缀的字符串。

`XcmsFormatOfPrefix` 函数返回指定色空间前缀的格式（例如字符串 `"CIEXY"`）。大小大小敏感。如果色空间在颜色系统中不可，`XcmsFormatOfPrefix` 返回 `XcmsUndefinedFormat`。

要获取与指定格式关联的颜色字符串前缀，请使用 `XcmsPrefixOfFormat`。

`char * XcmsPrefixOfFormat(format);`

`format` 指定颜色规格格式。

`XcmsPrefixOfFormat` 函数返回与格式关联的字符串前缀。否则，如果未找到编码，则返回 NULL。返回的字符串必须视为只读。

## 创建额外的色空间

色空间转换和颜色字符串解析所需的颜色特定信息存储在 `XcmsColorSpace` 结构中。因此，每个额外的色空间都需要包含此信息的新结构。在设备无关色空间的情况下，此新结构的句柄（通过全局变量）通常对客户端程序可见，用于 `XcmsAddColorSpace` 函数。

如果新的 `XcmsColorSpace` 结构指定了未在 X 协会注册的色空间，应将其视为私有，因为未注册色空间的格式是在运行时分配的。对未注册色空间的引用必须在客户端外部进行（例如，将颜色存储在文件中），然后使用 `XcmsFormatOfPrefix` 和 `XcmsPrefixOfFormat`。

## 颜色管理函数

（在使用未注册颜色空间的文件的规范中），然后应通过颜色空间前缀进行引用（参见 `XmsFormatOfPrefix` 和 `XmsPrefixOffFormat`）。
