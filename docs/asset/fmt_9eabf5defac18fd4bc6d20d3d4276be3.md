
- Hines, M. L., and Carvevale, N., 2001. A tool for neuroscientists, Neuroscientia, 7:123–135.

- Kergman, B. W., and Pike, R., 1984, UNIX Programming Environment, Englewood Cliffs, NJ: Prentice-Hall, pp. 329–333.

- Lytton, W. W., 1996. Optimizing synaptic conductance for networks, Neural Computational, 8:501–509.

- Moore, J., and Stuart, A. E., 2000, Neurons in Action: Computer Simulations with MATLAB, San Diego: American Physiological Society.

- Ruiter, A., properties of neurons, in Handbook of Physiology, vol. I, part 1, The Nervous System (Ed.), pp. 39–98.

# 神经障碍

## 为什么会有神经障碍？

神经障碍是关于大脑认知组织的重要争议来源。尽管存在明显的缺陷，患者往往能恢复到高水平的功能，这一事实限制了我们从他们身上学习的信息类型。然而，神经障碍的推断并不像看起来那样稳健。患者的大脑损伤并非由大脑一个或多个组件的简单缺失决定的，而是与其完好的部分。通常，大脑的塑性表明局部损伤也可以引起剩余部分的新功能模式。大脑的神经网络模型为理解关联系统的损失提供了一个框架（Farah, 1994）。此类系统的计算机模拟允许我们测试一个或多个单元的损伤如何影响单元之间的连接，可以通过损伤观察系统的行为。在许多突然引发的大脑损伤情况下，这与我们在正常系统中预期的非常不同，由于这种原因，解释神经障碍时使用的神经网络模型可能会对系统的性质产生非常不同的解释。加权连接决定了从一个单元到另一个单元的激活量，这与其他部分是并行的；因此，PDP 表征是分布在各个部分的激活模式，而长期记忆编码在分布于单元之间的连接模式中；因此有许多具有不同属性的 PDP 网络，网络类型是激活规则及其学习。PDP 在许多方面与包括大脑在内的真实神经网络不同。即使是最大的 PDP 网络，与只有一种类型单元和仅一种兴奋或抑制细胞的 PDP 网络相比，也是微不足道的。大脑拥有多种不同的神经元等等。当然，所有模型都是相关特征和理论相关特征的简化。理论相关特征包括不同神经元的使用、输入输出的数量以及单元之间连接的某些方面表现出的抑制和兴奋效应、速率和阈值。PDP 模型允许我们发现哪些行为（正常和病理）可以通过此类属性来解释。有三个属性如下所示

### 解释错误类型：聋性阅读写症病例

神经患者已经表明，可以根据所犯错误的类型推断出受损的组件。在阅读写症等综合症中，患者犯两种错误：语义错误和语音错误。语义错误涉及用一个词替换另一个词，例如用 `cat` 替换 `dog`。文章的剩余部分将通过一些著名的神经障碍示例来支持这些说法，这些障碍的视觉解释是经过神经网络建模改变的正常脑。在每个示例中，使用神经网络来模拟脑组织的处理，遵循并行分布式处理（PDP）的传统。Ruhemart 和 McLlland，PDP 系统由大量高度连接的类神经单元组成。这些单元通过正常网络中具有吸引子位置的若干病变效应相互连接，以访问患者的错误。建议，当系统在功能上受损时，错误类型的混合将是规律而非例外，从具有一组相似关系的表示（例如，在视觉上，`cat` 和 `cot` 相似）转换来，形成另一个具有不同相似关系的表示（例如，语义上，`cat` 和 `dog` 相似）。

不同的相似关系我们

Hinton 和 Shallice (1991) 触发了图 1 中的递归网络，在给定打印正字法的情况下产生一组单词的语义表示。当通过首字母映射出游戏-语义单元（作为语义表示的单位）时，义素（sememes）相互连接，并连接到最终的语义连接层，该层回溯到末端。语义层中的这种连接模式表明，对于特定单词的表示并不需要完美的表示；因为它与正确的语义（这是一个吸引子状态）足够相似，并且是内置的（即沿着单词的形状构建）。图 1 阐释了包含 `cot`、`cat` 和 `bed` 的激活空间区域的结构，以及形成语义损伤的改变后的结构。

