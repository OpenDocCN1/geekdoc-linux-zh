
```cpp
int leftReading = gIRSensors.frontLeft();

int rightReading = gIRSensors.frontRight();

int back = gIRSensors.rearLeft();
```

最后，代码确保传感器在沿墙运行时盯着墙，以确保它还在那里。

```cpp
case eRI_DrivingLookingForWall:

    // 是否看到了障碍物

    if (gMotor.isStopped()) {

        if (gMotor.isalled()) {

            enterUpState();

        }

    } else {

        // 检查找到了墙

        if (ultrasonic <= CLOSE_ULASONIC_RANGE

            || leftReading >= CLOSE_WALL_VALUE

            || rightReading >= CLOSE_WALL_VALUE) {

            enterLeftState();

        }

    }

    break;
```

## Rover 5 完美应对任何课程

```cpp
void enteringWallOnState() {

    // 将超声波传感器指向右侧

    panAngle = LOOK_RIGHT_PAN_ANGLE;

    giltAngle = RIGHT_TILT_ANGLE;

    gpanServo.write(gpanAngle);

    giltServo.write(giltAngle);

    Motor.clear();

    grightMotor.clear();

    Motor.setTargetRPM(BASE_WALL_FOLLOWING_RPM);

    grightMotor.setTargetRPM(BASE_WALL_FOLLOWING_RPM);

    gStateStartEncoderTicks = gMotor.getMeasuredEncoderTicks();

    gRobotState = eRS_LookingWallOn();

}
```

上方主板连接到机器人后部，易于访问更多组件。

## Pi2Go Lite

作为我们测试过的最小的机器人之一，你可以说`Pi2Go`有些过人之处。

`Pi2Go Lite`是一个非常有趣的设备。它被装在一个微小的盒子里，没有使用底盘，而是采用了`PCB`结构，这使得它是一个非常简单的机器人，可以执行命令而不会真正接触复杂的环境。它听起来像是一个遥控机器人，但可能比牙玩具要好得多。

由于`Pi2Go`可能是本期功能最丰富的机器人，但所有这些功能都是代价的；它是一个在组装前需要一些焊接和准备工作的机器人。虽然需要进行一些焊接，但不需要剥去任何电线之类的。大约有 50 个组件需要安装，可能更多，而且可能有点棘手。说明并不特别有用，但组件实际上列在`PCB`上，作为放置物品位置的大致指南。

一旦你需要将这少数几个部件组合在一起完成它。网站列出的组装时间为 90 分钟，但我们发现要长得多——比其他更大或更复杂的机器人都要长。

它是一个紧凑的小家伙，通过自定义`Python`库由树莓派供电。传感、驱动电机和其他功能都有其相应的`Python`函数。它让你能够创建脚本使其完全自主运行，只要这种自主只需要达到距离和接近传感以进行操作，如果设置正确，它就可以从树莓派获取额外的时间或网络信息。

考虑到价格、功能和相对容易的编程性，它是一个极佳的设备，非常适合入门机器人和敏捷性开发。需要一些焊接技巧。

## 技术规格

| 特性 | 细节 |
| :--- | :--- |
| 制造商 | 4tronix |
| 高度 | 90 mm |
| 宽度和深度 | 130 x 145 mm |
| 重量 | 0.40 kg |
| 电源 | 9V AA 电池 |
| 控制板 | 树莓派 (`Raspberry Pi`) |
| 运动方式 | 两轮驱动 |
| 传感器 | 超声波传感器、两个巡迹传感器和两个障碍传感器 |
| 网站 | `www.pi2go.co.uk` |

![](img/7b0011b9ca05b82c33c02a484fd02e99_55_0.png)

## 评分

- 组装 3/5
- 质量 3/5
- 可编程性 4/5
- 功能性 5/5

![](img/7b0011b9ca05b82c33c02a484fd02e99_55_1.png)

56 `www.linuxuser.co.uk`

## 树莓派机器人

### 挑战 2：巡迹

沿着黑色的线条移动，尽管你可能在终点找不到一个魔法师。

巡迹非常简单；你在地板上画一条线，让机器人跟随它。这包括转弯，准确遵循路线到达目的地或累积圈数。`Pi2Go Lite`是我们本月看到的唯一带有巡迹传感器的机器人，尽管它有很多功能。然而，来源显示`Python`脚本中没有巡迹功能，因此我们需要编写一个脚本。

正如我们引导的，解决方案涉及巡迹传感器——这些是位于万脚轮`PCB`底方的红外传感器。我们还将让`Pi2Go`在走廊上运行并直奔终点。

我们将面临的一个问题是电机的运行速度可能不同——通过几次尝试，你可能在第一个前进命令中修复此问题，在50 的速度下我们全速前进。你可以根据需要将其调整得更慢或更快。

循环非常简单：它检查巡迹传感器是否被激活，通过转动轮子，我们需要为每个`True`语句在特定方向修正路线。你可以在`turnforward()`函数中单独设置左、右电机的速度，然后在返回循环之前设置一个停顿。

代码在你停止时结束，并在退出前清理`GPIO`端口设置。代码需要`pi2go` Python 文件，你可以在这里获取：`http://tronix.co.uk/blog/?p=475`

![](img/7b0011b9ca05b82c33c02a484fd02e99_56_0.png)

![](img/7b0011b9ca05b82c33c02a484fd02e99_56_1.png)

## 代码列表

```python
import time, pi2go
pi2go.init()
pi2go.forward(50)
```

```python
try:

    while True:

        if pi2go.leftleft == True:

            pi2go.turnforward(0, 50)

            time.sleep(2)

            pi2go.forward(50)

        elif pi2go.rightRight == True:

            pi2go.turnforward(50, 45)

            time.sleep(2)

            pi2go.forward(50)

        else:

            time.sleep(0.5)

except KeyboardInterrupt:

    print("Stopped")

finally:

    pi2go.cleanup()
```
