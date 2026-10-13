
```python
def show(self):
    io.output(self.da, io.LOW)
    for i in range(0,32): # send header
        io.output(self.ck, io.LOW)
        io.output(self.ck, io.HIGH)
    for i in range(0,self.numLeds):
        d = self.ledArray[i] # send led
        for j in range(0,32):
            io.output(self.ck, io.LOW)
            if d & 0x80000000:
                io.output(self.da, io.HIGH)
            else:
                io.output(self.da, io.LOW)
            d = d << 1
            io.output(self.ck, io.HIGH)
    io.output(self.da, io.LOW)
    for i in range(0,33+(self.numLeds>>1)): # send footer
        io.output(self.ck, io.LOW)
        io.output(self.ck, io.HIGH)
```

注意看类名是否与文件名几乎相同？唯一的区别是文件名是小写字母。保持这种区别是非常重要的，因为这允许类被正确识别。每个方法的定义方式与函数一样。在 `__init__` 函数中，你会注意到许多变量以 `self` 开头。这是为了告诉编译器，该变量属于类本身，如果该类有多个实例，该变量实际上可以有不同的值。

通过查看函数名，你可以轻松判断出每个方法的作用。当你使用 `setBrightness` 时，发生的只是设置了一个变量，然后可以使用该变量来设置未来 LED 设置的亮度。注意，它不会影响 LED 的当前亮度。如果你愿意，可以写一个设置当前亮度的方法——这涉及到将新的亮度级别添加到列表中的所有 LED 中，并调用 `show` 方法。

来看下实际效果，我们使用了 Pimoroni Blinky 灯带，这是一种廉价的 `APA102C` 灯带，它可以覆盖所有的 40 个 `GPIO` 引脚，尽管它只使用了两个 `GPIO` 引脚用于电源 `[5V]` 和地线。列表 17-4 显示了一个用于使用该类的程序。请确保将其保存到与类文件相同的文件夹中。

# 列表 17-4: 使用 APA102 类

```python
#!/usr/bin/env python3
# demo1 Apa102bang class driver

import time
from apa102bang import Apa102bang

length = 8 ; brightness = 4
dataPin = 23 ; clockPin = 24 # Blinkyti! wiring
led = Apa102bang(length,dataPin,clockPin,wiring)

def main():
    print("APA102 demo - Ctrl C to stop")
    while True:
        for i in range(0,8):
            led.setled(i,(1,120,0)) # red
            led.show()
            time.sleep(0.06)
        time.sleep(0.6)
        for i in range(0,4):
            led.setled(i,(0,120,0)) # green
            led.show()
            time.sleep(0.06)
        time.sleep(0.6)
        for i in range(4,8):
            led.setled(i,(0,0,120)) # blue
            led.show()
            time.sleep(0.06)
        time.sleep(0.6)
        for i in range(0,8):
            led.setled(i,(0,0,0)) # black
            led.show()
            time.sleep(0.06)
        time.sleep(0.6)

# 主程序逻辑：
if __name__ == '__main__':
    main()
```

代码开始定义了你拥有的 LED 数量、想要运行的亮度以及用于数据线和时钟线的引脚。这些行是由 Blink! 制作决定的，但如果你想尝试连接到树莓派的更多灯带，可以使用任何两个 `GPIO` 引脚。`led` 变量被设置为类引用——通过点符号和方法名使用此引用来调用任何方法。程序简单地轮流将每个 LED 设置为三种原色并再次反之。注意在 `setLED` 方法中，颜色是以元组中的三个值给出的。是 `show` 方法实际上将数据缓冲区中的内容显示在 LED 上。如果你不调用方法，LED 就不会发生变化。

尽管这些都非常有趣，但运行此程序的结果并不壮观——所以让我们用这个小 LED 灯带做一个游戏吧。

## 树莓派入侵者 (Raspberry Invaders)

要启动这个项目，你要的第一件事是构建硬件。遗憾的是，添加按钮比想象的要复杂一点。有两种方法：你可以将按钮焊接在灯带背部，或者使用 `GPIO` 引脚。

游戏的软件部分是魔法发生的地方。我们使用 `apa102bang` 类来控制 LED，并使用 `pygame` 库处理图形和输入。游戏非常简单：你在屏幕上移动飞船并射击小行星。如果小行星击中你，你就会失去一条生命。如果你击中小行星，就会获得积分。

游戏的代码将在接下来的页面中显示。它有点长，但它是学习如何使用 LED 和树莓派的极佳方法。

## 列表 17-5: (续)

```python
setBombCol()
  return score
```

```python
def setBombCol():
    global bombCol
    gameSound[0].play() # 炸弹到来
    while t:
        r = random.randint(0,1) * 128
        g = random.randint(0,1) * 128
        b = random.randint(0,1) * 128
        if not(r==0 and g==0 and bombCol != (r,b)):
            break
        bombCol = (r,g,b)
```

```python
def init():
    global fireR,fireG,fireB,beam,sky,gameSpeed,base
    random.seed()
    io.setmode(io.BCM)
    fireR = 4 ; fireG = 3 ; fireB = 2
    io.setup([fireR,fireG,fireB],io.IN,pull_up_down=io.PUD)
    beam = getBeam()
    length = 8 ; brightness = 4
    sky = Apa102bang(26,23,24,brightness)
    gameSpeed = 0.3 * the speed of game in
    pygame.mixer.quit()
    pygame.mixer.init(frequency=22050, size=-16, channels=2)
    base = [[0,0,0],[32,0,32],[0,64,0],[0,128,128]] # 基座颜色
    soundEffects = ['ComputerBeeps2','Layer1','Pop','Screech']
    gameSound = [pygame.mixer.Sound("sounds/" + soundEffects[i] + ".wav")]
```

```python
# 主程序逻辑：
if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        pass
    # 关闭所有 LED
    sky.setAll((0,0,0))
    sky.show()
```

374 第 5 部分 使用树莓派探索电子

`main` 函数由两个大循环组成，是动作发生的地方。
