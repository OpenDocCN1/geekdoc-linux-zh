
进入`/path/to/xxx`目录，找到`xxx.json`。

在线算法在搜索过程中的行为尚不为人所知。信息几何将搜索描述为受约束分离的黎曼流形的一个示例。大量的子空间收敛于所有梯度。在线算法可以克服由随机样本选择过程引入的噪声。统计学方法为这些主题带来了新的见解。这些结果可能比在线算法更有效地预测方差。

- Dennis, J., and Schnabel, R. B., 1983, Numerical Methods for Unconstrained Optimization and Neural Networks, Edgecliffe NJ: Prentice Hall;
- Fisher, I., and Amari, S., 2000, Local minima and plateaus in structural characteristics of multic multilayer networks, Nature, 406:317–320;
- Le, C., Younun, H. G., and Hinton, K. R., 1998, Efficient backpropagation for Neural Networks, Tutorial Notes in Springer Science 152, New York: Springer-Verlag;

# 人工网络中的映射学习

相关阅读：神经形态与信息几何：感知、指控与反向传播：在线学习与泛化的随机方法

## 参考文献

Amari, S., 1967, The theory of adaptive pattern classifiers, IEEE Trans. Electr. Comput., 16:269–307.
- Benistev, A., Mitev, M., and Prince, P., 1990, Adaptive Algorithms and Stochastic Approximations, Berlin and New York: Springer-Verlag;
- Bottou, L., 1998, Online algorithms and stochastic approximations, in Online Learning and Neural Networks (D. Saad, Ed.), Cambridge, Engl.: Cambridge University Press, pp. 9–12.
- Ljung, J., and Sederberg, L., 1993, Theory and Practice of Recursive Identification: The Least Squares Neural Network Approach, Cambridge, MA: MIT Press.
- Murata, N., 1998, a statistical study of on-line learning, in Online and Neural Networks (D. Saad, Ed.), Cambridge, Engl.: Cambridge University Press, pp. 175–180.
- Radrad, J., and Amari, S., 1999, Analysis of neural network learning by stochastic gradient descent: Neural Networks, 12:527–534.
- Rumelhart, D. E., Hinton, G., and Williams, R., 1986, Learning algorithms by error propagation, in Distributed Backpropagation Problems in the Exploration of Complexity, vol. 1, Cambridge, MA: MIT Press, pp. 38–52.
- Typkin, J., 1971, Adaptive Learning and Learning in Artificial Systems, New York: Academic Press.

# 随机共振

# Frank Moss

# 引言

# 随机共振的定义

随机共振（SR）本质上是非线性现象，在弱信号中加入随机过程可以增强其被系统检测到的概率。通过系统的信息传输也得到了增强。最佳的噪声强度会导致最大检测效果。当噪声阈值小于或大于该值时，信息将会降低。这种现象如图 1 所示，其中信号被视为一个“黑箱”。

范式。虽然类似于神经输入的标记脉冲似乎是随机被检测到的，但它们携带了关于亚阈下信号的信息。这是因为在信号所在的位置，跨越阈值的概率要大得多；放电的“平均速率”取决于组件值距离阈值有多近。噪声充当信号的采样函数，每个脉冲仅携带跨阈值的时间。信号幅度被编码在阈值跨越的平均速率中。

仅测量了三个指标。图 1 画了我们黑箱的动作。阈值由虚线和粗线表示。相对于亚阈下信号平均值的噪声幅度指定为 `$A_n$`。叠加在信号加噪声之和上的（噪声）分布通过标准形状（带噪声）脉冲的时间来标记。噪声可以是外部的，例如环境噪声（包括热涨落），也可以是内部的，即感官神经元或区域内动态过程产生的确定性噪声。

当信号不存在时，阈值是必要的。只有在特定类的非线性系统中才会发生随机共振。阈值和噪声在人工和自然系统中无处不在；在 SR 中，它存在于各个领域。但在这里我们关注出现在几种生物环境中的 SR（Moss and Wiesenfeld, 1995）：小龙的机械感受系统，

