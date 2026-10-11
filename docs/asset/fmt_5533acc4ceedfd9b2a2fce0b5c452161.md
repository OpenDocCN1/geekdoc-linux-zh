
## 支持向量机

一个泛化良好的分类器是通过同时控制分类器容量和松弛变量 `$\xi_i$` 之和来实现的。可以证明它提供了训练误差数量的上界。使用软分类器的一种实现方法是通过最小化目标函数得到的：

$$
$$\min(w, \xi) = \frac{1}{2}||w||^2 + C\sum_{i=1}^{m} \xi_i
$$

![](img/5cb7d541b875c6d6c2092ad1a376440a_1141_0.png)

**图 3.** SVM 的思想：将数据映射到高维空间并构建一个具有最大间隔的分类超平面。这在输入空间中产生了一个决策边界。通过使用核（公式 3），可以在不显式将数据映射到特征空间的情况下计算出分离超平面（来自 Schölkopf, B., and Smola, A., 2002, *Learning with Kernels*, Cambridge, MA MIT Press. 经许可。）

受公式 34 和 35 中约束的，其中 `C>0` 决定了间隔与训练误差最小化之间的权衡。这种方法导致了最大间隔问题 32，受修改后的约束限制，其中与分离器的差异是误差 `C` 的上界。

另一种实现使用了更自然的 `$\alpha$` 参数化。在其中，参数 `C` 被替换为 `$\alpha \in (0, 1)$`，这使得间隔成为支持向量（SV）以及具有非零松弛变量样本数量直接上界。其对偶问题是最大化公式 32 中的二次部分，受 `0 \le \alpha_i \le \alpha_{max}`、`$\sum \alpha_i = 0$` 和 `C_{\max}=1` 的限制。

$$
maximize $W(\alpha) = \sum_{i=1}^{m} \alpha_i^2 - \frac{1}{2} \sum_{i,j=1}^{m} \alpha_i \alpha_j k(x_i, x_j)
$$

满足条件：

$$
\alpha_i \ge 0 \text{ 对于所有 } i=1, \dots, m \text{ 且 } \sum \alpha_i = 0
$$

**图 4** 示例说明。在实践中，如果高噪声水平导致类别之间大量重叠，可能不存在分离超平面。为了适应这一点，引入了松弛变量：

$$
\xi_i \ge 0 \text{ 对于所有 } i=1, \dots, m
$$

为了放公式 22 的约束：

$$
$y_i(\langle w, x_i\rangle + b) \ge 1 - \xi_i \text{ 对于所有 } i=1, \dots, m
$$

## 支持向量回归

与其处理离群值不同，回归关注的是估计实值函数 `y \in \mathbb{R}`。

为了将 SVM 扩展到回归算法，Vapnik (1995) 引入了 `$\epsilon$`-敏感损失函数：

$$
f(x) = \langle w, x\rangle + b
$$

我们最小化：

$$
\frac{1}{2}||w||^2 + C\sum_{i=1}^{m} \max(0, |y_i - f(x_i)| - \epsilon)
$$

在这里，项 `$\epsilon$` 与模式识别中的（公式 36）相同。我们通过添加松弛变量将其转换为一个约束优化问题，类似于软分类器。

类似的分析说明了损失（对于对偶而言，`C \ge 0`）提供了一个：

$$
maximize W(\alpha, \alpha^*) = -\frac{1}{2}\sum (\alpha_i^2 + (\alpha_i^*)^2) + \sum \alpha_i \alpha_j^* y_i y_j k(x_i, x_j)
$$

满足条件：

$$
0 \le \alpha_i, \alpha_i^* \le C \text{ 对于所有 } i=1, \dots, m \text{ 且 } \sum (\alpha_i - \alpha_i^*) = 0
$$

回归估计为：

$$
f(x) = \sum_{i=1}^{m} (\alpha_i - \alpha_i^*)k(x_i, x) + b
$$

其中，对于所有位于 `$\epsilon$`-管道之外的点，`$\alpha_i - \alpha_i^*$` 为零。注意其与模式识别案例的相似性（参见公式 31 和图 6）。

![](img/5cb7d541b875c6d6c2092ad1a376440a_1141_1.png)

