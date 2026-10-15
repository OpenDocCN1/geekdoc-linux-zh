
`tab_2 <- mutate(tab_1, rate = total / population * 10^5)`

`rates <- tab_2$rate`

# [1] 3

我们可以通过直接输入代码来定义任何新对象：

```r

filter(states, region == "South") %>%

  mutate(rate = total / population * 10^5) %>%

  summarize(median = median(rate)) %>%

pull(median)

# [1] 3

```

我们之所以这样做是因为这些函数中的每一个都接受数据框作为其第一个参数。但如果 `pull` 函数不可用，且我们想要访问数据框的某个组件，该用什么呢？例如，使用 `pull` 函数获取 `rate` 向量，我们可以使用点操作符：

```r

filter(states, region == "South") %>%

  mutate(rate = total / population * 10^5) %>%

.$rate

median(rates)

# [1] 3

```

在下一节中，我们将看到 `.` 有用的其他实例。

## 5.12 do

`tidyverse` 函数知道如何解释分组后的 `tibble`。此外，为了方便通过管道符 `%>%` 执行命令，`tidyverse` 函数一致地返回数据框，因为这确保了上一个函数的输出可以作为另一个函数的输入。大多数 R 函数既不识别分组后的 `tibble`，也不返回数据框。`quantile` 函数就是我们在 5.7 节中描述过的一个例子。在 5.7 节中我们注意到，如果我们尝试用 `quantile` 在一行内获取最小值、中位数最大值，将会收到一个错误：期望长度为 1 的结果，得到了 2。

```r

heights %>%

  filter(sex == "Female") %>%

  summarize(range = quantile(height, c(0.5)))

```

我们可以使用 `do` 函数来修复这个问题。首先，我们必须编写一个符合 `tidyverse` 方法的函数：它接收一个数据框并返回一个数据框。

```r

my_summary <- function(dat) {

  x <- quantile(dat, c(0.5, 1))

  data.frame(min = x[1], median = x[2], max = x[3])

}

```

现在我们将该函数应用到 `heights` 数据集以获取摘要：

```r

heights %>%

  group_by(sex) %>%

  do(my_summary())

# A tibble: 1 x 3

# min median max

# <dbl> <dbl> <dbl>

# 1 ... ...

```

但这不是我们想要的。我们想要为每个性别得到一个摘要，而代码只返回了一个摘要。这是因为 `my_summary` 不是 `tidyverse` 的一部分，它不知道如何处理分组后的 `tibble`。为了建立这种连接：

```r

heights %>%

  group_by(sex) %>%

  do(my_summary())

# A tibble: 2 x 4

# Groups: sex

#  min median max

#  <fct> <dbl> <dbl>

#  1 Female 51.0 79

#  2 Male 50.6 82.7

```

注意，我们需要使用点操作符。`group_by` 创建的 `tibble` 被传递到点之后。在对点的调用中，该 `tibble` 的名称是 `dat`，我们希望将其赋值给参数。如果不使用点，那么 `my_summary` 就没有参数并返回一个错误，告诉我们缺少参数 "`dat`"。

```r

heights %>%

  group_by(sex) %>%

  do(my_summary())

```

如果你没有括号，函数将不会执行，而是尝试返回函数本身。这会导致错误，因为 `do` 必须始终返回数据框。

```r

heights %>%

  group_by(sex) %>%

  do(my_summary)

```

## 5.13 purrr 包

在 4.5 节中，我们学习了 `sapply` 函数。如果我们想对向量的每个元素应用 `sapply` 来获取一个结果，我们构建了如下函数：

```r

my_n <- function(n) {

  x <- 1:n

  sum(x)

}

```

并使用 `sapply` 来计算 `n` 的和：

```r

n <- 1:25

sapply(n, my_n)

```

`purrr` 包包含了类似于 `sapply` 的函数。这种操作（将相同的函数应用到对象的每个元素）在数据分析中是非常常见的。`purrr` 的优势在于我们可以控制输出类型。相比之下，`sapply` 可能会产生不同的类型。`map_dbl` 总是返回向量：

```r

library(purrr)

map_dbl(n, my_n)

```

`map` 函数对于字符串非常有用：它返回列表。例如，如果我们映射字符串，可以使用 `map_chr`：

```r

map_chr(c("a", "b", "c"), nchar)

```

## 5.14 条件判断

`case_when` 函数用于根据现有变量定义分类变量。例如，假设我们想测量英格兰地区、西部海岸、南部和其他地区的速率。这里是使用使用 `case_when` 来实现这一点：