我们可以看到，正是噪声导致阈值增强了输出标记脉冲。在没有噪声的情况下，就不会产生跨越越，因此没有输出。正是噪声使得亚阈下信号在……中可检测

# 阈值跨越脉冲

![](img/5cb7d541b875c6d6c2092ad1a376440a_1131_0.png)

脉冲串的功率谱

![](img/5cb7d541b875c6d6c2092ad1a376440a_1131_1.png)

SNR 与噪声方差

![](img/5cb7d541b875c6d6c2092ad1a376440a_1131_2.png)

**图 1.** 随机共振（SR）所需的三个要素：一个阈值（虚线）、一个亚阈下信号（实线正弦线）和一个噪声（不规则线）。组合（正弦波+噪声）标准响应的跨越由上面的脉冲串所示。脉冲串的功率谱显示了亚阈下信号的证据，其在 `$f_0$` 和 `$f_2$` 处的尖峰，在宽带噪声背景（水平线）上。C. SNR 与噪声标准差的比值。图 1 显示了添加到亚阈下信号的噪声在最佳强度处是 SR 的特征。为了简单起见，我们考虑一个包含输入和输出的黑箱。如果在输入信号（足够幅度）的影响下跨越阈值，神经元“放电”或产生足够幅度的动作电位。这似乎有些抽象，但它是解释神经元产生动作电位的最早模型。如果强度太大，样本就会随机化，信息会被大噪声丢失。在最佳噪声强度下，信息达到最大值。通信工程师计算的一个测量是信噪比（SNR），基于功率谱。功率谱显示了包含每个频带内的功率。图 1 所示的脉冲串。我们看到尖峰（领先功率）和其二谐波。信号特征显示在 `$f_0 = 1\text{ Hz}$` 处的尖脉冲，其在 `$2f_0 = 2\text{ Hz}$` 处的二谐波也可见，类似于提到的阈值情况，图 2B 显示，尽管通过阵列的信号转换幅度作为层噪声电压的函数在约 `$10\text{ mV}$` 的最佳电压达到最大值。SNR 并不小；尽管如此，这个实验是首次在分子水平证明 SR 的。

# 随机共振的特征

随机共振的特征是图 1 中脉冲串包含的信息在最佳噪声值处达到最大值。将噪声视为采样过程，可以看到如果强度太小，信号就会欠采样，感官生物学家熟悉时间间隔的概率分布。一个被称为“跳跃（skipping）”的相关主题发生在一个或几个脉冲在信号极大值附近产生，每个脉冲之间的时间接近信号的周期 `$T$`。跳跃由 `$2T$`、 `$3T$` 等时间间隔表示。因此，我们预计在脉冲间隔的概率分布中看到一系列极大值；事实上，在感官神经元中观察到了这种具有衰减峰值的多态分布，这是我们三个实验的结果（Longley, Moss, 1991）。跳跃与 SR 的关系在于，在最佳噪声强度下存在多态分布。

![](img/5cb7d541b875c6d6c2092ad1a376440a_1132_0.png)

# 细胞离子通道中的随机共振

我们对生物 SR 发展的概述来自于对最小可能——单个分子的分析，并随着尺寸和复杂性扩展到整个动物和人类心理。几年前，Bezukov 和 Voyanov (1995) 发表了一项卓越实验的结果。他们测量了通过嵌入脂质双层的每个单个分子电压依赖通道阵列的电流。单个离子通道允许离子流以开放或关闭通道。开放概率由跨膜电位决定。亚阈下信号本质上是离子通道作为跨膜电位函数的平均开放概率的测量。关键是用弱信号调制二进制噪声：一个 `$1\text{ Hz}$` 的亚阈下周期脉冲，正如图 1A 所示。通过阵列的电流虽然有噪声，但带有关于弱信号的信息。图 2A 是通过阵列传输的电流的功率谱。信号特征显示在 `$f_0 = 1\text{ Hz}$` 处的尖峰，其在 `$2f_0 = 2\text{ Hz}$` 处的二谐波也可见，类似于提到的阈值情况，图 2B 显示，尽管通过阵列的信号转换幅度作为层噪声电压（圆）的函数在约 `$10\text{ mV}$` 的最佳电压达到最大值。SNR 并不小；尽管如此，这个实验是首次在分子水平证明 SR 的。![](img/5cb7d541b875c6d6c2092ad1a376440a_1132_1.png)