**图 4** 使用径向基核 `k(x, x') = \exp(-||x-x'||^2/2\sigma^2)` 找到分类器的示例。圆圈和点是两类训练示例；决策线是精确符合公式 22 中公式约束的曲面。注意，算法找到的支持向量（位于输入约束上）并不是某些对于泛化分类至关重要的示例。

## 第三部分：文章

![](img/5cb7d541b875c6d6c2092ad1a376440a_1142_0.png)

**图 5.** 在支持向量回归中，半径为 `$\epsilon$` 的管道拟合数据。模型复杂度与管道外点（带有松弛变量 `$\xi$`）之间的权衡由最小化目标决定。（来自 Schölkopf, B., and Smola, A., 2002, *Learning with Kernels*, Cambridge, MA MIT Press. 经许可。）

## 核成分分析

核技巧（trick）可以用于开发任何可以转换为点积的现代泛化算法，例如 PCA。在特征空间中找到所谓的协方差矩阵 `C` 的特征向量 `v` 和特征值 `$\lambda$`：

$$
C = \frac{1}{m} \sum \Phi(x_i)\Phi(x_i)^T
$$

在 `$\Phi$` 是高维的情况下，直接执行的成本是巨大的。幸运的是，可以证明 `$\lambda \neq 0$` 位于训练数据的图像空间内。那么我们可以将解扩展为：

$$
v = \sum \alpha_i \Phi(x_i)
$$

其中 `$\alpha = (\alpha_1, \dots, \alpha_n)$` 满足 `|\alpha|^2 = 1`。为了从测试点 `x` 提取特征，我们可以计算点积 `$\Phi(x)$` 和第 `n` 个特征空间：

$$
v^*(\Phi(x)) = \sum \alpha_i \Phi(x_i, x)
$$

图 7 显示了一个示例。在 SVM 的情况下，核可以通过图 6 可视化。

![](img/5cb7d541b875c6d6c2092ad1a376440a_1142_1.png)

**图 6.** SVM 和核方法的架构。SVM 和扩展部分（svx）显示在投影到特征空间 `$\Phi$` 中的两类。结果是点积的线性组合。例如，在识别中，`y=y_i`；在回归中，`v_i=\alpha_i^*`；或在特征值问题（核函数）。核 `k` 定义为函数 `$\sigma(x,x)$` 以及核 PCA 中，`$\sigma(x,x)=x`。

## 实现与结果

SVM 的一个缺点是二次规划问题的大小随样本数量增加。在实践中，训练集并不包含所有的 SVM。我们的实践是通过通道数据来提取 SVM，这揭示了最初未识别模式的可能性。如果不检查，目标函数的大小将 `m \times m`，其中 `m` 是所有训练示例的数量。

是否存在高噪声问题？在这种情况下，许多松弛变量 `$\xi_i$` 变为非零，所有示例都变成 SVM。对于这种情况，分解算法基于支持 SVM，因此我们可以离开当前块（例如，如果 `$\xi_i=0$`），所有现代实现可以在更大的范围内进行训练。成功案例包括 600 示例。

![](img/5cb7d541b875c6d6c2092ad1a376440a_1143_0.png)

**图 7** 使用径向基函数对三个高斯簇数据进行核 PCA 的前非线性特征的等高线。在左上面板中，第一和第二分量将数据分为三类。注意核 PCA 并不是为了聚类；它是为了提供 PCA 描述

## 讨论

MNIST 数字识别基准（带有记录的结果），DeCoste 和 Schkopf (2000)，以及问题分类-例如机器 (1999) 和解释。对于分类、密度估计和新颖检测等问题的各种应用视图，请参考 Burgers (1998), Papnik (1998), Schkopf, and Smola (1999), Smola et al. (2000), Cristiani and Shaw-Taylor (2000), 以及 Schkopf and Smola (2002)。

在过去的几年里，SVM 和其他方法已迅速成为处理大规模和高维数据的标准工具包。这种分析可能是由于与神经网络相比的许多优势，例如在优化过程中不存在伪局部最小值、在应用中易部署、表示模式可以与其他算法相结合，以及在高维上的卓越性能。

科学界特别感兴趣的是学习方法如何在执行简单几何算法的高维空间中表示数据。值得注意的是，尽管这些方法是基于学习问题的数学分析（由 Papnik 和 Schkopf 给出的公式），但它们并不限于任何

## 参考文献

