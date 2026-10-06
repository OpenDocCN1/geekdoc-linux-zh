
`sqrt(mean(true_ratings - predicted_ratings))`

#### 34.7.4 第一个模型

让我们从构建最简单的推荐系统开始：无论用户如何，我们为所有电影预测相同的评分。这个预测应该是多少？一个假设所有电影和用户的评分相同，且所有差异都由随机方差解释的模型看起来像这样：

> $Y_{u,i} = \mu + \varepsilon_{u,i}$

其中 $\varepsilon_{u,i}$ 是从中心为 0 的相同分布中采样的独立误差。

```r
mu_hat <- mean(train_set$rating)

mu_hat

# [1] 3.54
```

如果我们用 $\hat{\mu}$ 预测所有未知评分，我们将得到以下 RMSE：

# 第 34 章 大数据集

```r
naive_rmse <- RMSE(test_set$rating, mu_hat)

naive_rmse
```
# [1] 1.05
```

请记住，如果你输入任何其他数字，得到的 RMSE 都会更高。例如：

```r
predictions <- rep(3, nrow(test_set))
RMSE(test_set$rating, predictions)
```

```
# [1] 1.19
```

从评分的分布来看，我们可以直观地看到该分布的标准差。我们得到的 RMSE 大约是 1.0。为了获得 1,000,000 美元的大奖，参赛团队的 RMSE 必须达到 0.857 左右。所以我们完全做得更好！

在接下来的学习中，我们将比较不同的方法。让我们先用这种朴素的方法创建一个结果表：

```r
rmse_results <- data_frame(method = "Just the average", RMSE = naive_rmse)
```

#### 34.7.5 建模电影效应

我们经验知道，某些电影的评分通常比其他电影高。这种“不同电影评分不同”的直觉被数据证实了。我们可以通过添加项 $b_i$ 来代表电影 $i$ 的平均排名来增强之前的模型：

$$Y_{u,i} = \mu + b_i + \varepsilon_{u,i}$$

统计学教科书将 $bs$ 称为效应（effects）。然而，在 Netflix 挑战赛论文中，他们称为“偏差”（bias），我们称之为 theta。

我们可以再次使用最小二乘法通过以下方式估计 $b_i$：

```r
fit <- lm(rating ~ as.factor(movieID), data = movielens)
```

由于每部电影都有一个 $b_i$，总数有数千个，`lm` 函数在这里运行会非常慢。因此我们不建议运行上面的代码。在这种特定情况下，我们知道估计 $b_i$ 只需要每部电影 $i$ 的 $Y_{u,i} - \hat{\mu}$ 的平均值。因此我们以这种方式计算（在随后的代码中，我们将省略上帽符号以表示估计值）：

```r
mu <- mean(train_set$rating)
movie_avgs <- train_set %>%
  group_by(movieID) %>%
  summarize(b_i = mean(rating - mu))
```

我们可以看到这些估计值差异巨大：

```r
movie_avgs %>% qplot(b_i, geom = "histogram", bins = 10, data = ., color = I("black"))
```

## 34.7. 推荐系统

记住 $\hat{\mu} = 3.5$，因此当 $b_i = 1.5$ 时意味着完美的五星评分。

让我们看看当我们使用 $\hat{\mu}_{u,i} = \hat{\mu} + \hat{b}_i$ 时，我们的预测改进了多少：

```r
predicted_ratings <- mu + test_set %>%
  left_join(movie_avgs, by='movieId') %>%
  pull(b_i)
```

```r
model_1_rmse <- RMSE(predicted_ratings, test_set$rating)
rmse_results <- bind_rows(
    data_frame(method="Movie Effect Model",
    RMSE = model_1_rmse))
```

```r
rmse_results
# A tibble: 2 x 2
# method             RMSE
# <chr>               dbl
# 1 Just the average  1.05
# 2 Movie Effect Model 0.986
```

我们已经看到了改进。我们能让它更好吗？

#### 34.7.6 用户效应

让我们为那些评分超过 100 部电影的用户 $u$ 计算平均评分：

```r
train_set %>%
  group_by(userId) %>%
  summarize(b_u = mean(rating)) %>%
  filter(n()>=100) %>%
  ggplot(aes(b_u)) +
  geom_histogram(bins = 30, color = "black")