# 感官生物学中的随机共振

# 螃感受器

在生物学中，随机共振最早是在小龙的感受系统中观察到的（Douglas et al., 1993）。该系统适用于探测捕食者。小龙上对流体力学敏感的毛可以感知微弱的周期性水运动（8 到 12 `$\text{Hz}$`），这种运动由初级感官神经元感知，并汇聚到神经节（侧节或尾节）以检测接近尾部的捕食者。例如，某人和同事在接收带有单个毛的单个感官神经元的脉冲串的同时，对尾部施加机械刺激。选择传入纤维具有低输入强度，以提供单一噪声源的清晰实验。从传入纤维中汇的功率谱揭示了三个实验的特征——一个尖锐信号和一个幅度较小的二谐波在宽带噪声背景上。SNRs com- 图 2. A：从小龙通过带噪声传输的离子通道获得的功率谱。注意尖峰，这是双层膜诱发的亚阈下周期信号的证据。B：幅度和信噪比作为输入电压的函数。插图显示了由阈下噪声驱动的峰值前后噪声的变化（数据在约 `$10\text{ mV}$` 的最佳电压处显示极大值）。虚线和点线是用不同噪声水平测量的 SNR 曲线。S, M. and Voyanov, 1995. 噪声诱导的跨电压依赖离子通道信号转导证据，Nature, 378, 362–364.

## 随机共振

## 心理物理学与动物行为中的随机共振

### 心理物理学中的 SR

随机共振已进入人类心理物理学领域。在刺激中加入随机过程是否能增强人类准确感知刺激的能力？Neimovich (1998) 对心理物理学实验的方案控制、统计准确性和理论解释进行了研究。一项使用神经网络模拟人类大脑内部噪声的实验考虑了这一点。该模型考虑了具有极值的能量势（即稳定状态），这些极值代表感知（Fiani and Shimamoto, 1994）。人类对立方体的视角随机切换，这些实验提供了大脑内噪声的首次定量测量。

但噪声作为外部刺激能增强感知吗？对于人类听觉，两个实验小组已经解决了这个问题并给出了肯定的回答（Ward 2000; 等）。这种效应很小（仅约 3 dB），而且这些实验是在增加耳朵极高敏感性的基础上进行的。正在这里，两个实验小组获得了具有统计学意义的结果。在他们的实验中，Zerg 和同事向周期性刺激添加了听觉噪声。通过对两个不同频率的周期性刺激产生的拍频音使用高压力感受器，并再次添加了噪声。

一项方案还证明了使用噪声提供视觉刺激（Wad 等, 2011）。在这项实验中，视觉噪声呈现在一个计算机生成的系统中，发现快速显示器可以增强受试者的感知能力。

但在此之前，SR 已经在人类听觉中得到证实（Collins, Heinrich, and King, 1996）。一项实验证明了语音感知中的“随机共振”现象。在单独的实验中，分别向刺激添加了机械噪声和电噪声，产生了积极结果。

最近的研究还显示了 SR 对人类认知能力具有非常有前景且具有启发性的影响。他们发现，添加听觉噪声可以增强多项算术检索任务的记忆。实验

复杂度提升一个水平——使用不同的动物：该实验特别有趣，因为小虾和节肢动物对捕食者具有非常相似的机械感受器。然而，小虾是一种具有暴露在空气和水波中的毛发的动物。包裹的形式导致了游泳身体对刺激的扰动行为，但对于近周期性刺激，毛发的敏感度（122 到 150 dB）高于小虾。实验对肢体使用了电随机噪声，在神经节内产生了脉冲序列。为了改进其他方法，他们使用计算机测量了刺激电流与神经脉冲之间的相关性，而不是脉冲序列的信噪比（SNR）。测量清楚地证明了小虾感觉系统神经节水平存在 SR，如图 3 中的数据所示。