- Boser, B. E., Guyon, I., and Papnik, V., 1992, Optimal classifiers, in Proceedings of the 5th Annual ACM Workshop on Computational Learning (D. Huisle, Ed.), ACM Press, pp. 144–157.
- Burgers, C., 1999, A support vector machine for classification, Data Mining Knowledge Discovery, 3(1):161–177.
- Cristiani, N., and Shaw-Taylor, J., 2000, An Introduction to Support Vector Machines, Cambridge, J.: Cambridge University.
- Haussler, D., 1999, Convolutional Kernels on Discrete Structures, Techniques in Machine Learning, MIT Press, University of California at Santa Barbara.
- Herholz, R., 2002, Learning classifiers: Theory and applications, Artificial Intelligence, 130(1-2):1–39.
- Hoge, A., Papnik, V., 1999, Large scale SVM learning. In: Support Vector Machines (B. Schkopf, C. J. C. Burges, and A. J. Smola, Eds.), MIT Press, pp. 69–102.
- Schkopf, B., and Smola, A. J., 2002, *Learning with Kernels*, Cambridge, MA MIT Press.
- Smola, A. J., Bartlett, P., Schkopf, B., and Schulmans, D., 2000, Advantages of Large Scale Classifiers, Cambridge, MA: MIT Press.
- Poggio, A., 1990, The Theory of the Large Brain. In: AI Note, 1253, Cambridge: Massachusetts Institute of Technology, Artificial Intelligence.
- Papnik, V., 2000, Statistical Learning Theory, New York: Wiley.
- Watkopf, C., 2000, Dynamic alignment kernels, in Large Margin Classifiers (B. Schkopf, C. J. C. Burges, and A. J. Smola, Eds.), Cambridge, MA: MIT Press.
- Williams, C. K. I., 1998, Prediction with Gaussian processes: From linear regression to nonlinear prediction, and Learning and Inference in Generative Models (M. I. Jordan), Boston: Flauer.

## 突触交互

Alain Destexch, Zachary F. Mainen, and Terrence J. Sejowski

### 引言

在网络模型中对突触交互进行建模至关重要。此类模型不仅能够捕捉突触交互的重要生理特征，而且以计算高效的方式实现，从而促进大型网络的仿真。本文回顾了解决这些需求的几类模型。

突触释放是由离子通道和突触前末梢后突触重留激活的。动力学模型具有足够的表达能力来描述构成突触电流的离子通道行为。

然而，对突触的完全表示对动力学模型来说过于复杂，但存在某些计算效率更高的简单动力学模型。我们证明这些模型可以捕捉多种类型突触响应的时间和动力学，使其对网络中的突触交互建模非常有用。

### 突触电流模型

对于不包含电位的神经模型，突触电流通常被建模为突触活动测量的直接函数。在最简单的情况下，突触交互通过 sigmoid 函数和突触活动描述。或者，后突触电流可以用一阶方程描述，其中一个项通过 sigmoid 函数取决于后突触膜电位。

另一种方法是对脉冲神经元之间的突触交互进行建模。假设突触脉冲会触发一系列后突触电位。一种用于后突触电导增加的流行模型是由于 Ruff (1967) 提出的 alpha 函数。

$$r(t) = r_0 \cdot \exp[(t-t_0)/\tau_r]$$

`r(t)` 是后突触电位 (PSP) 的时间曲线。alpha 函数和指数衰减足够通用，可以用少量的参数近似大多数突触电流。它们已广泛应用于电生理学和感官研究（Saksmann and Heller, 1995）。alpha 函数或相关方法的局限性包括缺乏直接的生物学解释，以及突触前末梢产生的后突触电流 (PSC) 缺乏自然限制。

一种自然的方法基于底层离子通道的动力学对突触电流进行建模。动力学方法在该领域被广泛，从 Huxley (1952) 描述电压依赖离子通道的模型开始（见 Hille, 2001 回述）。动力学模型可以详细描述离子通道的性质，并由底层突触信号传递和神经调节的化学模型生成。在下一节中，我们将展示如何用动力学形式对各种离子通道进行建模。

### 动力学

离子通道是具有不同构象态的蛋白质，其中某些状态为“关闭”、“灭活”或“脱敏”，不导电。单通道记录技术已证明构象态之间的转换是随机且反应性的（见 Saksmann and Heller, 1995）。它有助于以与时间无关概率建模离子通道在状态之间的行为。

