
```c
int main(int argc, char **argv) {
    if (argc != 2) {
        printf("Wrong number of arguments. Exiting...\n");
        return -1;
    }

    int n = atoi(argv[1]);
    int i = 0;

    // Read /dev/random
    int afile = open("/dev/random", O_RDONLY);
    unsigned short mySeed;
    uint16_t myRead = read(afile, &mySeed, sizeof(mySeed));
    printf("seed used: %u\n", mySeed);
    close(afile);
}

for (int i=0; i<n; i++) {
    printf("%d ,\n", rand());
}
```

我们的随机生成器实现 `genNumBetter` 使用 `/dev/random` 随机生成器可以产生的值范围。显而易见，随机生成器最重要的属性是初始化整个过程的特殊种子。

种子不需要是随机的，通常由系统属性共享。一个选择糟糕或容易被猜测的系统可以弥补你想要使用的随机生成器值的缺陷，这在 `rand(3)` 函数的实现中占据了主导地位。大问题是：“`genNumberC` 是一个好的生成器吗？”答案是否定的，因为虽然 `rand(3)` 看起来像是一个随机生成器，但它的设计初衷是为了产生完全不随机的值！

在下一节将使用一种更好的方法，作为生成你的第一个随机字符串的基础。

## 创建随机数

## 创建随机字符串

本节将尝试通过下载并读取 `genNumC` 源码来学习如何生成随机数，这是随机生成器的第一种方法，`genNumC` 使用了产生低质量随机生成器的 `rand()` 函数。例如：它会产生以下输出：

这部分将展示如何使用随机数创建随机字符串，因为随机字符串是基于随机数的。程序的作用是生成一个包含 ASCII 字符的字符串，这意味着每个生成的数字值必须在 33（空格字符）和 126（即 `~`）之间。

由于可能值的数量为 $126-31$（即 95），每个生成的整数都必须使用模运算符进行处理。你必须将整数转换为所需的 ASCII 字符如下：

```
$/genNumber 2
16807
2875249
$/genNumber 3
16807
2875249
162650287
$/genNumber 4
16807
2875249
162650287
98493658
```

```
char c = rand() % 95 + ASCIICHARS + 1;
```

接下来，打开并读取 `genString.c`。正如你在 `genString` 中看到的，生成的字符串的字符数量将通过 `genString.c` 的命令行参数传递。再次，使用相同参数的 `genString.c` 将生成相同的“随机”字符串。

数字 4 是将要打印的随机整数的计数。它的问题在于，如果你一直执行它，你可能一直得到相同的“随机”数字序列！这主要要求：

## 随机生成教程

## Python 中的随机数

Python 有一个用于生成随机数的模块。如果你查看该模块的文档，你会发现它非常小。它的输出看起来如下：

```
$ python random.py
71 38 25 43 31 57
86 77 18 76 43 19
4 25 55 96 72 38
```

正如你所理解的，Python 每次执行脚本时会自动使用不同的种子。问题是，在不知道种子的情况下，你无法复制相同的序列。

请记住，密码越长越好。换句话说，通过数字生成的较短密码比长密码差。这是因为更长的密码会产生更多的数字。这主要是因为你可以

## 改进技术

`rand(3)` 函数的大问题是：“`genNumberC` 是一个好的生成器吗？”答案是否定的，因为虽然 `rand(3)` 看起来像是一个随机生成器，但它的设计初衷是为了产生完全不随机的值！

## 获取更好的结果

`rand(3)` 函数的大问题是：“`genNumberC` 是一个好的生成器吗？”答案是否定的，因为虽然 `rand(3)` 看起来像是一个随机生成器，但它的设计初衷是为了产生完全不随机的值！

# 教程

`rand(3)` 函数的大问题是：“`genNumberC` 是一个好的生成器吗？”答案是否定的，因为虽然 `rand(3)` 看起来像是一个随机生成器，但它的设计初衷是为了产生完全不随机的值！

# 星号

# #define 33

#define ASCICHARS 94

```c
int main(int argc, char **argv) {
    if (argc != 2) {
        printf("Wrong number of arguments. Exiting...\n");
        return -1;
    }

    int n = atoi(argv[1]);
    int i = 0;

    // Read /dev/random
    int afile = open("/dev/random", O_RDONLY);
    unsigned short mySeed;
    uint16_t myRead = read(afile, &mySeed, sizeof(mySeed));
    printf("seed used: %u\n", mySeed);
    close(afile);
}

for (int i=0; i<n; i++) {
    printf("%d ,\n", rand());
}
```

# 随机数生成教程

基于：

`getPassword`,

`breakPass` 展示了

暴力破解

密码破解器

