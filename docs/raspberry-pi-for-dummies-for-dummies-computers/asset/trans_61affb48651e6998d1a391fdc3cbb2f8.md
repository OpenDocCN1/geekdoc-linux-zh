

```python
def main():
    global lastTraffic, state, bleep
    print("行人交叉模拟器 Ctrl C 退出")
    initIO()
    io.output(green,1) # 绿灯开启启动
    state = 0
    bleepTime = time.time()
    bleep = False
    lastTraffic = time.time()
    while 1:
        checkTraffic()
        if checkRequest() and state == 0 :
            io.output(noCross,1) # 开启禁止通行灯
            if time.time() - lastTraffic > 10.0: # 立即过通过
                state = 1
        else:
            time.sleep(10.0) # 让交通流动一会
            state = 1
        crossSequenceFunction()
        if bleep and time.time() > bleepTime:
            bleepTime = time.time() +0.3
            io.output(sounder,not(io.input(sounder)))
```

```python
def checkTraffic():
    global lastTraffic
    if io.input(trafficSensor) == 0:
        lastTraffic = time.time()
```

```python
def checkRequest():
    request = False
    if io.input(crossRequest) == 0:
        request = True
    return request
```

```python
def crossSequenceTime(countFlash, state, bleep):
    if state == 0:
        nextSequenceTime = time.time() + 2.0
        return
    if time.time() > nextSequenceTime :
        if state == 1: # 显示黄灯
            print("doing state",state)
            io.output(green,0)
            io.output(amber,1)
```

## 第 16 章 控制你的树莓派电路

# 列表 16-11：（（续）

```python
state = 2
nextSequence = time.time() + 2.0 # 显示黄灯持续时间
elif state == 2: # 显示红灯
    print("doing state",state)
    io.output(amber,0)
    io.output(red,1)
state = 3
nextSequence = time.time() + 2.0 # 显示红灯持续时间
elif state == 3: # 显示禁止通行灯
    print("doing state",state)
    io.output(noCross,0)
    io.output(cross,1)
bleep = True
state = 4
nextSequence = time.time() + 5.0 # 通行时间
elif state == 4: # 变为黄灯清除通过
    print("doing state",state)
    io.output(amber,1)
    io.output(red,0)
bleep = False
    io.output(sounder,0) # 关闭蜂鸣器
state = 5
nextSequence = time.time() + 1.0
elif state == 5: # 黄灯和通行灯闪烁
    print("doing state",state)
    io.output(amber,not(io.input(amber)))
    io.output(cross,not(io.input(cross)))
nextSequence = time.time() + 0.2 # 闪烁速度
countFlash+=1
if countFlash > 20: # 清除通过时间 20 # 闪红灯
countFlash = 0
state = 6
elif state == 6: # 保持黄灯
    io.output(cross,0)
    io.output(noCross,1)
    io.output(amber,1)
state = 7
nextSequence = time.time() + 2.0 # 保持黄灯
elif state == 7: # 开启红灯
    print("doing state",state)
    io.output(amber,0)
```

```python
io.output(green,1)
io.output(noCross,0)
state = 0
nextSequenceTime = time.time() + 1.0
```

```python
def initGPIO():
    global red, amber, green, noCross, cross, countFlash, sounder
    io.setmode(io.BCM)
    io.setwarnings(False)
    for pin in range(0,len(control)):
        io.setup(LEDControl[pin],io.OUT) # 将引脚设为输出
        io.output(LEDControl[pin],0) # 设置为零
    io.setup(crossRequest,io.IN,pull_up_down=io.PUD_UP) # 将引脚设为输入
    io.setup(LEDControl[0])
red = LEDControl[0]
amber = LEDControl[1]
green = LEDControl[2]
noCross = LEDControl[3]
cross = LEDControl[4]
sounder = LEDControl[5]
countFlash = 0
```

- 主程序逻辑：
if __name__ == '__main__':
    main()

逐步分析此程序，首先注意 GPIO 引脚已初始化，并且列表中的每个引脚都分配了自己的名称。这使得程序易于阅读，尽管我们本可以使用“魔数”（一个在没有明显原因的情况下出现的数字——即 GPIO 列表中的索引）。在主函数的无限循环中，会测量交通活动情况，然后检查过路按钮。`checkRequest` 函数在按钮被按下时返回 `True` 值。这意味着该函数可以直接在 `if` 语句内部——不需要中间变量。此外，通过 `if` 语句可以检查是否正在运行通过序列。