从单个通道的微观描述到相似通道的宏观描述是直接的。在大数量的极限下，单个通道的统计行为可以用一组类似于普通化学反应的连续微分方程来描述。由以下连接的构象通道 `S_1 \dots S_n` 的存在或组合：

$$S_i \rightleftharpoons S_j \rightleftharpoons \dots \rightleftharpoons S_n$$

定义 `s_i` 为状态 `S_i` 下通道的比例，`r_{ij}` 为转换速率：

$$S_i \rightleftharpoons S_j$$

从而给出动力学方程：

$$\frac{ds_i}{dt} = \sum_j r_{ji}s_j - \sum_j r_{ij}s_i$$

通道表现出的广泛行为源于转换对通道外部因素依赖，例如与分子结合或跨膜电场。这些因素被称为配体门控和电压门控受体。

对于电压依赖离子，状态 `S_i` 和 `S_j` 之间的转换发生的速率取决于电压，例如：

$$r_{ij}(V)$$

电压依赖性的函数形式可以从简单的动力学建模获得（见 Huxley and Neher, 1995）。离子通道电压依赖性的动力学描述是通用的。特别是，著名的 Hod 钾离子通道模型可以用四通道模型表示。

对于配体门控通道，两个状态 `S_i` 和 `S_j` 之间的转换取决于 `n` 个配体分子 `L` 的结合：

$$S_i + nL \rightleftharpoons S_j$$

可以写为：

$$r_{ij}(L)$$

$$S_i + nL \rightleftharpoons S_j$$

其中 `L` 是配体浓度，`r(L) = r_0 L^n`。在该模型中，速率常数对配体具有简单的函数依赖性。对于某些受体类型，速率常数也取决于电压。

氨基酸通过离子性突触起作用，这种突触是神经递质分子检测到的离子通道。相比之下，代谢受体没有离子通道，与受体的结合会触发胞内信使（例如钙或蛋白）的激活，从而独立于受体控制离子通道的门控。这两种突触受体将在后续章节中讨论。

### 离子性受体的动力学模型：AMPA, NMDA, GABA

常见的配体门控受体类型是兴奋性 AMPA、NMDA 和抑制性 GABA。已经提出了许多动力学模型（见 Sakmann and Heller, 1995）。例如，AMPA 受体的多状态方案（Standley, Underwood, 1993）为：

$$D \rightleftharpoons[r_2](L)] C \rightleftharpoons[r_4](L) C_* \rightleftharpoons[r_6](L) O$$

其中 `D` 是关闭态，`C` 和 `C_*` 是单结合态和双结合态，`O` 是开放态，`D_*` 是脱敏双结合态。

该 AMPA 模型已用于解释这些受体的电生理特性（Destercke et al., 1994）。然而，状态数较少的简化方案可以很好地近似突触电流的时间和动力学行为。特别是，涉及两个状态的最简单方案：

$$C \rightleftharpoons[r_2](L) O \rightleftharpoons[r_4](L) C_* \rightleftharpoons[r_6](L) D$$

在这些方案中，`C` 和 `O` 代表通道的关闭态开放态，`D` 代表脱敏态，`r_1 \dots r_n` 是相关的速率常数。

简化模型的另一种方法是证明使用短时间氨基酸脉冲可以产生时间限制的突触响应（Sakmann and Neher, 1995）。这些数据表明响应时间是由动力学决定的，而不是神经递质的时间曲线。因此，可以假设神经递质是以每次突触脉冲触发的短暂（~1 ms）脉冲形式传递的。

AMPA 响应的简化方案可以与详细的动力学模型进行比较，以判断方法的质量（图 1-D）。脉冲需要一个瞬态事件，代表突触间隙中神经递质的释放。在 AMPA 动力学模型的仿真中，神经递质的时间曲线是通过突触前脉冲得出的。图 1-C 显示了对高频脉冲串的 AMPA 响应。响应幅度由于脱敏态而降低。使用脉冲的简化动力学方案可以很好地拟合多次连续事件期间兴奋性电流的时间曲线。

## AMPA/Kainate

## NMDA

![](img/5cb7d541b875c6d6c2092ad1a376440a_1146_0.png)