在另一项实验中，人类触觉系统显示出“功能性”（Hironoka, Nozaki, and Yamamoto, 2016）。这种方法使用了心脏和血压调节机制的耦合。将周期性信号应用于血压，将噪声应用于机械感受器。在心脏中观察到了 SR，这反过来可能作为一种超过异常刺激的机制。

最后，人们注意到，在与心理物理学实验并行的，动物实验（使用电感受鱼）也证明了 SR 作为一种行为感知的存在（Russell, Williams, and Moss, 1999）。

## 讨论

随机共振已经在生物学的多个水平得到了证实：从离子细胞到细胞膜，再到动物和人类的认知、感知，最终到行为。行为效应很小，因为 SR 发生在人类和动物感知阈值的边缘。随着时间的推移，进化系统可能通过选择优势理解了它的益处。因此，我们可以在广泛的生物中看到它的影响。这种波动是激发性的，无疑将导致进一步的研究。

Hidaka, H., Nozaki, D., and Yamamoto, Y.. 2000. 人类大脑中的功能性随机共振：对亚反射性刺激的无噪声增强检测。Phys. Rev. Lett., 85:3728–3731.

Longtin, A., and Miller, F. G.. 1996. 随机共振在皮层感觉系统中的广泛神经编码。Nature, 380:165–168.

地图导读：动态系统

相关阅读：应用、衰减与整合；生物系统中的链；神经系统中的链；协作操作者的集体行为；协作现象

## 参考文献

Anchevsko, V. M., Finn, A., and Schimansky-Gierke, L.. 1997. 随机共振：效应下的噪声指数。Phys. Rev. Uac, 156:3769–3772.

Bezzik, S. M., and Vadovsky, I.. 2005. 噪声诱导增强离子通道随机信号转导电压依赖性。Nature, 378:362–364.

Collins, L. F., Titt, T. T., and Gray, P.. 1996. 噪声增强的触觉感觉系统。Nature, 383:770–775.

Douglas, J. K., Puntello, E., and Moss, F., 1993. 随机共振对机械感受器功能的噪声增强。Nature, 365:367–370.

Fukuda, A., and Moss, F., 1991. 双稳系统中的时间序列和感觉神经元通过噪声诱导的信息传输。Neuron, 29(4-5):1033–1040.

Gier, L., and German, D., 1994. 随机共振：时间与空间先天性。Int. J. Biophys., 64:1383–1393.

Moss, F., and Winfield, K., 1995. 噪声的益处。Nature, 376:764–769.

Nozaki, K., 1993. 整合、感知与理论，9(2):225–230.

Rian, M., and Semimoto, E., 1994. 模糊图像的解释。Phys. Rev. E, 50(3):2443.

Russel, D., Wilkins, L., and Moss, F., 1999. 随机共振用于感觉。402:219–223.

Yang, F.-P., Q.-J., and Morse, R., 2000. 噪声增强的听觉。Brain Res., 861:251–255.

## 结构化连接主义模型

Lokendra Shastri

## 引言

连接主义的研究源于这样一个观点：理解大脑的计算特性对于理解人类认知至关重要，并且从计算、人工智能（AI）、心理学和学习等领域获得的见解对于基础研究是有用的。

## 认知模型的神经约束

人类大脑拥有超过 `10^9` 个元素和 `10^15` 个连接，其编码、通信和处理信息的容量是巨大的。即使大脑是

尽管极其强大，它也有局限性。神经元是计算缓慢的设备，尽管神经元对输入的时空整合是复杂的，但它们不太可能编码和解码仅包含几个比特信息的“消息”。因此，预计神经元将用于编码复杂的动力学机制。

互连允许了自下而上的感知处理受到自上而下的预期引导。该模型可以解释许多关于网络中优于孤立层级的单词和电话号码偏好的心理学发现。

