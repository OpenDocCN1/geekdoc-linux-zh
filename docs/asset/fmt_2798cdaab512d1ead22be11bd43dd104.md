
另一方面，存在常数 `$c$`，对于 `$L$` 的任何 PAC 学习，充分样本大小 `$m(d, \epsilon, \delta)$` 最多为 `$c(d + \log(\delta^{-1}))/\epsilon$`，对于所有 `$\epsilon \leq 1$` 和 `$\delta \leq 1$`。

在以上，定理 2 适用于 `[0,1]` 值函数，而不仅仅是神经网络。

正如 `$RP \neq NP$` 猜想。对于固定的 `$k$`，对于每个 `$n$`，`$\mathcal{P}_k^n$` 是连接到 `$k$` 个阈值单元的神经网络，每个单元有 `$n$` 个输入，这些阈值的输出通过一个 `$k$` 与门组合，当且仅当所有 `$k$` 个阈值单元都输出 1 时，网络输出 1。Baum 和 Bartlett 证明了以下结论（参见 Allison and Beng, 1992）。

**定理 5.** `$\mathcal{P}_k^n$` 如上所述，其中 `$k=2$`。如果存在对于 `$\mathcal{P}_k^n$` 在准确性、大小和输入数量方面高效的 PAC 学习算法，那么 `$RP \neq NP$` 猜想不成立。

因此，对于此类简单的神经网络类，不太存在高效的 PAC 学习算法。

本节的目的是定义什么是神经网络学习，并证明某些学习类是难以区分的。我们展示了一个“负性”结果：然而，高效的神经网络学习并没有限制。感知机存在高效算法，对于更复杂的网络（即网络输出不是输入的线性函数），也存在许多高效学习的例子，但都是以直接的方式给。例如，参见 Anthony 和 Bartlett (1999) 的第 26 章，关于学习某些具有线性阈值单元和线性单元输出的二层神经网络的高效算法。

## 路线图：可计算性与复杂度
相关阅读：学习与泛化：理论界限；神经网络的 VC 维度

## 参考文献
- Anthony, M., and Bartlett, P. L., (1999). *Neural Network Theory: Theoretical Foundations*. Cambridge: Cambridge University Press.
- Anthony, M., and Bartlett, P. L., (2002). *Computational Learning*. Cambridge: Cambridge University Press.
- Baum, E. A., and Haussler, D., (1989). What size do we need to generalize? In *Proceedings of the 1989 Conference on Machine Learning*, San Francisco, CA, pp. 9–18.
- Blum, A., and Rival, R. L., (1988). A 3-layer neural network in NP complexity, in *Proceedings of the 1988 Workshop on Computational Learning*, San Francisco, CA, pp. 39–48.
- Neumeier, U. (1972). *Science*, 177(4022), 517.
- Blumer, A., Haussler, D., and Warmuth, M. K., (1989). VC-dimension of binary classifiers. *Journal of the Machine Learning Society*, 6:965–978.
- Cores, J. H., Ehrenfeucht, U., and Bartlett, R. L., (1990). *Introduction to Computational Learning: PAC Learning*. Cambridge, MA: MIT Press.
- Rudyker, C., (1997). Critical learning theory for empirical measures, *Ann. Statist.*, 25(6), 2089–2092.
- Shalev, N., Kearns, M., and Valiant, L., (1989). A general lower bound on the number of examples needed for learning. *Journal of Computer and System Sciences*, 4:1–28.
- Goding, J., and Petrov, M., (1993). Bounding the Vapnik-Chervonenkis dimension of complex classes by real numbers, in *Proceedings of the 11th International Conference on Pattern Recognition*, New York: ACM, pp. 359–360.
- Se, J., and Petrov, M., (1995). Bounding the Vapnik-Chervonenkis dimension of polynomial networks by rational networks, *Journal of Machine Learning Research*, 8(1):131–148.
- Gruss, B., (1997). *Statistical complexity of generating examples of the PAC model for neural net and other efficient learning*. *Comput. Inform.*, 6:107–114.
- Karpinski, M., and Macintyre, A. J., (1995). Polynomial bounds for VC dimension of sigmoid neural networks, in *Proceedings of the 37th Annual Annual Symposium on Foundations of Computer Science*, New York: ACM, pp. 208–208.
- Valiant, L. G., (1984). A theory of the learnable, ACM, 27:1134–1142.
- Vapnik, V. N., and Chervonenkis, A. Ya., (1971). On the uniform convergence of frequencies to their probabilities, *Theory Prob Prob.*, 16:253–280.

## 讨论
我们考虑了应用于人工网络学习的基础 PAC 学习。我们讨论了两个不同的方面：训练样本的长度和学习的效率。在我们的语言中，我们处理了样本复杂度问题和计算复杂度。神经网络的 Vapnik-Chervonenkis 维度详细地定义了 PAC 中的样本复杂度。

## 感觉刺激编码
感觉信号的第一步是编码质量和位置。感觉感受器是初级神经（传入神经），其细胞体位于神经根（DRG）。每个神经根都有一根终止于肌肉、内脏等的轴突，以及一根在神经根中旅行并在脊髓中结束的中央轴突。