图 2. 基本动力学方案为突触后电流提供了良好的模型。A，AMPA 介导电流（由 Z. Xing, A. C. Greenwood 和 T. Brown 提供），NMDA 介导电流（由 N. A. Hessler 和 R. Malinowsky 提供），C，GABA 介导电流（由 T. S. Ono 和 I. Mojo 提供），D，GABA 介导电流（由 S. T 提供）。此处使用简单的动力学模型展示了突触电流的平均记录（A 和 B 的负电流向上；连续迹线——对于 A、B、C 为脉冲脉冲；A 修改自 Desethe 等人，1998 年；D 修改自 Desethe 等人，1998 年）。
速率和其他参数的数值可参考 Desethe 等人，1998 年。

## GABA_A

## GABA_B

![](img/5cb7d541b875c6d6c2092ad1a376440a_1146_1.png)

1D). 相比之下，Alpha 函数并不匹配突触电流的加和行为（图 1E）。对于其他类型的门控通道（包括 NMDA 和 GABA 受体），使用简单的动力学模型，可以获得类似于应用于 AMPA 响应的程序。双态模型和三态模型对 PSC 的全细胞记录提供了良好的拟合（图 2B–C），更多细节请详阅 Desethe 等人，1994 年，1998 年。

## 受体的动力学模型：GABA 与神经调节

某些神经调节蛋白并不直接结合到离子通道，而是通过第二信使起作用，将激活的受体与通道的开放联系起来。这种相互作用被称为神经调节，其发生的时间尺度比配体门控通道慢。如乙酰胆碱（ACh）（在第2 阶段）、血清素（HT-1）、多巴胺（D2）和 GABA 通过 G 蛋白的作用激活 K+ 通道（见 Brown, 1990 述）。我们开发了 GABA 受体介导的 G 蛋白响应动力学模型（Desethe 和 Sejnkowski，1995），它可以应用于这些递质中的任何一种。

与响应弱刺激的 GABA_A 受体不同，GABA_B 受体需要高水平的突触活动（Mody 等，1994）。这种特性可能由于 GABA_A 受体的突触外定位，但也完全从 GABA 响应期间 G 蛋白级联反应的动力学角度解释（Desethe 和 Sejnkowski，1995）。激活 GABA_B 响应的高水平活动可以通过以下动力学方案复制：

$R + T \rightarrow R \rightarrow D$ (11)

$R + G_i \rightarrow RG \rightarrow R + G$ (12)

$C_i \rightarrow G_i$ (13)

$G_i \rightarrow C$ (14)

其中，递质 T 结合到受体 R，导致激活形式 R 和 D 形式。G 蛋白通过激活的受体转化（G 蛋白结合）。最后，R 与 $K^+$ 通道结合，具有独立的结合位点。通过假设方程 12 和 14 具有准稳态，忽略脱敏，并考虑 $G_0$ 过量，可以获得具有相似行为的简化模型：

$\frac{dr}{dt} = K_1[T](1-r) - K_2r$ (15)

$\frac{dx}{dt} = K_{sf} - K_{as}$ (16)

## 突触相互作用 1129

**图 3.** 用于模拟丘脑网（RE）和丘脑核（TC）神经元小网络的突触电流动力学模型。这些神经元具有内在特性，在去极化或超极化后驱动动作电位脉冲。它们通过多种受体类型连接（对 AMPA 有选择性，以及从 RE 到 TC 的 GABA 混合）。模拟显示出振荡行为，其中精确的频率和相位关系取决于内在钙和电压依赖电流。需要用正确的动力学对突触电流进行建模以匹配实验观察（修改自 Dexthe 等人，1996；另见 SLEEP OSCILLATIONS）。

![](img/5cb7d541b875c6d6c2092ad1a376440a_1147_0.png)

$r$ 是丘脑区域受体的比例，$g$ 是 G 蛋白的归一化浓度，$K_1 \dots K_4$ 是速率常数。K^* 通道处于开放形式的比例给出：

$|O| = \frac{s^*}{s^* + K_d} (17)$

其中 $K_d$ 是 $g$ 在 $K^*$ 通道上结合的解离常数。这种计算高效的模型可以拟合 GABA性 IPSCs（图 2D），并考虑到 GABA 响应的典型依赖性（Dexthe 和 Sejkowski，1995）。K^* 通道处于开放形式的比例给出：