合理系统的一个特定局限性是，它们难以以动态方式表示计算结构。“John 给 Mary 读了一书”这一事件的表示不能仅通过在给定时间步上动态地激活相关节点来实现。这种表示对于“John 给 Mary 读了一书”来说是不够的。这种表示事件角色之间关系（例如……以及以及随事件发生的细节（例如……）之间关系的方式是不合理的。使用“绑定节点”（一个可以进行绑定的节点）来表示长期绑定是容易的，而在语言理解和视觉处理过程中，使用无法表示绑定的绑定节点是不可能的。基于诺依曼架构的绑定技术无法使用，因为其输出的存储容量和分辨率不足以存储和通信名称和指针。

早期结构化连接模型的其他例子是 Cottrell 和 Small (1983) 以及 Deutsch 和 Pollock (1986) 开发的意义模型。大多数模型都有缺陷，无法表示显性的语义信息来解释它们的含义。这些模型展示了这种动态绑定是如何发生的。Cottrell 和 Small (1983) 使用了一个三层网络模型，由感官层、概念层和输出层组成，并具有相互抑制的链接。

另一个早期结构化连接模型的例子是语义网络（CSN）。CNS 将语义记忆（SEMANTICS）中组织在“是”层次级（IS-hierarchy，例如“鸟是动物”）中的概念视为属性的集合。每个属性-值对都有一个分布，例如红色、绿色和黄色。CNS 可以为给概念找到某个属性最可能的值。例如，对于一个概念的描述，CNS 可以找到与描述最匹配的项。CNS 通过聚合可用信息并使用重叠最大值来寻找答案。然而，部分重叠可能会使其难以形成稳定的状态。

## 时间上的可扩展性

我们可以在 100 毫秒内识别常见物品，并以每分钟数百词的速度理解语言，尽管这涉及对语义、语法和语用知识的处理和整合。这表明大脑可以在几毫秒内完成广泛的复杂的语言和推理任务。这是一种我们可以为概念而设计的强大构架（Feldman and Ballard, 1982; Shastri and Ajagkar, 1993）。

这些模型的局限性并不高，考虑到必须考虑的属性。单元的表示输出、输入的“大小”由系统通过位映射进行处理，其中输出相对于输入数量是二次的（或更高），这是非神经的。对于常识推理或对于大型知识库，可以提出理由：

## 结构化连接模型示例

### 早期工作

早期的结构化连接模型使用了 McClelland 和 Rumelhart (1981) 提出的激活表示模型。该模型由三层组成：表示特征、字母和单词。神经元通过兴奋性和抑制性权重连接起来。例如，每个输入中代表字母的所有节点中都有一个节点。在特征层中，一个字母通过兴奋性连接到单词层中的节点。同样，单词层中的节点通过兴奋性连接到特征层中代表该位置字母的节点。此外，从单词层到字母层还存在互惠连接。

### 绑定问题的解决方案

上述结构化连接模型的一个关键局限性是它们无法表达动力学。例如，McClelland 和 Rumelhart 无法动态地将字母绑定到单词中的位置，以便表示长度为 n 的单词的特征。这些结构化连接模型在解决绑定问题方面取得了进展。这些模型（见 Barden and London, Pollock, 1991）、SHUTI（Shastri and Ajagkar, 1993）、CONSERDYN（ROBIN and Robyn, and Lisa and Holyaak, 1997）。

概念表示中可能的同步已被几位研究人员研究过（见 DYNAMIC ARCHITECTURE; SYNCHRONIZATION, BINDING AND EXPERIENCE; SPINNING NEURONS, COMPUTATION WITH），SHUTI 是第一个提供计算解释的模型，解释了此类活动如何解决高层概念知识的表示和处理中的问题并提供支持。

SHUTI 编码了大量的语义和规范知识，但在几百毫秒内就能执行对既有事实集的引用（Shastri and Ajayanagade, 1993）。给定故事“John 在走廊里摔倒了。关于他是如何指代走廊的，SHUTI 可以回想起他进入了那里，并且 John 摔倒是因为他在瓷砖上滑倒了。”

