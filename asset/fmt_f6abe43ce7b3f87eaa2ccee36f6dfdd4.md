
尝试一下这个。（它在 `pw-chapter6` 目录下，文件名为 `pw-firsttry.tcl`；你需要将其重命名或复制为 `pw.tcl`，游戏才能找到它。）正如你从名字猜的那样，这并不是我们想要的。是的，电脑船只确实会围着着玩家转，而且有了武器它可能会很快获胜。问题是这个脚本太优秀了——它没有给玩家公平的机会。电脑船只基本上是无法避开的。一旦它成功到达玩家身后，就很难摆脱它。这会让游戏变得非常无聊（除了武器不起作用之外）。

所以我们需要让电脑在游戏中表现得笨一点。脑海中浮现了一些想法。我们可以限制它的速度或转弯率，但那样太作弊了（而且可能很容易被察觉）。更好的做法是……

## 与状态无关的代码

### 找出朝向目标最快的方法。

```tcl
set target_angle [getAngleTarget]

set arc [expr $target_angle - $computer_angle]

if {$arc < 0} {

    set arc [expr ${arc + 360}]

}
```

```tcl
if {$arc < 180} {

    set computer_angle [expr ${computer_angle + 3}]

} else {

    set computer_angle [expr ${computer_angle - 3}]

}
```

```tcl
# 返回目标坐标与对手之间的
# 距离（像素像素）。

proc getDistanceToTarget { {

    global computer_x computer_y target_x target_y

    set xdiff [expr ${computer_x} - $target_x]

    set ydiff [expr ${computer_y} - $target_y]

    return [expr $sqrt($xdiff * $xdiff + $ydiff * $ydiff)]

}
```

```tcl
# 返回指向目标坐标的
# 角度（度）。使用基础三角函数（反正切）。

proc getAngleToTarget { {

    global computer_x computer_y target_x target_y

    set x [expr ${target_x} - $computer_x]

    set y [expr ${target_y} - $computer_y]

    set theta [expr {atan2(-$y,$x)}]

    if {$theta < 0} {

        set theta [expr {2*3.141592654 + $theta}]

    }

    return [expr {$theta * 180/3.141592654}]

}
```
