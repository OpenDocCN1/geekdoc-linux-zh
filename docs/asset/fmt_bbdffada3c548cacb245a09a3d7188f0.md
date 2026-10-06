
假设我们知道平均评分是 $\mu = \mu$。如果使用最小二乘法，第一部电影的 $b_i$ 估计值为 $\hat{b}_i = \bar{Y}_{.,i} - \mu$，我们期望它是相当精确的。然而，对于估计 2, 3, 4 和 5，这仅仅是基于一个评分得出的与平均评分的偏差 $\hat{b}_i = \bar{Y}_{.,i} - \mu$，因此它完全不精确。这些估计使得 $i=2,3,4,5$ 的误差 $Y_{u,i} - \mu$ 接近 0。事实上，忽略用户并假设 2, 3, 4 和 5 是平均电影（$b_i=0$）可能会提供更好的预测。惩罚回归的总想法是控制电影效应的总变异：$\sum_{i}^p b_i^2$。具体来说，我们不是最小化最小二乘方程，而是最小化一个加上惩罚项的方程：

```
$\frac{1}{N} \sum_{u=1}^N (Y_{u,i} - \mu - b_i)^2 + \lambda \sum_{i=1}^p b_i^2$
```

第一项是最小二乘，第二项是惩罚项，当 $b_i$ 很大时惩罚会增大。利用微积分，我们可以证明该方程最小化的 $b_i$ 值：

```
$\hat{b}_i(\lambda) = \frac{1}{\lambda + n_i} \sum_{u=1}^{n_i} (Y_{u,i} - \mu)$
```

其中 $n_i$ 是电影 $i$ 的评分数量。这种方法将产生我们想要的效果：当样本量 $n_i$ 非常大时（这会给我们一个稳定的估计），惩罚 $\lambda$ 实际上被忽略了，因为 $\lambda \approx n_i$。当 $n_i$ 较小时，估计值 $\hat{b}_i(\lambda)$ 会向 0 收缩。$\lambda$ 越大，收缩越厉害。让我们使用 $\lambda=3$ 计算这些正则化的 $b_i$ 估计值。稍后我们将看到为什么选择 3。

```r
lambda <- 3

mu <- mean(train_set$rating)

movie_avgs <- train_set %>%
  group_by(movieID) %>%
  summarize(b_i = sum(rating - mu)/n(), n_i = n())
```

为了看到估计值是如何收缩的，我们将绘制正则化估计值与最小二乘估计值的对比图。

```r
data.frame(original = movie_avgs$b_i,
           regularized = movie_reg_avgs$b_i,
           n = movie_avgs$n) %>%
  ggplot(aes(original, regularized, size=sqrt(n))) +
  geom_point(shape=1, alpha=0.5)
```

现在，让我们看看基于惩罚估计 $b_i(\lambda)$ 的前 10 部电影：

```r
train_set %>%
  count(movieID) %>%
  left_join(movie_avgs, by = "movieID") %>%
  left_join(movie_titles, by="movieID") %>%
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

假设我们知道平均评分是 $\mu = \mu$。如果使用最小二乘法，第一部电影的 $b_i$ 估计值为 $\hat{b}_i = \bar{Y}_{.,i} - \mu$，我们期望它是相当精确的。然而，对于估计 2, 3, 4 和 5，这仅仅是基于一个评分得出的与平均评分的偏差 $\hat{b}_i = \bar{Y}_{.,i} - \mu$，因此它完全不精确。这些估计使得 $i=2,3,4,5$ 的误差 $Y_{u,i} - \mu$ 接近 0。事实上，忽略用户并假设 2, 3, 4 和 5 是平均电影（$b_i=0$）可能会提供更好的预测。惩罚回归的总想法是控制电影效应的总变异：$\sum_{i}^p b_i^2$。具体来说，我们不是最小化最小二乘方程，而是最小化一个加上惩罚项的方程：

```
$\frac{1}{N} \sum_{u=1}^N (Y_{u,i} - \mu - b_i)^2 + \lambda \sum_{i=1}^p b_i^2$
```

第一项是最小二乘，第二项是惩罚项，当 $b_i$ 很大时惩罚会增大。利用微积分，我们可以证明该方程最小化的 $b_i$ 值：

```
$\hat{b}_i(\lambda) = \frac{1}{\lambda + n_i} \sum_{u=1}^{n_i} (Y_{u,i} - \mu)$
```

其中 $n_i$ 是电影 $i$ 的评分数量。这种方法将产生我们想要的效果：当样本量 $n_i$ 非常大时（这会给我们一个稳定的估计），惩罚 $\lambda$ 实际上被忽略了，因为 $\lambda \approx n_i$。当 $n_i$ 较小时，估计值 $\hat{b}_i(\lambda)$ 会向 0 收缩。$\lambda$ 越大，收缩越厉害。让我们使用 $\lambda=3$ 计算这些正则化的 $b_i$ 估计值。稍后我们将看到为什么选择 3。

```r
lambda <- 3

