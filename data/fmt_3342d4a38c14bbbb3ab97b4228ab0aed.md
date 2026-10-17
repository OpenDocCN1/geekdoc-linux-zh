
在用 Python 访问 GPIO 引脚时，出现了一个新的“新面孔”：`GPIO Zero` 库。不要把它与 Pi Zero 混淆 —— 两者之间没有关系。`GPIO Zero` 库采用类方法的方法进行控制，而不是 `RPiGPIO` 和其他库所使用的函数方法。引脚变成了 Python 对象，在使用之前必须对它们进行设置。尽管有这些复杂性，但使用这个系统仍然非常简单。例如，对于我们的 LED 闪烁示例，我们可以使用列表 16-3 中的代码。

### 列表 16-3：Python LED 闪烁

```python
#!/usr/bin/python3
import os
import time
import gpiozero as io # 使用 LED

led = io.LED(4) # 将引脚 4 设置为输出

print("LED blink using gpiozero - By Mike Cook")
print("Ctrl C to quit")
while True:
    led.on()
    time.sleep(0.30)
    led.off()
    time.sleep(0.30)
```

列表 16-3 看起来与列表 16-1 中的代码非常相似，但这仅仅是因为我们为了这种需求而那样写它。此库只使用 BCM 编号方法，因此不需要告诉库使用哪种系统。输出引脚被称为 `LED`，无论该引脚控制的是 LED、电电机还是芯片。因此，使引脚变为输出的行代码是 `io.LED(4)`。这段代码段返回一个指向类对象的引用。类和对象是我们第 17 章中涵盖的主题，在书中我们将描述如何编写它们，但基本上，它是一种获取代码片段来处理不同特定对象的方法 —— 在此特殊情况下，即不同的 GPIO 引脚。为了知道它需要做什么，每个物体/引脚必须单独声明，当声明时，程序会获得一个代码编号来识别它必须处理的哪个特定物体。该代码编号在列表 16-3 示例中被放在一个名为 `led` 的变量中，但也可以命名为任何名称。（此变量被称为实例引用。）类具有与其关联的方法 —— 换句话说，它能做的事情 —— 这些方法通过编写实例引用变量名、后跟一个点（`.`）、然后是方法名来调用的。开启或关闭 LED 是一个简单的过程 —— 你只需要写 `led.on()` 或 `led.off()` 即可。然而，在某种意义上，这有一点局限。例如，你不能在用于开启或关闭 LED 的变量中花费时间 —— 它必须具体地被写为一个方法名。这是 GPIO 工作方式的一种局限性。有方法可以避免这一点，但到那时，简单的系统就会变得复杂。

事实上，列表 16-3 的编写方式看起来与之前的列表相似。同样的内容可以简单地如列表 16-4 所示。

### 列表 16-4：简单的 LED 闪烁

```python
from gpiozero import LED
led = LED(4)
led.blink()
```

这就是你需要的所有了。除了连接硬件所需的实践技能外，我们不确定你从中从中学到什么，但它对初学者很有帮助。最后那句声明可以包含一些参数来控制闪烁频率 —— 例如，为了完全匹配我们的示例，最后一行可以写：

```python
led.blink(on_time = 0.3, off_time = 0.3)
```

这个库还有更多压箱底。如果你想让 LED 渐变亮，而不仅仅是闪烁，最后一行可以写：

```python
led.blink(on_time = 2.0, off_time = 2.0, fade_in_time = 1.0,
fade_out_time = 1.0 )
```

如果你只想这样做，这就太棒了，而且对于非常年轻的初学者来说，这正是你想做的。

由按钮控制的闪烁速度可以如列表 16-5 所示编写。

### 列表 16-5：按钮控制 LED 的 GPIO zero 示例

```python
#!/usr/bin/python3
import time
import os
import gpiozero as io # 使用 GPIO

led = io.LED(4)               # 将引脚 4 设置为输出
push = io.Button(24)     # 将引脚 24 设置为输入

print("LED blink using gpiozero - By Mike Cook")
print("Ctrl C to quit")
while True:
    led.on()
    if push.is_pressed:
        time.sleep(0.30)
    else:
        time.sleep(1.00)
    led.off()
    if push.is_pressed:
        time.sleep(0.30)
    else:
        time.sleep(1.00)
```

输入的工作方式与输出类似。在这种情况下，你创建一个 `Button` 类的实例，并将其引用放在变量 `push` 中。然后你使用该类的 `is_pressed` 方法来确定闪烁的延迟。默认情况下，在创建类时会启用上拉电阻。此输入中还包含其他选项。

## 开始使用骰子显示器