```

注意，不同用户之间也存在巨大的差异：有些用户很挑剔，而另一些喜欢每一部电影。这意味着我们模型的进一步改进可能比 5 好。

$$Y_{u,i} = \mu + b_i + b_u + \varepsilon_{u,i}$$

其中 $b_u$ 是用户特定的效应。现在，如果一个挑剔的用户（负的 $b_u$）评价了一部好电影（正的 $b_i$），效应会相互抵消，我们可能可以正确预测该用户给这部电影打 3 分而不是 5 分。

为了拟合这个模型，使用 `as.factor(movieId)` + `as.factor(userId)`，但由于上述的原因，我们不会包含它们。相反，我们将通过计算 $\hat{\mu}$、$\hat{b}_i$ 和 $\hat{b}_u$ 为 $y_{u,i} - \hat{\mu} - \hat{b}_i$ 的平均值来进行近似：

```r
user_avgs <- train_set %>%
  left_join(movie_avgs, by='movieId') %>%
  group_by(userId) %>%
  summarize(b_u = mean(rating - b_i))
```

我们现在可以构建预测器并看看 RMSE 改进了多少：

```r
predicted_ratings <- test_set %>%
  left_join(movie_avgs, by='movieId') %>%
  left_join(user_avgs, by='userId') %>%
  mutate(pred = mu + b_i + b_u) %>%
  pull(pred)
```

```r
model_2_rmse <- RMSE(predicted_ratings, test_set$rating)
rmse_results <- bind_rows(rmse_results,
                          data_frame(method='Movie + User Effects',
                            RMSE = model_2_rmse))
```

```r
rmse_results

# A tibble: 3 x 2

# method             RMSE

# <chr> <dbl>

# 1 ...# ...
```

### 34.8 练习题

- 1. 加载 `movielens` 数据。计算每部电影的评分次数并绘制其年份图。对计数进行平方根变换。
- 2. 我们看到平均而言1993年后的电影评分更多。我们还看到从1993年开始的新电影，评分次数随年份而减少：电影越新，用户评分的时间越少。在1993年或之后出出的电影中，哪些电影评分最多？请报告它们的平均分。
- 3. 从之前的表中可以看出，评分最多的电影往往分较高。这并不意外：人们会看热门电影。为了证实这一点，将1993年的电影按评分分层，并绘制平均评分与年份的趋势图。
- 4. 在之前的例子中，我们看到电影评分越高，分数越高。假设你正在进行预测分析，需要填充缺失评分。你会使用哪些策略？
    - A. 用所有电影的平均值填充缺失值。
    - B. 用 0 填充缺失值。
    - C. 用低于平均值的填充填充评分。尝试上述方法并在测试集上评估。
    - D. 以上均不。
- 5. `movielens` 数据还包含 `timestamp`。该变量表示提供评分的时间。单位是自1970年1月1日的秒数。创建一个日期列。提示：使用 `lubridate` 包中的 `as_datetime` 函数。
- 6. 计算每部电影的平均评分并将其与日期绘制。提示：在 `group_by` 之前使用 `round_date`。
- 7. 图表显示了一些关于时间的证据。如果我们将 $d_{u,i}$ 为用户 $u$ 电影 $i$ 的日期，以下哪个模型是合适的？
    - $Y_{u,i} = \mu + b_i + b_u + d_{u,i}$
    - $Y_{u,i} = \mu + b_i + b_u + d_{u,i}^2 + \varepsilon_{u,i}$
    - $Y_{u,i} = \mu + b_i + b_u + d_{u,i}^3 + \varepsilon_{u,i}$
    - $Y_{u,i} = \mu + b_i + b_u + f(d_{u,i})$，其中 $f$ 是 $d_{u,i}$ 的平滑函数。
- 8. `movielens` 数据还有 `genre` 列。该列包含了适用于电影的所有类型。某些电影属于多个类型。将列中出现的任何组合定义为一个类别。保留评分超过1000次的类别。然后计算每个类别的平均值和标准误差。将这些作为误差棒绘制。
- 9. 图表显示了强烈的类型效应。如果定义 $g_{u,i}$ 为用户 $u$ 电影 $i$ 的类型，以下哪个模型是合适的：
    - $Y_{i} = \mu + b_i + d_{u,i} + \epsilon_{u,i}$
    - $Y_{u,i} = \mu + b_i + d_{u,i}\beta + \epsilon_{u,i}$
    - $Y_{u,i} = \mu + b_i + d_{u,i} + \sum_{k=1}^k x_{u,i}\beta_k$，如果 $g_{u,i}$ 是类型 $k$，则 $x_{u,i}^k=1$。
    - $Y_{u,i} = \mu + b_i + f(d_{u,i}) + \epsilon_{u,i}$，其中 $f$ 是 $d_{u,i}$ 的平滑函数。

## 34.9 正则化

#### 34.9.1 动机

尽管电影之间存在巨大差异，我们的 RMSE 改进仅为5%。让我们探索我们在第一个模型（仅使用电影效应 $b_i$）中哪里犯了错。以下是最大的10个错误：

```r
test_set %>%
  left_join(movie_avgs, by='movieId') %>%
  mutate(residual = rating - (mu + b_i)) %>%
  arrange(abs(residual)) %>%
  select(title, residual) %>% slice(1:10)