```c
int main(int argc, char **argv) {
    // Password length
    int n = 0;
    int i, j;
    char myPass[n+1];
    int mySeed = (unsigned)time(NULL);
    printf("Seed: %u\n", mySeed);
    srand(mySeed);
    for (i = 0; i < n; i++) {
        myPass[i] = FROM + rand() % ASCIICHAR + 1;
    }
    myPass[n] = 0;
    printf("Password: %s\n", myPass);

    // 睡眠 5 分钟
    sleep(5);
    int currentEpoch = (unsigned)time(NULL);
    printf("Current epoch time: %u\n", currentEpoch);
    char tempPass[n+1];
    // 尝试通过回溯猜测种子。
    for (i = currentEpoch; i >= mySeed; i--) {
        for (j = 0; j < n; j++) {
        }
    }
}
```

## Swift 中的 randomswift

既然 Apple 已经将 Swift 项目开源，你就可以使用 Swift 作为命令行界面语言。来看看 `randomswift` 的源码。`randomswift` 输出的输出类似于：

- `randomswift:hash`

`896570532 286557538 464532981 203257990`

`199102717 127609419 141358962 212398464`

`147081815 614368917`

如你所见，你可以使用 `generator.c` 中的相同方法将 `randomswift` 的输出转换为字符串。

请注意，C 代码允许你使用现有的 C 代码函数——这种情况下需要调用 `random()` 函数。

```c
if (numArgs != 1) {
    printf("Please provide one command line argument\n");
    exit(1);
}
my $chars = $ARGV[0];
for (i = 0; i < $chars; i++) {
    printf("%c", i + (rand()%MAX));
}
printf("\n");
exit 0;
```

在 `genPer3.c` 之前。再次，生成的密码长度必须作为命令行参数传递给脚本。`randomPer3.pl` 运行三次的部分产生以下输出：

```bash
./randomPer3.pl 10
*S601-SF77
*X15,EH4
*E14!:ZZX
```

输出看起来非常随机且难以猜测，这意味着 `randomPer3.pl` 工作得很好。

```perl
#!/usr/bin/perl
use Math::Random::Secure qw(rand);
use strict;
my $i = 0;
my $MAX = 95;
my $OFFSET = 32;
my $numArgs = $ARGV[0] + 1;
```

在你研究中有一点提醒，你可能会在网上读到关于 `Math::Random::True` 模块的内容。该模块已不再维护，且无法工作，否则你将浪费时间尝试使用它。有些脚本语言可以帮助你轻松地完成工作，所以不要低估脚本语言的力量，特别是在解决相对较小的项目时。

## Rust 中的随机数

Rust 是另一种现代且功能强大的编程语言，它防止许多常见错误，一方面，它保证了安全性。我们实现的 Rust 代码显示生成八位字符随机数的代码如下：

```rust
extern crate rand;
use rand::{thread_rng, Rng};
fn main() {
    let mut rng = thread_rng();
    for _ in 0..10 {
        let n: u32 = rng.gen_range(0..100);
        println!("{}", n);
    }
}
```

教程中的 `random` 文件夹包含了我们实现的各种文件，显示了 Rust 方法以及如何使用 `cargo`，你将在教程中学习。

Rust 的一个优点是不需要调用函数来设置种子，它提供了一种生成范围的方法，必须产生：

## 使用 R 生成随机数

原因是 R 在这里是一个数学和编程语言，它允许你比预期更容易地完成许多事情。之一是它允许你生成属于特定分布的随机数；这非常有帮助！另一点是生成你需要的任意随机数序列。

要在 R 中生成相同的随机数序列，你应该使用相同值的 `seed()` 函数。以下代码说明了：

- `set.seed(123, min=0, max=10)`

- `runif(103, 0.28759, 0.83071, 0.89779, .83014, .04673)`

- `runif(45565, 0.52189, 0.89219, .54150, .46617)`

- `set.seed(123)`

- `runif(100, min=0, max=10)`

- `runif(28759, 0.831,1, .8979, .83011, .04673)`

- `runif(100, min=0, max=10)`

- `runif(45565, 0.52189, 89299, 54140, 46617)`

当 `runif` 函数继续生成数字时，如果你使用相同的种子运行命令，函数将开始生成相同的随机数序列！下一个命令从均值为 10、标准差为 20 的正态分布生成 10000 个随机数：

```r
mySample <- rnorm(10000, 10, 20)
```

同样易用，R 可以轻松地绘制你的数据并让你对样本有更好的理解。同样，下一个命令创建 100 个属于均值为 10 的泊松分布随机数：

```r
mySample <- rpois(100, 10)
```

R 可以直观地创建各种数据，同样易用，可以轻松绘制数据并让你理解样本。

## 你能轻易破解密码吗？

通过暴力破解法，这意味着程序生成各种种子。`BreakPass` 做了两个假设：首先，你知道原始密码。这是破解密码的实际方法；通过尝试猜测可能需要多年。

