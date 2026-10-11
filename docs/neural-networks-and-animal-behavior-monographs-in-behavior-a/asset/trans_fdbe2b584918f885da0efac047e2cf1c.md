

![](img/4e7230a4ecf676d308ca85f3d2e65bae_70_0.png)

图 2.14 用于自组织模拟的网络架构。输入节点排列在一个二维网格中，模拟视网膜上受体的物理排列。

视网膜，并且后续的处理阶段可以利用这些信息来执行诸如定位物体或在环境中定向等任务。

如何产生一个覆盖整个视网膜的接收野网络？仅仅添加彼此独立操作的输出节点是不够的。事实上，图 2.16（左）表明大多数节点发展出非常相似的接收野（这意味着输入序列是权重组织的强决定因素）。如果在呈现输入之后、更新权重之前，我们将除了最活跃节点以外的所有节点的活动设置为零，我们会获得更好的结果。从生物学角度来讲，这可能对应于神经元之间强烈的相互抑制。以这种方式获得的接收野在视网膜上分布得更加均匀，如图 2.16（右）所示。为了理解原因，仅考虑两个节点，并假设由于初始权重的差异，节点 1 对输入 **x** 的反应比节点 2 更强。那么，根据方程 (2.52)，节点 1 对 **x** 和类似输入的敏感性将增加，而节点 2（其活动已被设为零）对相同输入的敏感性将降低。这种权重的变化使得节点 1 对类似于 **x** 的输入比节点 2 更活跃的可能性更大。总之，我们有一个自我强化的过程（正反馈），它赋予两个节点对不同输入模式的敏感性。

## 2.5 使用自己的模型

