
```
(gimp-palette-set-foreground old-fg)
(gimp-palette-set-background old-bg)
```

让我们添加其他让脚本更具配置性的变量：

- `SF-COLOR` "字体颜色：`$(0 0 100)`

- `SF-COLOR` "深色偏移颜色：`$(0 0 0)`

- `SF-COLOR` "浅色偏移颜色：`$(255 255 255)`

- `SF-ADJUSTMENT` "模糊半径：`$(2 1 50 1 10 0 0)`

- `SF-ADJUSTMENT` "深色偏移：`$(1 -100 100 1 10 0 1)`

- `SF-ADJUSTMENT` "浅色偏移：`$(1 -1 100 100 1 10 0 1)`

### 6.3.3.6 完成的脚本

适当变量已添加到 `define` 函数中，变量名已替换硬编码变量。我们完成的脚本如下：

```
(define
(script-fu-alexh-logo textStuff fontType fontSize fontColor
bgColour offset lightOffset
blurRadius posoffset negaffset )
```

# 编写你自己的 Script-Fu：增强脚本 101

```
; 开始脚本
(let*
(
; 声明宽度和高度变量并分配一个哑值
(imgWidth 1)
(imgHeight 1)

; 声明并创建新图像
(img
(car
(gimp-image-new imgWidth imgHeight RGB))

; 声明并创建图像中的图层：
(bgLayer)
(car
(gimp-layer-new img imgWidth imgHeight
RGB_IMAGE "Background" 100 NORMAL))
)
(baseLayer)
(car
(gimp-layer-new img imgWidth imgHeight
RGB_IMAGE "Text Layer" 100 NORMAL))
)

; 留背景颜色
(old-fg (car (gimp-palette-get-foreground)))
(old-bg (car (gimp-palette-get-background)))
)

; 禁用撤销记录
(gimp-image-disable-undo img)

; 将图层添加到图像
(gimp-image-add-layer img bgLayer @)
(gimp-image-add-layer img baseLayer @)

; 设置前景和背景颜色
(gimp-palette-set-background bgColor)
(gimp-palette-set-foreground fontColor)

; 清除背景层
(gimp-edit-clear img bgLayer)

; 添加透明通道并清除文本图层
(gimp-layer-add-alpha baseLayer)
(gimp-edit-clear baseLayer)

; 创建新的文本图层
```

继续...

```
(let*
(
(floatText
(car
  (gimp-text-fontname img baseLayer @ 0 textStuff 5 TRUE fontSize PIXELS
ype)
)
(blackblurLayer)
(whiteblurLayer)
)
)
```

; 调整图像到合适尺寸

```
(set imgWidth (car (gimp-drawable-width floatText ))
(set imgHeight (car (gimp-drawable-height floatText )) )
```

```
(gimp-image-resize imgWidth imgHeight @ 0)
(gimp-layer-resize bLayer imgWidth imgHeight @ 0)
(gimp-layer-resize baseLayer imgWidth imgHeight @ 0)
(gimp-layer-set-offsets blackLayer 1 1)
```

# 102 编写你自己的 ScriptFu：增强脚本

```
(gimp-layer-preserve-trans blackLayer FALSE)

(gimp-layer-preserve-trans whiteblurLayer FALSE)

(plug-in-gauss-iir TRUE img blackblurLayer 2 TRUE)

(plug-in-gauss-iir TRUE img whiteblurLayer 2 TRUE)
```

# 104 编写你自己的 Script-Fu：在图像或绘制图上使用 Script-Fu

我们将通过以下步骤完成：

- 1. 将图像复制一份新图像。
- 2. 当剩余帧数大于1时，循环：
   a. 复制基础层。
   b. 将其重命名为剩余帧数。
   c. 进行一定程度的像素化（Pixelize）。
   d. 减少帧数和像素化程度。
- 3. 将基础层重命名为 Frame 1。
- 4. 清理工作。

只需要两个变量：

- 最大像素化值
- 帧数

### 6.3.4.1 定义函数

编写脚本的第一步是创建 `define` 函数和 `script-fu-register` 函数：

```scheme

(define script-fu-pixel-anim img drawable maxPixel totalFrames)

(script-fu-register "script-fu-pixel-anim"

  "<Image>/Script-Fu/Animators/Pixelate"

  "超级马里奥风格的图像像素化"

  "Alex Harford (alexh@edowco.com)"

  "Copyright 1999 Alex Harford"

  "July 21, 1999"

  "RGB RGBA GRAY GRAYA" @

  SF-IMAGE "Image" @

  SF-DRAWABLE "Drawable" "Max Pixelization" (10 1 100 1 10 0 0)

  SF-ADJUSTMENT "Number of Frames" (10 1 100 1 10 0 1))

```

注意，这里有两个额外的变量：`img` 和 `drawable`。这些变量由 GIMP 自动传递给脚本，因为它们应用于特定图像上的特定绘制图。在编写影响现有图像的脚本时总是会使用。还要注意此滤器的位置：`<Image>/Script-Fu/Animators/Pixelate`。通常，作用于现有图像的脚本放在 `<Image>/Script-Fu` 部分。

### 6.3.4.2 分配变量

现在脚本的骨架已经到位，我们可以开始创建脚本。它从一个 `let*` 函数开始：

```scheme

(let*

  ; 声明变量并赋值

  (maxPixel (max 1 maxPixel))

  (totalFrames (max 1 totalFrames))

  (delta (/ maxPixel totalFrames))

  (framesleft totalFrames)

  (image (car (gimp-channel-ops img)))

  (base-layer (car (gimp-get-active-layer image))))

)

```

此函数完成了几项工作：

- 确保 `maxPixel` 和 `totalFrames` 大于 1。
- 声明变量 `delta` 并将其初始化为 `maxPixel` 除以 `totalFrames` 的结果。
- 声明变量 `framesLeft` 并将其初始化为 `totalFrames`。
- 声明新变量 `image`，并将其设置为 GIMP 传递给脚本的活动图像的副本。
- 声明变量 `base-layer` 并将其初始化为图像中的活动层。

### 6.3.4.3 像素化

现在我们必须决定如何处理实际的像素化。这是通过一个 `while` 循环和一个 `let*` 函数实现的：

```scheme

(while (> framesLeft 1)

  (let*

    (

      (pixel-layer (car (gimp-layer-copy base-layer TRUE)))

      (layer-name (string-append "Frame " (number->string framesLeft)))

    )

    (gimp-image-add-layer image pixel-layer (- totalFrames framesLeft))

    (gimp-layer-set-name pixel-layer layer-name)

    (plug-in-pixelize

      TRUE

      image

      pixel-layer
```
