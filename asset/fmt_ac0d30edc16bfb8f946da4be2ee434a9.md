
现在软件包到达一家想要部署该软件包的公司。在检查软件包上的每个签名后，它知道这是一份真实的副本，自创建以来未作任何更改。根据部署公司的内部控制，它可能会选择添加自己的签名，从而让员安心该软件包已获公司认可。

在这段冗长的例子之后，`--addsign`选项的实际输出有点平淡无奇：

```bash
# rpm --addsign blather-7.9-1.1386.rpm
Enter pass phrase: <passphrase> (Not echoed)
Pass phrase is good.
blather-7.9-1.1386.rpm:
```

如果我们检查该软件包的签名，我们将能看到多个签名：

```bash
# rpm --checksig blather-7.9-1.1386.rpm
blather-7.9-1.1386.rpm: size pgp pgp md5 OK
```

`--checksig`输出中的两个`pgps`清楚地表明该软件包已被签名两次。

### 17.3.1. 一些注意事项

与`--resign`选项一样，`--addsign`选项无法在3版本之前的软件包文件上施展魔法：

```bash
# rpm --addsign blah.rpm
Enter pass phrase: <passphrase> (Not echoed)
Pass phrase is good.
blah.rpm:
blah.rpm: Can’t re-sign v2.0 RPM
```

好吧，错误信息可能并不100%准确，但你明白意思了。另一件需要注意的事情是`--addsign`选项不会检查多个相同的签名。尽管这样做没多大意义，但RPM会愉快地让你添加相同签名任意多次：

```bash
# rpm --addsign blather-7.9-1.1386.rpm
Enter pass phrase: <passphrase> (Not echoed)
Pass phrase is good.
blather-7.9-1.1386.rpm:

# rpm --addsign blather-7.9-1.1386.rpm
Enter pass phrase: <passphrase> (Not echoed)
Pass phrase is good.
blather-7.9-1.1386.rpm:

# rpm --addsign blather-7.9-1.1386.rpm
Enter pass phrase: <passphrase> (Not echoed)
Pass phrase is good.
blather-7.9-1.1386.rpm:

# rpm --addsign blather-7.9-1.1386.rpm
Enter pass phrase: <passphrase> (Not echoed)
Pass phrase is good.
blather-7.9-1.1386.rpm:

# rpm --checksig blather-7.9-1.1386.rpm
blather-7.9-1.1386.rpm: size pgp pgp pgp pgp md5 OK
```

从`--checksig`的输出中可以看到，该软件包现在有四个相同的签名。也许这是数字时代用力过猛签名的等效行为。

![](img/5ceb645f91e0f928013c644127692ba8_268_0.png)

![](img/5ceb645f91e0f928013c644127692ba8_268_1.png)

![](img/5ceb645f91e0f928013c644127692ba8_268_2.png)

在本章中，我们将探索RPM的一个更有趣的功能：创建子软件包的能力。

### 18.1. 什么是子软件包？

简单来说，*子软件包*是由单个spec文件创建的多个软件包文件之一。RPM能够创建一个主软件包，以及一个或多个子软件包。子软件包也可以在没有主软件包的情况下创建。这完全取决于软件包构建者的选择。

### 18.2. 为什么需要子软件包？

如果世界上所有的软件都遵循通常的“一个源代码，一个二进制文件”结构，那么就不需要子软件包了。毕竟，RPM完全能够处理将程序构建和打包到单个软件包文件中。

但软件并不总是符合这种简单的结构。软件支持两种或多种不同的操作模式是很常见的。例如，客户端/服务器程序有两种形式：客户端和服务器。

而且情况可能比这更复杂。有时软件完全依赖另一个程序，以至于两者无法单独构建。结果往往会产生几个软件包。

虽然肯定可以想出一些复杂的方法来强制将这些类型的软件放入单软件包结构中，但让RPM管理子软件包的创建更合理。为什么？从软件包构建者的角度来看，使用子软件包的主要原因是消除任何重复劳动。

使用子软件包时，无需维护单独的spec文件，也无需忍受新版本软件出现时带来的头痛问题。通过将所有内容保留在一个spec文件中，可以快速集成新的软件版本，并且可以用一条命令重新构建所有相关的子软件包。

但前置说明就到此为止。让我们看看子软件包是如何创建的。

### 18.3. 我们的示例Spec文件：满满的子软件包！

在本章中，我们将构建一个包含多个子软件包的spec文件。让我们首先列出spec文件的需求：

- 主软件包名称为`foo`。
- 版本为`2.7`。
- 有三个子软件包：
    - 名为`foo-server`的服务器子软件包
    - 名为`foo-client`的客户端子软件包
    - 名为`bazlib`的baz开发库子软件包
- `bazlib`子软件包的版本为`5.6`。
- 每个子软件包将拥有自己的`summary`和`description`标签。

每个spec文件都以前导部分开始。在这种情况下，前导部分将包含以下标签：

```spec
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
Copyright: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junkie
%description
This is the long description of the foo app, and the baz library needed to
build it...
```

如你所见，这里没有不同：目前这是一个普通的spec文件。让我们深入探讨一下，看看我们需要向这个spec文件添加什么才能创建我们需要的子软件包。

### 18.4. 用于子软件包的Spec文件更改

子软件包的创建严格基于spec文件的内容。但这并不意味着你需要学习整套新的标签、条件语句和指令才能创建子软件包。事实上，你只需要学习一个。

对spec文件的主要更改是结构性的，始于为每个子软件包定义前导部分。

#### 18.4.1. 子软件包的前导部分

当我们在第10章“RPM开发基础”中介绍RPM软件包构建时，我们说过每个spec文件都包含一个前导部分。前导部分包含各种标签，定义关于软件包的多种信息。在单软件包情况下，前导部分必须位于spec文件的开头。我们要创建的spec文件也会在那里有一个前导部分。

当你创建一个将构建子软件包的spec文件时，每个子软件包也需要自己的前导部分。这些子前导部分只需在信息与主前导部分定义的信息不同之处定义子软件包的信息。例如，如果我们想为子软件包定义安装前缀，我们会将该子软件包的前导部分中添加适当的前缀标签。这样，该子软件包将是可重新定位的。

在单包规格文件中，除了其位于文件顶部的位置外，没有任何明确标识导言部分的内容。然而，对于子包，我们需要更加明确一些。因此，我们使用`%package`指令来标识每个子包的导言部分。

##### 18.4.1.1. `%package`指令

`%package`指令实际上执行两个功能。如上所述，它用于表示子包导言部分的开始。它还在形成子包名称方面发挥作用。例如，假设主导言部分包含以下`name`标签：

```
name: foo
```

在规格文件的稍后部分，有一个`%package`指令：

```
%package bar
```

这将导致子包的名称为`foo-bar`。

通过这种方式，可以轻松地看出子包与主包（或其他子包）之间的关系。当然，这种命名约定可能并不适用于所有情况。因此，针对这种情况，`%package`指令有一个选项。

##### 18.4.1.2. 在`%package`指令中添加`-n`

`-n`选项用于将子包的最终名称从*主包-子包*更改为*子包*。让我们修改之前示例中的`%package`指令，使其变为：

```
%package -n bar
```

结果是子包的名称将是`bar`，而不是`foo-bar`。

##### 18.4.1.3. 更新我们的规格文件

让我们将新学到的知识应用到我们要编写的规格文件中。以下是我们需要创建子包的列表：