当单词的首字母无法通过词尾的基准提供时，非单词字符串的单词会发生这种现象。这对于单词识别和空间注意力（字母与非字母）影响注意力分配的顺序，似乎具有相当具体但又出人意外的启示，即单词识别发生在首字母之后。

这里引入了吸引子的舒适性，表明视觉注意力过程可以无视阅读写症的影响效能。Behriman (1990) 通过在单词识别的计算模型中破坏注意力机制来研究阅读写症，使得注意力仅指向位于非单词之前的字母。事实上，我们视觉特征输出信息的门控可能需要来自字符串右侧的信息，但仅需要来自左侧的部分信息，这将导致表示。

Plaut 和 Shallice (1993) 通过使用各种不同的网络和不同的训练模式复制他们的结果，证明了 Hinton 和 Shallice 方法的通用性。存在一些吸引子，它们可以将那些基于视觉激活的相似性的输入模式转换为语义表示。激活空间的景观将由视觉相似性和语义相似性共同组织，由于网络损伤导致的失真会同时出现在视觉错误和语义错误中。

这种错误由于对左侧字母的视觉视觉信息不足而产生，这些信息不足以精确识别是哪些字母。相反，关于单词首字母的空间信息与剩余字母形成了一个与注意力模式相匹配的吸引子状态。因为单词是吸引子，网络将正确选择单词。通过这种方式，可以解释为什么阅读写症患者读得比非单词好，而不需要放弃注意力。

## 确定处理序列：忽视性阅读写症示例

视觉忽视患者会遗漏或错误识别字母字符串左侧的字母。当字母字符串是一个单词时，这种性能模式被称为忽视性阅读写症。惊讶的是，忽视性阅读写症患者更容易读出首字母。

值得注意的是，计算模型做出了可以测试的预测。根据这种忽视性阅读写症模型，它影响注意力，使得关于首字母的信息较少进入单词表示，激活状态不会落在正确单词的吸引盆内。Behriman (1990) 对左侧字母有严重忽视的读者测试了这一预测，他发现他们对单词首字母的感知并不比非单词更有效。此外，当他的注意力被引向左侧，且注意力不对称性变得不极端时，他显示出单词和名词字母字符串之间典型的差异。一个通常显示出单词和名词之间这种差异的患者，通过增加其非对称性的有意操控被阻止了这种差异的表现。

图 1。Hinton 和 Shallice (1991) 的阅读 PDP 模型，其中视觉图形表示与语义表示相关联。该模型中的单病变会导致视觉错误和语义错误的混合。

| 清理单元 |

| :--- |

| 义素单元 (Sememes Units) |

| 中间单元 |

| 字形单元 (Grapheme Units) |

## 正字法

## 语义

图 2。Plaut 和 Shallice (1993) 代表的 Hinton 和 Shallice 激活空间的一部分，显示了单词的吸引子。语义单元受损后，吸引盆从实线变为虚线所示，导致了视觉错误。

## 无需分离的分离：隐性识别示例

面脸识别症（Prosopagnosia）是一种识别障碍，可以独立于物体障碍而发生。行为性面脸识别症患者（下文描述）的案例表明，识别和意识依赖于可分离且不同的流式系统（图 3）。我和我的同事建立了一个计算机模拟，它能够以不同任务的方式无缝恢复（Farah, O'Reilly, and Vechara, 1993; O'Reilly and Farah, 1999）。网络如图 4 所示，由识别单元、语义单元、知识单元和脸部单元（分别为物理外观、关于它们的通用信息和名称）组成。这些层之间的隐藏层允许网络在学习中通过语义将脸部和名称联系起来。网络没有任何部分与意识相连。

第一个发现是，当配对为真时（例如，Harrison 的脸与 Harrison 的名字），模拟的面脸识别症学习将脸与名称关联的能力比为假时（例如，Harrison 的脸与 De Haan 的名字，De, June, and November, 1988）强。这最初被认为意味着这些患者正在正常识别脸部，而且在从视觉提取的处理层中（如图 3 所示），虽然脸部单元从视觉系统中消除了，网络恢复旧脸部-名称的速度也比新的快。我们为什么应该将学习看作一个穿过权重空间的过程。损伤后，网络在脸-名称模式和新模式上都处于权重空间的高区域，因此网络无法将任何脸与任何名称联系起来。然而，学习过程更短。

