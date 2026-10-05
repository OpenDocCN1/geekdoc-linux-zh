

# 列表 18-5：（接续）

```python
needsRedraw = False

def init():
    global clothes,cList
    path = os.path.realpath(__file__)
    path = os.path.dirname(path) + "/doll/"
    # 获取文件列表
    cList = [fn for fn in next(os.walk(path))[2]]
    list.sort(cList) # 按字母顺序排序
    print("files found")
    for i in range(0,len(cList)):
        clothes = pygame.image.load("doll/"+cList[i]).convert_alpha()

def enrolCard(name):
    print("正在录入", name, "请将卡片放在读卡器上")
    data1 = []; data2 = []
    for i in range(0,16): # 填充扇区对应的零
        data1.append(0); data2.append(0)
    for i in range(0,len(name)):
        data1[i] = ord(name[i])
    # 保存此项的位置
    data2[0] = xPlot >> 8
    data2[1] = xPlot & 0xFF
    data2[2] = yPlot >> 8
    data2[3] = yPlot & 0xFF

    # 这是身份验证的（默认）密钥
    key = [0xFF, 0xFF, 0xFF, 0xFF, 0xFF]
    rfReader.RC522_WriteSector(key,8,data1)
    rfReader.RC522_WriteSector(key,9,data2)
    print("编码完成")

def terminate(): # 关闭程序
    print("正在关闭")
    pygame.quit()
    os._exit(1)

def checkForEvent(): # 检查是否需要写入完成状态或录入
    global xPlot,yPlot,needsRedraw,enrol
    event = pygame.event.poll()
    if event.type == pygame.QUIT:
        terminate()
    if event.type == pygame.KEYDOWN :
        if event.key == pygame.K_ESCAPE :
            terminate()
        if event.key == pygame.K_SPACE :
            done = True
            enroll = False
        if event.key == pygame.K_e :
            done = True
            enrol = True
        if event.key == pygame.K_UP :
            yPlot -= 1
            needsRedraw = True
        if event.key == pygame.K_DOWN :
            yPlot += 1
            needsRedraw = True
        if event.key == pygame.K_RIGHT :
            xPlot += 1
            needsRedraw = True
        if event.key == pygame.K_LEFT :
            xPlot -= 1
            needsRedraw = True
```

- 主程序逻辑：
```python
if __name__ == '__main__':
    main()
```

你只需要进行一处修改：将窗口尺寸设置为你人偶图像的尺寸。双击人偶会弹出一个窗口，顶部栏会以像素为单位指定图像尺寸。确保这些数字用于设置代码中 `screenWidth` 和 `screenHeight` 变量的值。

运行代码时，你将看到人偶和第一件衣服。使用方向键将该衣服移动到你希望出现在人偶上的精确位置。将卡片放在读卡器上并按 E 键，将文件名存储在第 8 扇，位置存储在第 9 扇。取出卡片并按空格键处理下一件衣服。

> 继续按空格键循环切换服装，直到找到你想要录入的那件。这样一来，如果你发现某件衣服不太合适，可以再次录入该件。另外，如果你将文件添加到 doll 文件夹，只需在新的卡片上录入新衣服即可。

![](img/df9a01bf057d58c2401b5edabd6e8829_420_0.png)

最后，将每件衣服打印在纸上，并使用喷雾胶将其贴在每张卡片上。用透明塑料薄膜覆盖卡片，并用锋利的刀片修掉多余部分，将卡片正面朝放在切割垫上。我们的部分卡片如图 18–4 所示。

![](img/df9a01bf057d58c2401b5edabd6e8829_421_0.png)

图 18-4：
人偶衣服 RFID 卡片。

经 Imani Osman 许可复制

# 运行时间

现在是时候真的为人偶穿衣服了。实现此操作的程序位于列表 18–6。

列表 18-6：为人偶化妆
```python
#!/usr/bin/python3
# 由 Mike Cook 编写

from rc522rfid import rc522rfid
import pygame
import os

pygame.init() # 初始化图形界面

os.environ['SDL_VIDEO_WINDOW_POS'] = 'center'

pygame.display.set_caption("换装")
pygame.event.set_allowed([pygame.KEYDOWN,pygame.QUIT])
pygame.key.set_repeat(500, 80)

screenWidth = 240
screenHeight = 550
screen = pygame.display.set_mode([screenWidth, screenHeight], 0)
xPlot = [0]
yPlot = [0]
```