SHUTI 使用由特征组成的神经网络编码关系知识（例如框架和动作）。P 和 O +role 之间关系的学习表明，该项是一个由 P 的某个方面锚定的动作，+role 表明系统对该方面的信息具有选择性，对于与 P 关联的每个角色都有一个。实体与正在形成的角色之间的动态绑定是由实体和实体角色的同步触发的。

例如，知识“John 摔倒受伤了”被编码为 fell+hurt 的激活模式，以及 fell-hallway 和 hurt-location 之间的双向链接。根据上述内容，激活显示角色-hurt 与父级 John 同步开始，角色-location 也同步开始。

SHUTI 通过集群之间的链接来增强关系。正如这个示例所示，动态绑定源于跨集群的活动传播。事实上，SHUTI 结合预测信息并实例化新的实体（如果 John 摔倒了，由于 John 摔倒了，必须在走廊，链接到 man）。这些特征使得 SHUTI 允许在几毫秒内得出广泛的推理。所需的时间与链的长度成正比。

SHUTI 提供了一种动态绑定的通用策略，允许大量实体同时出现，只要作为角色的实体保持较少。这受到生物学限制的促进；参与动态绑定的每个实体占据一个空间，动态框架中发生的角色数量是有限的。在这里，SHUTI 使用感觉细胞的连续触发（作为绑定，允许同步-2 ms）。

## 结构化网络中的学习

Regier (1996) 的空间学习模型提供了连接模型中学习的例子。观察模型涉及相对于彼此的两个维度，其中去语境化的表示标签（单词）和它描述的事件。

除了通过反复接触数据进行增量学习外，连接模型还使用了强化学习（Rosenhold, 1998; Shastri, 1998; Shastri, 2001b）。提取可以描述如下：在特定结构内的学习允许网络通过与其他节点或半角色（即尚未激活为“自由”的节点）强连接来学习特定的“意义”（或功能）。框架节点通过链接连接自由节点网络。自由节点可能被新项激活。Shastri (2001a) 显示学习加强了这些节点 x 和 y 之间链接的权重，这可以通过长程增强（LTP）现象产生。

在 SHUTRI 中，神经系统中的记忆通过海马-皮层相互作用来调控（Shastri, 2000a, 2001b）。我们系统中的情节记忆与各种感觉和声明性数据的去语境化表示有关，这种表示是由海马状态、内嗅皮层、齿回和下托复合体塑造的。

多个模型被提出解释海马如何存储情节记忆，但事件记忆的一些关键问题仍未解决。大多数现有模型将记忆中的项作为特征或特征的组合。每个记忆轨迹可以通过激活作为绑定的集合来形成。

# 支持向量机

路线图：人工智能
背景：人工智能与神经网络
相关阅读：认知建模：心理学与连接主义；
连接主义与符号表示；链路架构

## 参考文献

- Barden, J., and Pollack, L., Eds., 1991, Advances in Connectionism and Neural Computation Theory, vol. 1, New York, NJ: Academic.
- Cort, G. W., and Smith, S. L., 1983, a connectionist scheme for word sense disambiguation, Cogn. Brain, 7:689–720.
- Feldman, J., et al., 1990, Connectionist models in neural networks, Cogn. Biol., 4:967–1042.
- Feldman, J., and Barden, H., 1992, Layered connectionist models for cognition: Phonological and Semantic Role; S. Werner and R. Smith, Eds., Heidelberg: Springer-Verlag, pp. 24–27.
- Henson, J., 1994, Connectionist syntax using temporal variable binding, Psych. Res., 23:553–569.
- James, J., and Patterson, E. L., 1997, Distributed representations of structures: A theory of analogy and mapping, Psych. Rev., 10:445–462.
- McClelland, J., and Rumelhart, D. E., 1981, An activationist model of cognition. In Parallel representations of the mind, Cambridge: MIT Press, pp. 1–96.
- Page, M., 2000, Cognitive modeling in psychology: A localist framework, Berlin: Springer, 243–254.
- Rumelhart, D., 1990, Thematic Role: Spatial Language and Constrained Connectionism, Cambridge, MA: MIT Press.
- Shastry, L., 1988, Semantic Networks: An Evolutionary Foundation for Connectionist Models, Cogn. Sci., 10(4):435–50.
- Shastry, L., 2001, Cognitive grounding of biological learning and long-term memory, in Emergent Properties of Artificial Intelligence, edited by J. Smola, S. Terner, and D. Wilhars, Eds., Berlin: Springer-Verlag, pp. 348–367.
- Shastry, L., 2001b, Episodic memory and cortico-hippocampal interactions, Trends in Neurosci, 4:7–12.
- Shastry, L., and Ajanagande, A., 1993, From symbols to systems: A connectionist encoding of rules, variables and temporal reasoning, Cogn. Brain, 16(4):417–460.
- Van, R. R., 1992, On variable binding in connectionist networks, Cogn. Sci., 4:93–124.
- Waltz, D. L., and Pollack, J. B., 1985, Massively parallel parsing: A highly interactive model of natural language interpretation, Cogn. Sci., 9:51–74.