# title      residual
# 1 Day of the Beast, (The la Bestia, El) -4.50
# 2 Horror Express -4.00
# 3 No Holds Bared -4.00
# 4 Dear Zachary: A Letter to a Son About His Father -4.00
# 5 Faust -4.00
# 6 Hear My Song -4.00
# 7 Confessions of a Shapaholic -4.00
# 8 Twilight Saga: Breaking Dawn - Part 1, The -4.00
# 9 Tazi Driver -3.81
# 10 Tazi Driver -3.81
```

这些看起来都是电影。许多电影有很大的预测值。让我们根据 $b_i$ 查看表现最好的前10部电影。首先，创建一个连接电影 ID 和电影标题的数据集：

```r
movie_titles <- movielens %>%
  select(movieId, title) %>%
  distinct() %>%
  select(title, b_i) %>%
  slice(1:10)
```

这里是估计我们平均值的最好的10部电影：

```r
movie_avgs <- left_join(movie_titles, by="movieId") %>%
  arrange(b_i) %>%
  select(title, b_i) %>%
  slice(1:10)
```

以及那10个：

## 34. 正则化

```r
movie_avgs %>% left_join(movie_titles, by="movieId") %>%
  arrange(b_i) %>%
  select(title, b_i) %>%
  slice(1:10)
```

# A tibble: 10 × 2
| title | b_i |
| :--- | :--- |
| <chr> | <dbl> |
| 1 Santa with Muscles | -3.04 |
| 2 B*A*P*S | -3.04 |
| 3 Ninjas: High Noon On Mega Mountain | -3.04 |
| 4 Barney's Great Adventure | -3.04 |
| 5 Merry War, A | -3.04 |
| 6 Day of the Beast, The Dia (Dia de Bestia, El) | -3.04 |
| ... with 4 more rows | |

它们看起来都非常冷门。看看它们的评分情况。

```r
train_set %>% count(movieId) %>%
  left_join(movie_avgs) %>%
  left_join(movie_titles, by="movieId") %>%
  arrange(desc(b_i), n) %>%
  select(title, b_i, n) %>%
  slice(1:10)
```

# 连接,by = "movieId"
| title | b_i | n |
| :--- | :--- | :--- |
| <chr> | <dbl> | <int> |
| 1 America | 1.46 | 1 |
| 2 Love & Human Relations | 1.46 | 3 |
| 3 Enfer, L' | 1.46 | 1 |
| 4 Picture Bridge (Bijo photo) | 1.46 | 1 |
| 5 Red Firecracker, Green Firecracker (Pao Da Shua Deng) | 1.46 | 3 |
| 6 Face | 1.46 | 1 |
| ... with 4 more rows | | |

```r
train_set %>% count(movieId) %>%
  left_join(movie_avgs) %>%
  left_join(movie_titles, by="movieId") %>%
  arrange(desc(b_i), n) %>%
  select(title, b_i, n) %>%
  slice(1:10)
```

# 连接,by = "movieId"
| title | b_i | n |
| :--- | :--- | :--- |
| <chr> | <dbl> | <int> |
| 1 Santa with Muscles | -3.04 | 1 |
| 2 B*A*P*S | -3.04 | 1 |
| 3 Ninjas: High Noon On Mega Mountain | -3.04 | 1 |
| 4 Barney's Great Adventure | -3.04 | 1 |
| 5 Merry War, A | -3.04 | 1 |
| 6 Day of the Beast, The Dia (Dia de Bestia, El) | -3.04 | 1 |
| ... with 4 more rows | | |

这些所谓的“最佳”和“最差”电影是由极少数的用户评分的，大多数情况下只有 1 个人。这些电影大多是冷门电影。这是因为当用户很少时，我们的不确定性会更大。因此，$b_i$ 的估计值（无论正还是负）会变得极端。

这些都是我们不应该信任的噪声估计，特别是在涉及到预测时。巨大的误差会推高我们的 RMSE，因此在不确定时我们应该保持保守。

在之前的章节中，我们计算了标准误差并构建了置信区间以考虑不同程度的不确定性。在进行预测时，我们需要一个数字、一个预测，而不是一个区间。为此，我们引入了正则化的概念。

正则允许我们对使用小样本形成的巨大估计值进行惩罚。它与第 17.4 节中收缩预测的贝叶斯方法相似之处。

### 34.9.2 惩罚最小二乘法

正则化的核心思想是限制效应大小的总变异性。为什么这有帮助？考虑一种情况：我们有电影 $i=1$ 有 100 个用户评分，而电影 $i=2,3,4,5$ 只有一个评分。我们打算拟合模型：

```
$Y_{u,i} = \mu + b_i + \varepsilon_{u,i}$
```