第二个发现是，在语境下先前熟悉的脸感知得更快，这之前被解释为对先前已知的面部感知的证据（De Haan, et al., 1997）。然而，当脸部单元进入稳定状态后，网络恢复旧脸部-名称的速度比新的快。图 3。De Haan 和 Greve (1992) 提出的关于隐性识别的注意力机制。

当视觉注意力受损时，由于注意力不对称性变得不极端，显示出单词和名词字母字符串之间的通常差异。图 4。O'Reilly 的脸 的模型，当其视觉激活性时，识别的出现。

当单词的首字母无法通过词尾的基准提供时，非单词字符串的单词会发生这种现象。这对于单词识别和空间注意力（字母与非字母）影响注意力分配的顺序，似乎具有相当具体但又出人意外的启示，即单词识别发生在首字母之后。

# 神经仿真：工具与资源 777

特定信息（Bower and Colouri, 2002; Skrzypak, 2014; Koch and Seeg, 2007；在本章中未列出神经化学家（参见 Mueller, 2010）。

本文还描述了增加不同程序之间可比性的努力，这些努力具有两个目的：首先，使用 `neuromatch` 构建的兼容性模型可以使用不同的程序进行独立评估和扩展；其次，描述不同复杂度水平（例如：分子、细胞、网络）的兼容性模型可以在它们之间相互关联。

## 通用考虑

选择仿真器程序时的通用考虑因素包括实验室的硬件能力和编程专业知识。复杂模型需要快速的工作站或并行运行的分布式计算节点网络（Hamill and Edelberg）。可能需要简化模型，以便性能较弱的计算机能够在合理的时间运行仿真。构建一个模型花费的时间比仿真一个模型要长，因此使用程序构建一个简单模型可以进一步加速过程。

## 硬件问题

各种仿真器的平台要求列在表 1 至表 3 中。我们包含了少数可以在所有平台上运行的程序（例如：`NEURON`, `ModelNet`）。用 Java 或 Peri 编写的程序（例如：`CATACAB`, `Neli`, `SWAP`, `Stochastic`）可以在无需修改的情况下在多个平台上运行。另一种解决方案是基于计算机的图形界面，这使得功能对用户界面敏感（例如：`NEST/SIM`, `ONICAL`）。对于某些仿真器，用户可以通过浏览器登录到中央网络服务器（例如：`iCell`, `CMSS`, `Web`）。

## 支持级别

一个重要问题是开发者提供多少支持（参见表 2）。大多数程序在更新程度上差异很大。商业软件包的者可能会获得个人指导（例如：`iCell`, `Simulator ModelMaker`, `SABER`）。另一种选择是参加工作坊或国家会议的短期课程（例如：`GENESIS`, `MCell`, `NEURON`, `SNAP`）。许多开发者维护邮件列表或论坛，用户可以在那里提问。

离散连接器通常使用标量变量来表示发放率和突触权重（单细胞模型）。用于描述离散事件变化的积分法（例如：`NeuroNet`）更加真实。它们使用一种方法来累加脉冲之间的间隔，这发生在膜电位达到阈值时，以及不应期。当触发脉冲时，会产生一个定时脉冲事件（而非动作电位），膜电位被重置。

通过调整控制各种生物网络阈值和频率适应性的参数，对膜电位的电导适用于研究。离散事件更适用于产生它们的相互作用（例如：`INTEGRATE-FIN-AND-NEUR`）。

常微分方程 (`ODE`)。大多数仿真器将神经元表示为 `ODE` 系统，这些系统描述了在仿真时间步内，定义良好的空间隔间内依赖变量（通常是电压或浓度）的变化（Bogg and Foster, 1998）。定期间隔的离散事件允许用户选择模型的特征（通常是数十个微连接）。在某些仿真器中，使用可变时间步，其中依赖变量变化快速时变化大，缓慢时变化小。这些算法可以缩短模拟大型网络的计算机时间。