# 结构化连接主义的优势

结构化连接主义方法促进了包含不同类型节点的网络的发展，涉及差异学习并整合解剖和生理约束——这是一种实现高水平的抽象方法。这导致了记忆、推理和语言等大规模认知模型的发展。这些模型的表示能力超过了为相似认知现象开发的并行网络。此外，结构化连接主义方法不是开发将方框视为特征的网络，而是开发了定义认知功能（例如记忆）的网络。结构化连接主义提供了结构与功能之间的对应，这有助于更好地理解认的神经基础。

# 讨论

结构性连接主义为生物学引导的认知发展提供了一个丰富的框架。结构化连接主义提供了一个丰富的框架，用于生物学引导的认知发展。结构化连接主义提供了结构与功能之间的对应，这有助于更好地理解认知的神经基础。

# 支持向量机

引言

连接主义网络中的变量绑定问题之一是，为了使用点积作为相似性度量，我们首先需要将模式映射到点积空间。为此，我们假设

$$(x_1, \dots, x_n) \in \mathcal{X}$$

换句话说，我们定义了一个分类函数 `f: \mathcal{X} \to \{\pm1\}`。对于未知分布 `P` 的训练和测试，我们希望得到较小的误差。

$$R(f) = \frac{1}{2} \int f(x) dP(x)$$

如果 `(x, y)` 被正确分类，则损失为 `0`，否则为 `1`。

# 算法

首先，我们并没有假设模式实际上存在于点积空间。因此，我们使用一个映射 `Φ` 到特征空间。

$$y = sign (\langle c_m, w \rangle)$$

$$y = sign (\langle x, (c_m + c_n)/2, w - c_m \rangle)$$

$$y = sign (\langle x - c_n, w \rangle)$$

如果我们使用基准 `Φ` 将 `x` 映射到向量表示。

$$\Phi : X \to Y$$

$$x := \Phi(x)$$

其次，即使原始模式在点积空间，我们仍然可能考虑更通用的相似性度量。

$$b := \frac{1}{2}(\|c_m\|^2 - \|c_n\|^2)$$

在这里，我们定义了偏移，如果均值到原点的距离相同，则该偏移为零。

这种类型的相似性度量非常不同；因此我们从一个特殊情况开始推广到一个简单的情况。一种重要的相似性度量是点积。对于给定的两个向量 `x, x' \in R^d`，标准点积定义为：

$$\langle x, x' \rangle = [x][x']$$

标准点积的几何意义是它计算向量 `x` 和 `x'` 之间角的余弦，前提是它们被归一化为长度 1。此外，它也涵盖了 `x` 的长度（范数）。能够对模式进行点积允许我们进行所有的几何构造。然而，请注意点积方法在处理有趣的问题时并不完全充分。

$$\langle x, x \rangle := (x, x)$$

# 核相似性度量

让我们考虑一个通常被称为的函数

$$k : X \times X \to R$$

$$k(x, x') := (x', x')$$

核方法的一个优势是它们独立于特征。这允许我们适应特定的问题。

## 支持向量机

八，通过方程 1 和 10 得到决策函数

```
```