mu <- mean(train_set$rating)

movie_avgs <- train_set %>%
  group_by(movieID) %>%
  summarize(b_i = sum(rating - mu)/n(), n_i = n())
```

为了看到估计值是如何收缩的，我们将绘制正则化估计值与最小二乘估计值的对比图。

```r
data.frame(original = movie_avgs$b_i,
           regularized = movie_reg_avgs$b_i,
           n = movie_avgs$n) %>%
  ggplot(aes(original, regularized, size=sqrt(n))) +
  geom_point(shape=1, alpha=0.5)
```

现在，让我们看看基于惩罚估计 $b_i(\lambda)$ 的前 10 部电影：

```r
train_set %>%
  count(movieID) %>%
  left_join(movie_avgs, by = "movieID") %>%
  left_join(movie_titles, by="movieID") %>%
  arrange(desc(b_i), n) %>%
  select(title, b_i, n) %>%
  slice(1:10)
```

# A tibble: 10 × 3
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
train_set %>% count(movieID) %>%
  left_join(movie_avgs) %>%
  left_join(movie_titles, by="movieID") %>%
  arrange(desc(b_i), n) %>%
  select(title, b_i, n) %>%
  slice(1:10)
```

# A tibble: 10 × 3
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

假设我们知道平均评分是 $\mu = \mu$。如果使用最小二乘法，第一部电影的 $b_i$ 估计值为 $\hat{b}_i = \bar{Y}_{.,i} - \mu$，我们期望它是相当精确的。然而，对于估计 2, 3, 4 和 5，这仅仅是基于一个评分得出的与平均评分的偏差 $\hat{b}_i = \bar{Y}_{.,i} - \mu$，因此它完全不精确。这些估计使得 $i=2,3,4,5$ 的误差 $Y_{u,i} - \mu$ 接近 0。事实上，忽略用户并假设 2, 3, 4 和 5 是平均电影（$b_i=0$）可能会提供更好的预测。惩罚回归的总想法是控制电影效应的总变异：$\sum_{i}^p b_i^2$。具体来说，我们不是最小化最小二乘方程，而是最小化一个加上惩罚项的方程：

```
$\frac{1}{N} \sum_{u=1}^N (Y_{u,i} - \mu - b_i)^2 + \lambda \sum_{i=1}^p b_i^2$
```

第一项是最小二乘，第二项是惩罚项，当 $b_i$ 很大时惩罚会增大。利用微积分，我们可以证明该方程最小化的 $b_i$ 值：

```
$\hat{b}_i(\lambda) = \frac{1}{\lambda + n_i} \sum_{u=1}^{n_i} (Y_{u,i} - \mu)$
```

其中 $n_i$ 是电影 $i$ 的评分数量。这种方法将产生我们想要的效果：当样本量 $n_i$ 非常大时（这会给我们一个稳定的估计），惩罚 $\lambda$ 实际上被忽略了，因为 $\lambda \approx n_i$。当 $n_i$ 较小时，估计值 $\hat{b}_i(\lambda)$ 会向 0 收缩。$\lambda$ 越大，收缩越厉害。让我们使用 $\lambda=3$ 计算这些正则化的 $b_i$ 估计值。稍后我们将看到为什么选择 3。

```r
lambda <- 3

mu <- mean(train_set$rating)

movie_avgs <- train_set %>%
  group_by(movieID) %>%
  summarize(b_i = sum(rating - mu)/n(), n_i = n())
```

为了看到估计值是如何收缩的，我们将绘制正则化估计值与最小二乘估计值的对比图。

```r
data.frame(original = movie_avgs$b_i,
           regularized = movie_reg_avgs$b_i,
           n = movie_avgs$n) %>%
  ggplot(aes(original, regularized, size=sqrt(n))) +
  geom_point(shape=1, alpha=0.5)
```

现在，让我们看看基于惩罚估计 $b_i(\lambda)$ 的前 10 部电影：

```r
train_set %>%
  count(movieID) %>%
  left_join(movie_avgs, by = "movieID") %>%
  left_join(movie_titles, by="movieID") %>%
  arrange(desc(b_i), n) %>%
  select(title, b_i, n) %>%
  slice(1:10)
```