检查 `break.pass` 的源码，它是 `genPassword` 的 C 代码。程序在开始前使用循环生成需要的数据；如果你更改种子的值，将必须编译程序才能生效。输出显示破解大约五分钟前生成的密码所花费的时间：

```bash
$ time ./breakPass
real 15.979s
user 0.001s
sys 0.002s
```

由于结果包含了 `sleep` 的延迟，你可以看到速度几乎是瞬时的。输出显示了 `breakPass` 回溯 15 分钟破解密码所花费的时间：

```bash
$ time ./breakPass
real 14.5979s
user 0.001s
sys 0.002s
```

如你所见，过程非常快。因此，在不修改的情况下使用它是非常糟糕的主意，对于你自己的密码应该避免这样做。

# With Aster

`www.lux.com`

# 探索内部技术

`www.gadgetdaily.xyz`

# Gadget

热售中

- 2016 技术预览

- 顶级厨房套件

- 游戏设备

- 最酷设备拆解

购买建议

科学解释

操作指南

# 今日购买你的杂志

纸质版可在 `www.imagineshop.couk` 购买

数字版可在 `www.greatdigitalmags.com` 购买

# 程序员与制作者的必备指南

# 实用型树莓派

“我们将带你了解 Raspberry Pi Zero、所需的电缆、如何准备 NOOBS SD 卡以及如何焊接 GPIO 引脚”

# 目录

- 60 使用 Python 开发

- 68 LED 驱动的像素球体

- 70 使用你的 Pi 监控音频

- 72 设置你的 Pi Zero

- 76 制作 Pi Zero 可穿戴技术

# 特色

# 使用 Python 开发

Python 受全球 Web 开发者、学术研究人员和工程师的依赖。以下是如何将你的 Python 技能用于专业用途

# 系统管理

利用 Python 充分处理所有保持系统健康的日常维护

## 特

## WEB 开发

Python 提供了几个框架可用于你的 Web 开发任务。我们将查看其中一些流行的框架。

通过将内容和日期托管在服务器上，Web 应用程序可以为终端用户提供一致的体验。流行的 Django 框架提供了一个完整的插件环境，并遵循 DRY 原则（不要重复自己）。正因如此，你应该能够快速构建你的 Web 应用程序。使用 Django，你可以通过 `sudo pip django` 来安装它。根据你对应用想要的操作，你可能需要安装 MySQL 或 PostgreSQL 来存储你的应用程序数据。然后 Django 将自动为你的新项目生成一个起点。

```bash
django-admin startproject website
```

此命令创建了一个名为 "manage.py" 的文件和一个名为 "website" 的子目录。"manage.py" 文件包含几个实用函数，你可以使用这些函数来管理你的新应用程序。新的子目录包含文件 `__init__.py`、"settings.py"、"urls.py" 和 "views.py"。这些文件会在你的服务器启动时被加载。你网站的配置可以在 "settings.py" 中找到。URL 路由存储在 "urls.py" 中。"views.py" 文件包含了与 WSGI 兼容的 Web 入口。

一旦你的应用程序完成，它应该托管在一个适当加固的 Web 服务器上。但如果你正在开发 Web 应用程序的过程中，这并不麻烦。为了帮助你，Django 框架中内置了一个 Web 服务器。你可以通过切换目录到“新项目”目录并运行此命令来启动它：

```bash
python manage.py runserver
```

这将启动一个在你的本地机器上监听 8000 端口的服务器。由于这个内置服务器是为开发设计的，它会为每个请求重新加载你的 Python 代码，因此你不需要重启服务器就能看到你的更改。

所有这些步骤都让你开始运行一个项目。你现在位于 "website" 子目录中，输入：

- `python manage.py startapp webapp`

这将创建一个新的子目录 "webapp"，其中包含 `models.py`、"views.py" 和其他文件。最简单的视图由以下代码组成：

```python
from django.http import HttpResponse
def index(request):
    return HttpResponse("Hello world")
```

然而，这还不足让它运行起来。你还需要为它创建一个 URL。如果 "urls.py" 文件不存在，请使用以下代码创建它：

```python
from django.urls import url
urlpatterns = [ url('', views.index, name='index') ]
```

接下来，使用以下代码在你的项目中注册 URL：

```python
from django.urls import path, include
from django.contrib.admin import admin
urlpatterns = [ path('admin/', admin.site.urls), include('webapp/urls.py') ]
```

这需要位于主项目的路径中。你现在可以使用 URL http://localhost:8000/webapp/ 运行你新创建的应用程序。

上述 Python 解释器与数据库配合以支持 Web 服务器

模型-视图-控制器（MVC）架构被我们使用。

## 虚拟环境
