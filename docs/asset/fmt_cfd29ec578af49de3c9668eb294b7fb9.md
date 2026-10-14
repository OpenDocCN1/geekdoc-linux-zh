
图 5.1a 所示为具有标准输出的简单反相器门。反相器有两个晶体管：`Tₖ` 连接在反相器的输出引脚和 +5 V 供电之间，以及 `T₁` 连接在输出引脚和地之间。当反相器的输入被拉到地时（图 5.1b），晶体管 `T₁` 被关断而 `T₁` 被导通。这意味着 `T₁` 像一个开关闭合而 `T₁` 像一个闭合开关。因此，现在输出引脚和 +5 V 供电之间存在低电阻路径。这将输出引脚拉高到 +5 V。当输入连接到 +5 V 时（图 5.1c），会发生相反的一系列动作：`Tₖ` 关断而 `T₁` 导通，从而在输出引脚和地之间形成低电阻路径。这将输出拉到地电位。

如果我们施加一个介于 +5 V 和地之间的电压到输入会怎样？在这种情况下，`T₁` 和 `T₁` 都可能导通并相互“对抗”。`T₁` 试图将输出拉到地，而 `T₁` 试图将输出拉到 +5 V。输出将稳定在 +5 V 和地之间的电压，并且大量电流将从 +5 V 供电通过 `Tₖ` 和 `T₁` 流向地。问题是，

#### 图 5.1 简单反相器的操作。

输入必须多接近地线或 +5 V 才能防止这种情况？答案取决于 `T1` 和 `T2` 的详细电气特性，但对于 TTL 来说，答案是有效的低逻辑电平是 0 V 到 0.8 V 之间的任意电压，有效的高逻辑电平是 2.0 V 到 5.0 V 之间的任意电压。对于 CMOS 逻辑，电压范围略有不同：分别为 0V–1.0V 和 3.5 V–5.0 V。

如果我们不将输入连接到任何东西会怎样？在这种情况下，电路的状态是不明确的。晶体管的输入未被驱动到任何稳定的电压，晶体管可能处于导通或关断状态。因此，输出电压可能在 +5 V 和地之间任意。为了防止未连接的输入导致逻辑电路进入不确定状态，一些 IC 在每个输入到 +5 V 电源之间都有上拉电阻（见图 6.2a）。当你将输入悬空时，上拉电阻 `RP` 将晶体管的输入拉到 +5 V。上拉电阻通常具有较大的电阻值

![](img/5124daf79d2807d81e49f49c22f1f8c1_153_0.png)
![](img/5124daf79d2807d81e49f49c22f1f8c1_153_1.png)
![](img/5124daf79d2807d81e49f49c22f1f8c1_153_2.png)

值（超过 10K），这样当你想将输入拉到地时，就不需要提供太多功率来完成。（你不会想使用低电阻上拉，因为将输入拉低会使大量电流从 +5 V 通过上拉电阻流向地。）

![](img/5124daf79d2807d81e49f49c22f1f8c1_154_0.png)
![](img/5124daf79d2807d81e49f49c22f1f8c1_154_1.png)

#### 图 5.2 FPLD I/O 选项。

输出电路也可以修改以具有不同的电气特性。标准输出，如我们所见，可以通过导通的晶体管的低电阻被拉到 +5 V 或地。然而，在某些情况下，你只希望输出被拉到地，而永远不拉到 +5 V。这样的开漏输出如图 5.2b 所示。当输入处于高逻辑电平时，输出通过晶体管 `T_l` 被拉到地。但当输入被拉到低逻辑电平时，输出不会被拉到 +5 V（像标准输出那样），因为 `T_h` 缺失。由于 `T_h` 缺失且 `T_l` 被关断，输出既不连接到 +5 V 也不连接到地，因此处于浮空状态。当然，在这种情况下，你可以从输出到 +5 V 连接一个外部电阻来将其拉高。

开漏输出的一种用途是结合上拉电阻执行线与操作（见图 5.3）。如果两个开漏输出直接连接在一起，结果将是如果任一输出为低，则输出电平为低。如果两个输出都处于浮空状态，则线与输出由上拉电阻拉到 +5 V。你不想尝试用具有标准输出的门来构建线与。那是因为一个门输出可能正试图通过其 `T_l` 将线与节点拉低，而另一个门试图通过其 `T_h` 将节点拉高。线与节点上的 resulting 电压是不确定的，大量电流流动，你可能会烧毁一个或两个门。

![](img/5124daf79d2807d81e49f49c22f1f8c1_155_0.png)

#### 图 5.3 使用开漏输出的线与。

另一种类型的输出是三态输出。三态输出可以驱动到 +5 V 或地，但也可以使其浮空。这与开漏输出不同，开漏输出只能驱动到地或浮空。三态输出的电路如图 5.4 所示。添加了两个新的 `Tₑ` 晶体管，它们由使能输入控制。当使能输入被拉到 +5 V 时，`Tₑ` 晶体管像闭合开关一样工作，门被使能（即输出可以被驱动到 +5 V 或地）。然而，当使能线被拉到地时，两个 `Tₑ` 晶体管都打开并完全将输出与 +5 V 电源和地断开。因此输出被禁用并处于浮空状态。这有什么用？多个三态输出可以连接到另一个门的同一输入，使能线可用于防止输出相互干扰。当一个输出驱动输入时，另一个输出被禁用因此浮空，无法干扰第一个输出。然后，通过禁用第一个输出并使能第二个，第二个输出可以在没有干扰的情况下传输信号。因此，通过智能控制输出的使能线，输入引脚可以从两个输出中的任一个接收信号。这一原理将在你创建多点总线时使用。例如，你 PC 中的内存总线允许微处理器从大量内存芯片中的任何一个接收信息。所有内存芯片输出都可以连接到同一总线，因为它们都有三态输出，只有在特定芯片应该传输某些 data to the microprocessor. They will not interfere with each other as long as only one output is enabled at a time.

![](img/5124daf79d2807d81e49f49c22f1f8c1_156_0.png)

#### Figure 5.4 Circuitry for a tristate output.

Where can all this get you in trouble? Obviously, if you use an open-drain output and do not provide a pull-up resistor, you cannot expect to drive the output to +5 V. Or if you use a tristate output and do not enable it, you won’t be able to drive the output to either +5 V or ground. But there can be, more subtle, problems. Suppose you have a single logic gate output that is driving a lot of inputs of other logic gates (see Figure 5.5). Further, suppose that these other inputs all have 10K pull-up resistors. Now, your output can be pulled to ground through `T_7`, but `T_7` has some finite resistance (i.e., it is not a perfect conductor). Suppose that the ON-resistance of `T_7` is about 100 Ω. The 100 Ω resistance will be trying to pull node `A` to ground while the pull-up resistors try to pull `A` to +5 V. Thus, a voltage divider is formed. The question is, How many inputs can be connected to the output before the combined pull-up resistors bring the voltage on node `A` above 0.8 V (the upper limit for a TTL low logic level)? The answer is given by solving

`0.8 V = 5.0 V × 100 Ω / (100 Ω + (10,000 Ω / N))`

and it turns out that `N = 19`. So you can drive 19 gate inputs from the single output. This is the maximum allowable fanout of your gate output. Trying to drive more gates could lead to problems caused by violating the limits on allowable logic levels. (Note that driving the inputs high is no problem because now the pull-up resistors help `T_A` pull the output to +5 V.)

![](img/5124daf79d2807d81e49f49c22f1f8c1_157_0.png)