$|O| = \frac{s^*}{s^* + K_d} (17)$

其中 $K_d$ 是 $g$ 在 $K^*$ 通道上结合的解离常数。这种计算高效的模型可以拟合 GABA性 IPSCs（图 2D），并考虑到 GABA 响应的典型依赖性（Dexthe 和 Sejkowski，1995）。激活 GABA_B 响应的高水平活动可以通过以下动力学方案复制：

$R + T \rightarrow R \rightarrow D$ (11)

$R + G_i \rightarrow RG \rightarrow R + G$ (12)

$C_i \rightarrow G_i$ (13)

$G_i \rightarrow C$ (14)

其中，递质 T 结合到受体 R，导致激活形式 R 和 D 形式。G 蛋白通过激活的受体转化（G 蛋白结合）。最后，R 与 $K^+$ 通道结合，具有独立的结合位点。通过假设方程 12 和 14 具有准稳态，忽略脱敏，并考虑 $G_0$ 过量，可以获得具有相似行为的简化模型：

$\frac{dr}{dt} = K_1[T](1-r) - K_2r$ (15)

$\frac{dx}{dt} = K_{sf} - K_{as}$ (16)

## 神经元网络模拟

使用快速简单的机制来模拟生物网络中的突触相互作用。基于介导突触响应的离子通道动力学的简单模型可以以很小的计算开销实现。这些模型捕捉了实例事件的广泛特征（加和、饱和、去同步），对于研究神经元同步非同步振荡和传播的网络行为至关重要。

所示模型均使用 NEURON（Hines 和 Carlisle, 1997）进行模拟。NEURON 软件和其他程序用于模拟这些模型，可在 http://www.nci.edu/neuron/ 或按要求获取。

生物地图与同步

轴：轴模型

相关阅读：神经元的生物马赛：离子通道与时间特异性；去同步：突触动力学

#参考文献

Brown, D. A., 1996, G-protein and potassium currents in neurons, Ann. Rev. Phys., 52:215-242

Deshtex, A., Bal, T. T., McCormick, D. A., and Sejkowski, J. T., 1996, Ionic kinetics of unynchronized oscillations and propagating

# 突触噪声 (SN) 与脊椎动物神经元中的混沌

递归图 (RPs) 以方矩阵的形式表示了 d 维信号的动力学（Eckmann, Kamphmeier and Ruelle, 1985）。当向量 $\vec{x}_i$ 和 $\vec{x}_j$ 处于预定义的阈值 $\epsilon$ 内时，RP 在 $(i, j)$ 处显示一个点。在二维空间中，事件之间的时间差定义为 $I_{i,j} = |i - j|$，其中 $I_{i,j} \approx \tau$ 是活动周期。如果 $I_{i,j} \le \tau$，则 $\epsilon = \tau$（见图 1c，左）。因此，长度为 $L$ 的段表示空间中在一段时间内保持接近的递归点数量。

RP 的结构揭示了动力学特征，通过适当的技术指示所研究信号在相空间中是离散的还是连续的（Schreber, 1999）。RP 捕捉了确定性、混沌或随机系统中小尺度不连续性或大尺度结构的形式（见图 1c）。这种方法对于检测 SN 中的周期性和非周期性混沌模式非常有用。

序列级参数可以通过量化使用长度为 $L$ 的向上对角线段的确定性程度来估计。特别是，对角线段中中点的比例（$\delta$）由 RP 中点的总数决定（Weber and Zblatt, 1994）。$\delta$ 的值是直方图的函数。这与动力系统的经典解释有关，即柯尔莫哥洛-Sina 熵（Furey and Kahn, 1998）及其作为 $C$ 函数的变体，用于表征时间序列的动力学（图 1d，插图）。

在连续事件之间的时间间隔情况下，寻找一个与下一个之间确定性关系的方法是将每个间隔 $I_i$ 对 $I_{i+1}$ 作图。回归图 (RM) 显示了 SN 中的动力学和分叉 (BIFURCATION)，这使得动力学可以可视化为点对序列。在周期动力学情况下，这些点被分组成簇；在混沌情况下，则表现为一种不填充空间的扩展结构。对于 M 细胞 SN，通过改变阈值 $\theta$，在多个事件中观察到了高周期性的 RM。随着 $\theta$ 的逐渐增加，RM 显示了三种不同的模式。第一种是周期性的——

