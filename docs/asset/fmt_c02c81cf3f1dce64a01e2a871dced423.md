
`S -> NP VP`

`NP -> (det) N`

`VP -> V (NP)`

使用这些规则来定义词法和短语成分：
`[The] [is fully a chair]`

为了捕捉人类语言的完全通用性，需要向规则中引入递归。我们可以通过一条向 NP 添加潜在短语的新规则，将递归纳入上述规则中：

```
NP -> det(NP)

NP -> prep
```

这些规则是递归的，因为每个规则右侧的扩展可以包含对自身的调用。例如，上述规则集中的 NP 递归地嵌入了简单的 NP VP。这个过程可以很容易地应用，例如，创建一个包含三个嵌入式 NP 的 NP：

```
NP -> The is in the chair

NP -> on the table

NP -> the window
```