## 疼痛网络
通过感觉神经传入。神经冲动从受体、背根（DR）出发，无障碍地进入中枢神经系统（CNS）。该细胞经过特殊设计，会产生脉冲。鉴于背根神经节（DRG）中没有突触，它没有理由为这种脉冲转换末端。

## 上行通路与细胞表征
教科书对上行躯感觉通路的描述通常代表感受野，脊髓丘脑束（用于疼痛和振动的前侧系统，以及用于触摸和振动的后柱内侧系统）通过腹侧丘脑中继并终于初级感觉皮层。

## 中枢汇聚
感觉感受器阵列（于皮肤）中的空间信息是通过初级传入轴在脊髓上的拓扑（体体）映射表示的。感觉强度的编码更为复杂。

## 调制与闸控机制

## 外周神经敏化
感觉调制源于近期的经历。例如，在皮肤中，疼痛损伤导致外周敏化，即炎症可以增加皮肤、肌肉、关节等处痛觉转导过程的增益（敏感性），从而对以前无反应的刺激产生反应。

## 中枢系统的调制
1965年，Melzack 和 Wall 提出了第一个疼痛闸控理论。

## 下行抑制
中脑导水管灰质（图1中的 PAG）作为痛觉控制的节点，大脑通过此上传痛觉信息。

![img/5cb7d541b875c6d2092ad1a37440a864_0.png](img/5cb7d541b875c6d2092ad1a37440a864_0.png)

## 中枢敏化
脊髓疼痛/闸多年年来发生了变化，这一概念通过对 CNS 调制的丰富见解得到了巩，形成了新综合的基础。

## 神经性疼痛
重新审视疼痛经典想法的最动力来自于对慢性患者的观察，特别是源于损伤的脊髓和根。

## 神经病理/异位
理解神经性疼痛的关键是意识到神经并不像电缆。

# 第 847 页
尽管许多不同区域的皮层神经会对有害刺激产生反应，但体感觉皮层也会激活（Puron, Layrent, and Garcia-Larra, 2000）。

# 观点
疼痛，持续性疼痛对于第一现场观察者来说仍然是一个医学健康问题：治疗疼痛的尝试毫无进展，这在很大程度上是因为传统医学的治疗失败。

**图 3.** 正常刺激下的刺激诱导和激活，以及神经损伤时的静电现象，揭示了细胞体和轴端膜属性的调节。

## 路线图：感觉系统
- 相关诱发；机制；体感觉系统；
- 体感觉：感觉系统的可塑性

## 疼痛在哪里？
我在这篇文章的开头讨论了慢性大脑由有害刺激引起的不愉快经历。

## 过去时

### 引言
过去时是一个看似简单的语言现象，它模仿了理性主义者和经验主义者之间几个世纪争论中的最新辩论。

## 过去式 840
关于月份中的规则，通常引用两个主要的观察结果。第一是，儿童经常将该规则应用到他们从未听过的单词上。

## 过去式
认为不规则反射显示了底层规则运作的观点是由 Rumhart 和 McDonnell (1996) 的里程碑式连接主义模型提出的。

## 屈折形式的频率
规则和不规则区别的一种方式是屈折形式的频率如何影响它们的处理。

## 神经系统损伤与成像
规则和不规则区别的一种方式是屈折形式的频率如何影响它们的处理。

## 参考文献
- Berko, J., 1958. 儿童对英语形态形态的学习。Word, 14:150–177.
- Chomsky, N., 1999. B. F. Skinner《言语行为》评论。Language, 35:1.
- Pinker, S., 1999. 语言的先天能力（第1版）。纽约：Basic Books.

## 讨论
关于规则屈折过程的活跃认知解释大多数认为，不规则形式的心理表征并非被排除，而是运作得像一个连接主义模型。

## 路线图：语言学与语音处理
相关阅读：连接主义与符号表征；对语法大脑的影响；语言处理：心理语言学

## James D Murray

## 引言
生物空间模式的产生对许多学科都至关重要。

## 生物学模式形成
LFFeBook

## 852 第三部分：文章

| 图 | 描述 |
| :--- | :--- |
| A | 蝴蝶翅膀上观察到的各种空间模式的小样本 |
| B | 多细胞藻（Dictyostel discoideum）的移动和静止带 |
| C | 贝卢索夫-季廷斯基反应中的圆形和螺旋波 |
| D | 条纹 |
| E | 模式 |

## 模式形成，生物学
在本文中，我们讨论了……

## 第三部分：文章

![](img/5cb7d541b875c6d6c2092ad1a376440a_872_0.png)

> 图 2。某些相互作用表现出扩散驱动的不稳定性。在部分 A 中，自激活的 B 抑制了两种物种。产生的空间模式在部分 C 中示意性地给出。

（见 Murray, 2002, 第 II 卷）。方程 5 表明图灵不稳定性可以在宽的尺度上发生。对于足够大的 `$\delta$`，条件 `$\delta f_u - g_v + 2\sqrt{\delta f_u g_v \dots} > 0$` 满足。

数学分析还可以为边界尺寸和形状对模式形成的影响提供见解。

在图灵的形态学理论中，发育概念是化学扩散允许细胞产生不同的反应并形成空间模式。这些化学物质被称为形态发生素（morphogenesis）。

我们量化灰质和白质中胶质母瘤差异运动性的基本数学模型为：

```
```