蒙特卡洛方法。其他仿真器显式地随每个时间步跟踪每个分子（例如：`BOQ`, `CMSS`, `StochSim`）。在每个时间步，为……选择随机数用于

## 网站

| 表 1. 适用于仿真和教学的程序 |
| 名称 | 工具 | 控制 | 平台 | 支持 | 网站 |
|---|---|---|---|---|---|
| ArtMemMemProtMem S | PIACS | G | W, DOS | M | http://www.umd.edu/PHISoft/ |
| cLabs S | PIACS | G |  | T | http://www.clubs.de/clabs.html |
| Neuroscience Science | C |  |  | M | http://sdphis.edu/icell/ |
| AC |  |  | W | T | T |net-neuron.com/ |
| NerveWorks | PIACS | G | M, U | W | T://www.genesis.edu/of/ |
| NeuroSim S | PIACS | G |  | T | http://sites.ac.uk/neutrosim/ |
| Vclamp/Electroology | C | G | W, DOS | M | T | http://stanford.edu/~johnf/ |
| * |该软件必须购买。工具：P = 静性膜；I = 离子通道；N = 神经元。控制：C = 命令行；S = 脚本；平台：M = MacOS；W = Windows。支持：T = 模板；L = 列表。 | | | | |

## 第三部分：神经生物学建模

**表 2. 适用于神经生物学建模**

| 名称 | 脉冲动力学 | 化学动力学 | 控制 | 平台 | 支持 | 网站 |
|---|---|---|---|---|---|---|
| BioPSN | ODE |  | G W | U | T M | http://www.utah.edu/biops/ |
| BSimM | ODE |  | G. W |  | U | T | http://um-ai.edu/kjdp/bios/ |
| CATALCOMB | ODE |  | G, M | M, W |  | http://computer.com/catacomb/ |
| CONIS | ODE |  | C, M | D, O | S | http://street.conical/ |
| GENESIS | ODE |  | S G | U | T C L | http://genesis-sim.org/GENESIS/ |
| MaxNeuron | ODE |  |  |  |  | http://maxneuron.com/maxsim/ |
| Mcell | ODE | MC | C S | U | T C L | http://mcell.edu/ |
| NeuroNet | ODE |  | S G | U | T C L | http://montana.edu/neuro-research/ |
| NESTySim | ODE Inf |  |  |  | T M | http://nest-sim.org/ |
| Neurolator |  | ODE Inf | G W | U | T M | http://cellinfo.com/ni/ |
| NEURON | ODE |  | C G | U | M | http://neuron.yale.edu/ |
| Nodux | ODE |  | D, O S | U |  | http://neuroanatomy.com/opera.html |
| NSY | SDL Inf |  | S G | U |  | http://bf.um-ai.edu/BASFT/ |
| SEES | ODE |  | C M, W | U | T M | http://hub-ub.projects/nets.html |
| SNAP | ODE |  | S G | U |  |  | http://neuroscience-atlas.org/ |
| SPKE | ODE Inf |  |  |  | T C L | http://nsim.com/conf/tools/ |
| SONN | ODE Inf |  |  |  |  | http://hiij.edu/itika-live/sonn.html |
| SurHyper | ODE |  | G W | U |  |  | http://ucf.edu/atlas-spike/ |
| XNBQ | ODE Inf |  |  |  | M L | http://cfgfly.org/freehyper/ |
| YBIQ | ODE |  | G W | U | M | http://4444.caussie,freeja/ |
| CS |  |  |  |  | T M | http://atlasmap.com/it-bioq.html |
| DSalve | ODE |  | G W | U | T M | http://atlasmap.com/it-gorany/ |
| In Silico Cell | ODE |  |  |  |  | http://gepsi.org/ |
| JarnacIndigo | ODE |  | S G | U | T M L | http://www.sys-bio.org/ |
| KimSimFish |  |  |  |  |  |  | http://biocheck.weed.edu/v3/facenews.html |
| MAK | ODE |  |  | M, W | M | http://nnk.edu/netdep/hd/arkmet.xml |
| MetaModel |  |  |  |  |  | M | http://www.modelkinetics.com/ |