可以使用精细的分析来确定 SN 中的频率漂移是与噪声还是确定性动力学有关。以这种方式注意到的 RM 在三个水平的群体出现后，具有出乎意料和预期的周期性，都在范围内范围内（Faure, and Kahn, 2000）。

## SN 中的不稳定周期轨道与确定性

在相空间中，周期轨道是动力系统 (SN) 和神经元中分叉 (BIFURCATION) 的平衡态。如果没有不稳定轨道，任何轨迹都会从周期轨道被排斥（由于相位近似）。收敛性会离开不稳定周期轨道 (UPOs)，这可以作为混沌的指标。它们可以通过检测使用几何规则趋近并描述周期轨道的稀有事件序列来识别（见，et al., 1998）。在三角形模式的 SN 中发现了 UPOs（图 2b）。此外，M 细胞还包含其他由重复识别和间歇锁定（现在）定义的其他类型的递归。因此，SN 中时间通道的多样性可能存在于突触网络中。

## 时间模式的传输；学习的影响

如果信息不是来自整合神经元上的独立代理群体，那么编码在单个脉冲中的任何信息都会丢失，因此该群体可以被单个随机通道取代。但只有当并行通道模拟了突触后效应时（Perkel and Bucks, 1996），这才是真实的。

SN 的各种几乎周期的事件体现在同一条训练序列中，如果某些事件恰好发生在之前/下方？那么对于观察到的突触对之间的全局转换（图 2a 到 2b），事件的分布则较低（图 3a）。RPS 的这些属性与突触动力学的发现是一致的。

事实上，诱发递质的自由度是概率性的。也就是说，通信由两个二进制参数 $p$ 和 $q$ 支配求q$ 代表能够表示脉冲的“基本单元”群体，$p$ 代表它们的平均概率。乘积 $np$ 是我们所说的连续周期之间接头的平均数量（图 3b）。乘积 $np$ 是决定突触效率的量。

在图 3c 中实现模型，每个振荡器末端带有“突触”，这表明如果 $p$ 在所有它们中不相同，突触后事件将在范围内波动，且不会发生频率锁定（图 3d）。鉴于不同的突触后效应，RPS 将表现出此类分级特征，正如实验观察到的那样（图 2e）。因此，异质性提供了一种“分离”的活动模式，SN 对应于突触网络的动力学。这已通过调查长期同步的年龄得到了验证，这种同步可能发生在 MC 抑制系统中。PMS 中的模式以及学习的增强（见于 Faure, 2000）。

**图 2. PM 分析，A₁ 和 C。** 实验图显示了两个检测到的事件的 10 个样本 SN 的平均值，B 为从 A₁ 中提取的、具有稳定（St.）和不稳定（Un.）流形的 4 个 UPOs，在 C 中% 和 det 参数的变化水平随 $\theta$ 的函数而变化。垂直线表示 2ˢ⁶ 处的 95% 水平（A, b 来自 fromid, 2000）。

递归程度，如果是确定性的，可以确定事件之间时间的随机分布。当在不同的 $\theta$ 水平下研究 SN 时（在定义的三角形模式区域，图 2d），事件 ($p$) 显著增加（Faure and Korn, 1998）。这些结果的统计显著性使用回归分析进行评估（生物学统计）。

来自模型和系统的结果支持一种耦合系统的形成可能嵌入在 SN 中。

## 突触网络中的确定性

周期和混沌过程可以由耦合振荡器产生（Borisitsky, 1995），对 SN 的研究可以揭示神经系统中这种机制的存在。SN 的结构特征与观察到的周期一致。

## 讨论

虽然 SN 是稳定的，但表明非线性动力学要求我们关注神经系统的全局动力学，而不是证明混沌（参见 EEG 和 MEG 分析）。SN 的同步表明产生 SN 的耦合振荡器处于活动的起始（例如通过关联增强 SN 中的学习）。

# 突触动力学 1133