希望使用神经网络研究动物行为的学者可以选择多种软件工具，其中许多工具在 Hayes 等人（2003）以及 [http://www.faqs.org/faqs/ai-faq/neural-nets/part5](http://www.faqs.org/faqs/ai-faq/neural-nets/part5) 中进行了综述。然而，这类软件的重点往往不是动物行为。在这里我们为初学者提供了一些指南。我们将软件广泛分为神经网络模拟器、通用编程语言和科学计算软件。

![](img/4e7230a4ecf676d308ca85f3d2e65bae_71_0.png)

**图 2.15** 使用方程 (2.52) 和图 2.14 中的网络进行模拟（输入网格为 $100 \times 100$ 个节点）。从左到右：刺激样本使输入网格的一部分节点兴奋；初始权重配置；权重的三种组织形式，对应于方程 (2.52) 中参数 $b$ 的三种选择，且 $\eta=5, a=0.05$。从左到右：兴奋中心和抑制边缘，兴奋和抑制半球，抑制中心和兴奋边缘。模拟由 1000 次呈现类似于图中所示的随机放置在模型视网膜上的刺激组成。每次呈现后，方程 (2.52) 被应用于所有权重。较浅的灰色代表较强的权重；负权重比刺激样本中最深的灰色更暗。

![](img/4e7230a4ecf676d308ca85f3d2e65bae_71_1.png)

**图 2.16** 由方程 (2.52)（其中 $a=0.5$ 且 $b=0.05$）在两个不同网络中诱导出的权重组织。左：在类似图 2.14 的网络中发展的接收野，但该网络有 16 个独立的输出节点（每次呈现输入时所有权重都独立更新）。右：在相似网络中发展的接收野，但 16 个输出节点之间有强抑制（仅更新馈送到最活跃节点的权重）。在后一种情况下，接收野分布得更加均匀。

```C
#include <stdio.h>  /* these two lines are needed to use */
#include <math.h>  /* functions printf() and exp(); see below*/

/* this function calculates node input, see equation (2.3) */
/* W = weight vector, x = input vector, n = size of W and x */
float weighted_sum( float *W, float *x, int n ) {
   int i;
   float y= 0.;
   for( i=0; i<n; i++ )  y += W[i]*x[i];
   return y;
}

/* logistic node transfer function, see equation (2.7) */
float transfer_function( float y ) {
   return 1/(1+exp(-y));
}

/* a C program starts executing from the “main” function */
int main( void ) {
   float x[] = { 1, 1, 1, 1};  /* input vector */
   float W[] = { 1, 0, 1, 0 };  /* weight vector */
   float y;             /* input to output node */
   float z;             /* activity of output node */
   y = weighted_sum( W, x, 4 );    /* calculate y */
   z = transfer_function( y );      /* apply the transfer function */
   printf( “Output is %f\n”, z );  /* print result */
   return 0;            /* end of the program */
}
```

列表 2.1 一个模拟具有 N = 4 个输入节点和 1 个输出节点的两层网络的 C 程序。数字表示为 *float* 类型的变量，向量表示为此类变量的数组。*int* 类型的变量表示整数（例如，向量索引）。表达式 x[i] 是数组 x 的第 *i* 个元素（C 索引从 0 开始）。函数 weighted_sum 和 transfer_function 分别将方程 (2.3) 和方程 (2.7) 翻译出来，并提供模拟两层网络的基本结构。解释性注释包裹在 /* 和 */ 之间。

神经网络模拟器是即用型程序，通常具有图形用户界面，专门用于研究神经网络。一些最发达的模拟器旨在进行神经生理学上逼真的模拟（Hayes 等人 2003 及其中的参考文献）。它们倾向于考虑神经元的许多细节，结果导致具有许多状态变量和参数的节点模型，而这些目前对行为建模的价值尚不确定（参见 2.1.2.2 节末尾）。神经网络模拟器也在人工智能、计算机科学和工程领域得到开发。此类软件的缺点是，它通常需要一些技术背景，并且倾向于关注与动物行为不同的问题。两个相当通用的神经网络模拟器，虽然需要一些学习，但对于初学者来说并不太难，且不需要编程，分别是 PDP++ ([http://psych.colorado.edu/~orcelli/PDP++/PDP++/PDP++.html](http://psych.colorado.edu/~orcelli/PDP++/PDP++/PDP++.html)) 和 JavaNNS ([http://www-ra.informatik.uni-tuebingen.de/software/JavaNNS/welcome.html](http://www-ra.informatik.uni-tuebingen.de/software/JavaNNS/welcome.html))。前者专注于（人类）认知，包括行为层面的现象（O'Reilly & Munakata 2000），而后者对网络模型的解读则更为中立。

使用通用编程语言（如 Pascal、C、C++ 等）而不使用特定软件进行神经网络研究也是可能的。这些语言本身不具备神经网络的知识，但简单的神经网络模拟可以容易地实现。例如，要模拟一个具有一个输出节点的两层网络，只需要两个数字数组来存储输入和权重向量，一个数字用于响应，以及计算加权和并定义传递函数的能力。作为一个例子，列表 2.1 展示了一个完整的 C 程序，它计算具有单个输出节点和权重 **W** = (1, 0, 1, 0) 的两层网络对输入 **x** = (1, 1, 1, 1) 的输出。该程序在大多数其他编程语言中看起来不会太大差别。人们还开发了语言的扩展，称为 *库*，使得用少量工作就能编程更复杂的模拟。通常，这些库提供数据结构来表示各种网络架构，以及执行常见任务的能力，如计算网络响应或梯度下降学习。对于有一定编程经验或希望开始编程的读者来说，探索这些语言扩展可能是有益回报的。许多神经网络库列在 [http://www.faqs.org/faqs/ai-faq/neural-nets/part5](http://www.faqs.org/faqs/ai-faq/neural-nets/part5)。

科学计算软件非常适合希望使用相当直接的编程语言模拟简单或中等复杂网络的初学者。关键见解是，神经网络的运算可以用向量和矩阵代数来表示，而这有着广泛的支持。下面我们在 Octave（[http://www.octave.org](http://www.octave.org)，免费提供）和 Matlab（[http://www.mathworks.com](http://www.mathworks.com)）程序常用的语法中呈现了一些例子。类似的软件，尽管编程语法不同，包括 Scilab（[http://www.scilab.org](http://www.scilab.org)，免费提供）和 Mathematica（[http://www.wolfram.com](http://www.wolfram.com)）。后续章节中的许多模型只需要比以下例子稍多的编程，我们鼓励读者尝试复现我们的部分结果。我们并不期望没有编程经验的读者理解以下代码的每一行，而是希望他们能对使用科学软件进行神经网络编码有一个大致的了解。

### 2.5.1 两层前馈网络

在科学软件中，简单的神经网络编码相当紧凑。例如，以下代码与列表 2.1 等效：

```
function r = f( y )
    r = 1 ./ (1+exp(-y)); % cf. equation (2.7)
end

x = [ 0 1 0 1];        % input vector
W = [ 1 1 1 1];        % weight vector
r = f( W*x )          % cf. equation (2.17)
```

注意最后一行如何几乎逐字地翻译方程 (2.17)，其中 $\hat{W} * \hat{x}$ 等同于加权和的记法 **W** · **x**。按照惯例，如果相应的行*没有*以分号结尾，则计算结果会被打印出来；因此上述代码将显示 $r$ 的值，即 $r = 0.88080$。

