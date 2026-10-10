
```python
import numpy as np
import cv2
cap = cv2.VideoCapture('test.avi')
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE,(3,3))
fbg = cv2.createBackgroundSubtractorMOG2()
while(1):
    ret, frame = cap.read()
    fgmask = fbg.apply(frame)
    fgmask = cv2.morphologyEx(fgmask, cv2.MORPH_OPEN, kernel)
```

# 树莓派嵌入式系统设计 409

```python
# 在帧上绘制文字和时间
cv2.putText(frame, "Room Status: {}".format(text, "(de Oliveira et al.)"), (10, 20),
cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255), 2)
cv2.putText(frame, datetime.now().strftime("%A %b %Y %H:%M:%S%p"),
(10, frame.shape[0]-10), cv2.FONT_HERSHEY_SIMPLEX, 0.35, (0, 0, 255),
1)

# 如果用户按下键，则显示并记录
cv2.imshow("Security Feed", frame)
cv2.imshow("Thresh", thresh)
cv2.imshow("Frame Delta", frameDelta)
key = cv2.waitKey(1) & 0xFF

# 如果按下 'q' 键，跳出循环
if key == ord("q"):
    break

# 清理摄像头并关闭所有打开的窗口
cv2.release()
cv2.destroyAllWindows()
```

其余的代码只是组合了所有之前的命令。我们在左上角绘制了房间状态，随后在左下角绘制了时间戳（类似于“真实的”监控录像）。使用了一种称为 `LPs` 的纹理描述符。与通过纹理全局表示（即灰度级共生矩阵）计算的纹理特征不同，`LBP` 将计算纹理的局部表示。这种局部表示是通过比较每个像素与其相邻的像素来构建 `head` 的。构建 `LBP` 纹理描述符的第一步是将图像转换为灰度图。对于灰度图像中的每个像素，我们选择环绕中心像素的大小为 `$r$` 的邻域。计算该中心像素的 `LBP` 值并将其存储在与输入图像宽高相同的输出 2D 数组中。`LBP` 实现的一个主要优势是我们可以捕捉到图像中极其细微的细节。然而，捕捉小尺度细节的能力是该算法的缺点之一。例如，我们无法捕捉不同尺度的细节，只能捕捉固定的 3x3 尺度。`LBP` 中均匀原型的数量完全取决于标记为 `$p$` 的点数。随着 `$p$` 值的增加，直方图的维度也会增加。然而，对于 `LBP` 中给定数量的点，有 `$p+1$` 种均匀模式。直方图的最终维度是 `$p+2$`，其中新增的条目汇总了所有非均匀模式。这些均匀 `LBP` 模式非常重要，因为它们将增加额外的旋转不变性和灰度不不变性。因此，在从图像中提取 `LBP` 特征向量时经常使用它们。

# 410 不确定环境下的嵌入式机电系统设计

```python
# 导入必要的包
from skimage import feature
import numpy as np

class LocalBinaryPatterns:
    def __init__(self, numPoints, radius):
        # 存储点数和半径
        self.numPoints = numPoints
        self.radius = radius

    def desc(self, image, eps=1e-7):
        # 计算图像的局部二值模式表示
        # 然后使用 LBP 表示
        # 构建模式的直方图
        lbp = feature.local_binary_pattern(image, self.numPoints,
            self.radius="uniform")
        (hist, _) = np.histogram(lbp.ravel(),
            bins=np.arange(0, self.numPoints + 3),
            range=(-0, self.numPoints + 2))

        # 归一化直方图
        hist = hist.astype("float")
        hist /= (hist.sum() + eps)

        # 返回局部二值模式的直方图
        return hist
```

`LocalBinaryPatterns` 类定义了 `LBP` 的构造函数，并接收所需的参数环绕中心像素的模式半径以及沿外半径的点数。`local_binary_patterns` 函数返回的 `LBP` 变量不能直接作为与输入图像宽高相同的数组使用。每个 `LBP` 值的范围从 `[0, numPoints + 2]` 到每个可能的 `numPoints + 1` 种旋转不变原型的对应值。因此，为了构建实际的特征向量，我们需要调用 `np.histogram`，由它来统计每个 `LBP` 原型出现的次数。返回的直方图是 `numPoints + 2` 维的，每个原型都有一个整数计数。然后我们对该直方图进行归一化，使其在返回给调用函数之前值为 1。

```python
# 构建参数解析器并解析参数
ap = argparse.ArgumentParser()
ap.add_argument("-a"
```

# 树莓派嵌入式系统设计 411

使用两个开关来解析我们的命令行参数。以下代码段用于从训练图像中提取 `LBP` 特征。

```python
# 遍历图像
for imagePath in path.list(args["training"]):
    # 加载图像，转换为灰度图并进行描述
    image = cv.imread(imagePath)
    gray = cv.cvtColor(image,cv.COLOR_BGR2)
    hist = desc(gray)

    # 从路径中提取标签，更新标签
    # 和数据列表
    labels.append(imagePath.split("/")[-2])
    data.append(hist)

# 在数据上训练线性 SVM
model = LinearSVC(C=100.0, random_state=42)
model.fit(data, labels)

# 遍历测试图像
for imagePath in path.list(args["testing"]):
    # 加载图像，转换为灰度图，进行描述
    # 并进行分类
    image = cv.imread(imagePath)
    gray = cv.cvtColor(image,cv.COLOR_BGR2GRAY)
    hist = desc(gray)
    prediction = model.predict(hist)[0]
    # 显示图像和预测结果
    cv2.putText(image, prediction, (10, 30), cv2.FONT_HERSHEY_SIMPLEX)
    cv2.imshow("Image", image)
    cv2.waitKey(0)
```

最后，我们计算直方图。`Haar` 特征（如 7.1 节所示）是在相邻亮暗矩形的两个维度上定义的。用于识别的典型特征用于实时人脸检测。这是一种基于机器学习的方法，级联函数通过许多正样本和负样本训练而成。一组不同尺度的 `Haar` 特征也可以积分图技术高效地计算。每个像素被分配其上方和左侧像素之和。如果差异超过阈值，则确定了某些 `Haar` 特征的存在。为了训练我们的分类器，我们需要显示要检测对象的图像样本（正样本）以及更多不包含该对象的图像（负样本）。

# 412 不确定环境下的嵌入式机电系统设计

表 7.10 人脸检测方法的比较

| 方法 | 准确率 | 计算时间 | 备注 |
|---|---|---|---|
| 局部二值模式 | 中到高 | 高 | 检测极细微信息的准确率较高，但受噪声问题影响。因此，其计算需求也。 |
| Haar 级联 | 高 | 中 | 在中等计算需求下，人脸检测具有高准确性。 |

# 树莓派嵌入式系统设计 413

参数如下：

- `Image`: 类型 `CV_8U` 的矩阵，包含一张检测到对象的图像。
- `scaleFactor`: 图像尺寸在每个尺度上缩小了多少？该缩放因子用于创建尺度金字塔。缩放因子为 1.03 时，意味着使用较小的步长进行缩放，尺寸缩小了 3%。
- `minNeighbors`: 每个候选矩形需要多少个邻居才能保留？此参数将影响检测到的人脸的质量。值越高，检测到的数量越少，但质量越高。
