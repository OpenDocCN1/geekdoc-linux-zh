
```python
#!/usr/bin/python3
## Mike Cook 编写的简单 RFID 唱胶机

from rc522rfid import Rc522rfid
import pygame

pygame.mixer.quit()
pygame.mixer.init(frequency=22050, size=-16, channels=2, buffer=512)
fidReader = Rc522rfid()
tokens = [0xf690ebb, 0xc3ba4ad5, 0xc9c35fdd, 0x8cd32ddee, 0xc6822ade, 0x1cb413de]
files = ["", "DrumMachine", "DrumSet1", "DrumSet2", "Eggs", "Drip"]

def main():
    print("Simple RFID Jukebox reader")
    print("Press Ctrl-C to stop")
    while True: # 无限循环
        cardNumber = rfidReader.RC522_GetCard()
        pygame.mixer.music.stop()
        for i in range(len(tokens)):
            try:
                pygame.mixer.music.load("/home/pi/Music/"+str(files[i])+".mp3")
                pygame.mixer.music.play()
                print("Playing-"++str(files[i])+".mp3")
            except:
                print("No file:-/home/pi/Music/" + str(files[i]) + ".mp3")

# 主程序逻辑：
if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        pass
```

你必须更改 `tokens` 列表为你拥有的卡片的令牌号，并将 `files` 列表匹配你拥有的声音文件。程序会自动添加 `.mp3` 前缀。所以，当你呈现卡片时，文件将通过 `Pygame` 系统播放。这里发生的情况是文件与 RFID 卡号之间的关系固定在列表中文件名的位置和卡号的位置上。这意味着列表中的第一个数字将触发列表中的第一个文件。

这虽然很好，但意味着每当我们想要更改东西时都必须编辑代码。如果卡片本身携带文件名，效果会好得多。

## 一个更好的 RFID 唱胶机

你可以让卡片携带文件名，但你需要一个程序来处理此任务。换句话说，这种注册是通过读取卡号并将其放入列表中完成的。在上节中，已经完成了这种注册。它还涉及复制目标文件夹中的文件名并将其添加到列表中。在更好的系统中，可以通过任何注册程序完成。这里的想法是有两个程序：一个用于响应卡片播放文件，另一个用于将文件名保存在卡片的 4 和 5 扇区。如果你选择注册一个卡片，文件名（包括扩展名）存储在卡片的第 4 和 5 段。注册程序如列表 18-3 所示。

### 列表 18-3：RFID 唱胶机注册程序

```python
#!/usr/bin/python3
## Mike Cook 编写的将文件名写入 4&5 扇区的 RFID注册

from rc522rfid import Rc522rfid
import os

def main():
    print("RFID enrolner")

    rfidReader = Rc522rfid()
(continued)
```

### 列表 18-3：继续

```python
print("Press Ctrl-C to stop")
getFiles()
for file in range(0,len(soundList)):
    action = ""
    print(soundList[file])
    print("Enroll (e) or just Skip")
    action = input()
    if action == "e":
        enroll(soundList[file])

def enroll(name):
    print("Enrolling", name, "place a card on the reader")
    data1 = []
    data2 = []
    for i in range(0,16): # 用全填充
        data1.append(0)
        data2.append(0)
    for i in range(0,len(name)):
        if i < 16:
            data1[i] = ord(name[i])
        else:
            data2[i-16] = ord(name[i])
    # 这是（默认）密钥身份验证
    key = [0xFF,0xFF,0xFF,0xFF,0xFF]
    rfid.RC522_WriteSector(key,4,data1)
    RFID.RC522_WriteSector(key,5,data2)
    print("finished enrolling\n")

def getFiles():
    global soundList
    path = os.path.abspath("/home/pi/Music/")
    # 获取文件列表
    soundlist = [fn for fn in next(os.walk(path))[2]]
    list.sort(soundlist) # 按字母顺序排序
    print(len(soundlist), "files found")

# 主程序逻辑：
if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        pass
```

`getFiles` 函数针对 `path` 变量中的特定文件夹，并搜索该文件夹，使用 `os.walk` 方法列所有找到的文件并创建一个列表。然后，该列表将按字母顺序排序，以获得一个用于录入选择的有序列表。接着，`main` 函数逐个显示文件名，你可以按 `e`（并按 `Enter`）来录入卡片，或直接按 `Enter` 键跳到下一个。`enroll` 函数接收文件名并将其分成两个 16 块（blocks），然后将其写入卡片。

像这样录入卡片后，最好用某种方式标记卡片，以显示哪些是你已经录入的。你可以通过许多方法实现这一点，从简单的手写标签到带有艺术家名字的复杂设计——甚至可以根据专辑进行设计。在彩色打印机上打印完成后，用喷雾胶将其贴在卡片上。最后用图书馆中常用的覆盖和保护书籍的透明塑料膜覆盖卡片即可完成。

制作好卡片后，你需要一个新程序来播放它们。这在列表 18-4 中所示。

### 列表 18-4：RFID 唱片机录入卡片播放

```python
#!/usr/bin/python3
## RFID Jukebox2 with track names on the card by Mike Cook

from rc52rfid import Rc52rfid
import pygame

pygame.mixer.quit()
pygame.mixer.init(frequency=22050
```

### 列表 18-4：（接续）