```r

heights %>%

  mutate(group = case_when(

    abb %in% c("ME","NH","VT","CT") ~ "New England",

    abb %in% c("WA","OR") ~ "West Coast",

    region == "South" ~ "South",

    TRUE ~ "other"

  )) %>%

  group_by(group) %>%

  summarize(rate = sum(total) / sum(population) * 10^5) %>%

  arrange(rate)

# A tibble: 4 x 2

# group         rate

# <chr>         dbl

# 1 New England  1.72

# 2 other        2.71

# 3 West Coast   2.90

# 4 South        3.63

```

### 5.14.2 between

数据分析中的一个常见操作是判断值是否在某个范围内。我们可以使用条件判断进行检查。例如，检查向量 `x` 的元素是否在 `a` 和 `b` 之间，我们可以输入 `x >= a & x < b`。但这在 `tidyverse` 方法中可能非常繁琐。`between` 函数执行相同的功能：

```r

between(x, a, b)

```

## 5.15 练习

1. 加载 `murders` 数据集。哪项是正确的？
   - A. `murders` 是 `tidy` 格式并存储在 `tibble` 中。
   - B. `murders` 不是 `tidy` 格式并存储在数据框中。
   - C. `murders` 不是 `tidy` 格式并存储在 `tibble` 中。
   - D. `murders` 不是 `tidy` 格式并存储在数据框中。
2. 使用 `as_tibble` 将 `murders` 数据表转换为 `tibble` 并保存到名为 `murders_tibble` 的对象中。
3. 使用 `group_by` 代码编写与以下代码等：`exp(log(murders$population))`。使用管道符使得每个函数调用时不带参数。提示：使用点操作符访问 `population`。
4. 使用 `map_df` 创建一个包含 `n`、`s_n` 和 `s_n_2` 三列的数据框。第一列应包含 1 到 100 的数字。第二列和第三列应分别包含 1 到 `n` 的和，其中 `n` 为行号。

## 第 6 章

### 导入数据

我们已经使用了已经存储为 R 对象的数据集。数据科学家很少有这种幸运，他们将不得不从文件、数据库或其他源将数据导入 R 中。目前，存储和共享数据分析结果的最常用方法之一是通过电子电子表格。电子表格以行和列的形式存储数据。它本质上是数据框（`data frame`）的文件版本。在将此类表格保存到计算机文件时，需要一种方法来定义新行或新列何时结束、另一行或另一列何时开始。这种定义定义了存储单个数值的单元格。

当使用文本文件创建电子表格时，新行通过换行符定义，列与列之间通过某些预定义的字符分隔。最常见的字符是逗号（`,`）、分号（`;`）、制表符（`tab`）或预设数量的空格。

第一行包含名称而非数据。这被称为表头（`header`），当我们从电子表格中读取数据时，知道文件是否包含表头很重要。读取函数假设存在表头。要确定文件是否有表头，在查看文件之前先观察它是很有帮助的。

# [3] "murders.csv"
# [4] "olive.csv"
# [5] "RD-Mortality-Report_2015-18-180531.pdf"

`system.file` 函数允许我们提供子目录作为第一个参数，因此我们可以这样获取 `extdata` 目录的完整路径：
`dir <- system.file("extdata", package = "dslabs")`

`file.path` 函数用于组合目录名，以生成我们要导入的文件的完整路径。
`fullpath <- file.path(dir, filename)`

### 6.1.5 复制文件

我们用于将文件复制主目录的最后一行代码使用了 `file.copy` 函数。该函数的参数是：要复制的文件以及在新目录中给它指定的名字。
`file.copy(fullpath, "murders.csv")`
# [1] TRUE

如果文件复制成功，`file.copy` 函数将返回 `TRUE`。注意，我们提供了文件名 `murders.csv`，但也可以将其命名为任何名称。同时请注意，字符串不以斜杠开头意味着这是一个相对路径，并将文件复制到当前工作目录。
你你应该能够在工作目录中看到该文件，并使用以下命令进行检查：
`list.files()`

## 6.2 readr 和 readxl 包

在本节中，我们将介绍 `tidyverse` 中主要的导入导入函数。我们将使用由 `dslabs` 包提供的 `murders.csv` 文件作为示例。为了方便说明，我们将使用以下代码将文件复制到工作目录：

```r

filename <- "murders.csv"

dir <- system.file("extdata", package = "dslabs")

fullpath <- file.path(dir, filename)

file.copy(fullpath, "murders.csv")
```