图 3. 一系列不同类型的抑制性突触后电位（IPSPs）示意，根据频率标记为 $\square$ 和 $\Delta$。上方和下方的事件分别由实心和空心符号表示。R 为位于中心突触处的发射器。如果一个具有 $n=6$ 个神经元的轴突产生动作电位，其中一些轴突会释放一个量子，概率分别为 $p$ 和 $1-p$。连续脉冲的结果是突触后波动的幅度在平均计数 $n$ 周的 0 到 $n$ 之间波动。C 显示了它们的时间脉冲序列（Syn）以及它们向突触前输入传输的脉冲序列样本。通过 SN 构建的表达与图谱的相关性显示，所有神经元都具有相同的（$D_1$）或不同的（$D_2$）计数。（修改自 Faure 等人，2000）。

![](img/5cb7d541b875c6d6c2092ad1a376440a_1151_0.png)

实验数据对于评估动力学相对于随机模式的行为优势仍然是必要的，并理解混沌动力学如何影响神经功能。

此处特别相关的是非线性整合与高阶动力学之间可能的关系。越来越多的证据表明，神经电序列的可变性（这在感觉处理中可能起着英雄作用）影响的是脉冲序列的精确性，而不是随机的“噪声”。也就是说，大脑通过随机模式被持续驱动，这为更特定的 S 引入了更多信息（Skarda 和 Freeman, 1990；Twodelsky 等人，1999；混沌和，可能在这些自适应过程中起着作用（Tiuda, 2001）。

路线图：生物学神经元与系统

背景：系统中的混沌

相关阅读：系统中的混沌，合成动力学

## 参考文献

Boryk, G. R., Borostik, R. M., Mikhail, A. and Roze, D., 1995. 不同频率类型的耦合神经振荡器的动力学与膨胀。Math. Biol. Sci., 57, 539–540.

Eckmann, J.-P., Kampost, S. and Ruelle, D., 1997. 动力学系统中的短回路的影响。Europhys. Lett., 34, 973–977.

Faure, F., and Roche, M. L., 1998. 从复现图中估计哥尔莫洛熵的新方法。其在神经信号中的应用，Physics D, 122:265–279.

Faure, F., Kaplan, D., and Koh, H., 2000. 突触效率与神经元间复杂发放模式的传输。Neurophysiol., 84:3010–3025.

Fujii, H., Ito., Sugihara, K., Nishimura, T., and Tsukada, M., 1996. 视觉的动态组装：皮层时间编码的层级解释。Nature, 391:1305–1310.

Hatta, K., and Koh, H., 1999. 鱼类逃避反应期间随机对激活的抑制性神经元。Proc. Natl. Acad. Sci. USA., 96:12900–12905.

Koh, H., and Faber, S. F., 1991. 信息传输中的定量分析与突触效率。Science, 253:221–2214.

Perkel, D. B., and Bullock, T. H., 1998. 混沌在神经系统中的作用。Neurosciences, 88(17):5–14.

Schrieber, T., 1999. 非线性时间序列分析的跨学科方法。Cambridge University Press.

Skarda, C. A., and Freeman, W. J., 1990. 混沌和，大脑。

Tiuda, I., 2001. 自适应过程。

Webber, J., 1994. 动力学分析。Am. J. Phys., 76.

# 突触动力学

信息从发送神经元到接收神经元的流动，通过被称为突触释放的奇异过程。神经末的突触。

# 信息

信息从发送神经元到接收神经元的流动，通过被称为突触传输的奇异过程。突触传输的步骤序列是当神经脉冲到达突触时，它导致末端钙浓度的短暂升高，这种升高被

## 第三部分：文章

信息从发送神经元到接收神经元的流动，通过被称为突触传输的奇异过程。突触传输的步骤序列是当神经脉冲到达突触时，它导致末端钙浓度的短暂升高，这种升高被

# 突触强度的变化

信息从发送神经元到接收神经元的流动，通过被称为突触传输的奇异过程。突触传输的步骤序列是当神经脉冲到达突触时，它导致末端钙浓度的短暂升高，这种升高被

# 突触传输的概率性质

# 突触结构

突触的三个部分被识别为：触（连接发送神经元的部分）、突触后密度（连接接收神经元的部分）以及突触间隙（20 纳米的间隙）。

# 突触的变化

信息从发送神经元到接收神经元的流动，通过被称为突触传输的奇异过程。突触传输的步骤序列是当神经脉冲到达突触时，它导致末端钙浓度的短暂升高，这种升高被

# 突触传递

滤波器的基础和计算意义是当前研究的主题。

释放概率的基本关系是：

```
