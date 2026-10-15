
# 教程：在 Kali Linux 2022 上安装 Grokevt-elder node 博客

> 原文：<https://blog.eldernode.com/install-grokevt-on-kali-linux/>

![Tutorial-Install-Grokevt-on-Kali-Linux](img/c58d7d5edc5dcf0e733f0a2d6e9a24ff.png)

你很可能遇到过这样的情况：你想从系统中提取信息，并把它转换成一份可理解的报告。`Grokevt` 就是由多个脚本组成的工具之一。在本文中，我们将介绍 `grokevt`，并学习如何在 Kali Linux 上安装它。你可以访问 [Eldernode](https://eldernode.com/) 网站提供的套餐来购买 [**Linux VPS**](https://eldernode.com/linux-vps/) 服务器。

## 如何在 Kali Linux 上安装 Grokevt

### 什么是 Grokevt？

`Grokevt` 是一组安装在一个或多个分区上并协同工作的脚本。这些脚本提取注册表项、消息模式和日志文件等信息，并将报告转换为人类可读的格式。`Grokevt` 在 GNU GPL 许可下发布，并使用 `Python` 实现。

## 在 Kali Linux 上安装 Grokevt

在本篇来自 Kali Linux 培训系列的文章中，我们将回顾在 Kali Linux 上安装 `grokevt` 的 3 种方法。

### 如何使用 `apt-get` 安装 Grokevt

首先，**使用以下命令更新 APT 数据库**：

```
sudo apt-get update
```

然后，**使用下面的命令安装 grokevt**：

```
sudo apt-get -y install grokevt
```

### 如何使用 `apt` 安装 Grokevt

首先，运行以下命令**更新 APT 数据库**：

```
sudo apt update
```

然后，使用下面的命令**安装 grokevt**：

```
sudo apt -y install grokevt
```

### 如何使用 `aptitude` 安装 Grokevt

要使用 `aptitude` 安装 `grokevt`，需要先在 Kali Linux 上安装 `aptitude`。然后，**用下面的命令更新 Apt 数据库**：

```
sudo aptitude update
```

现在，你可以用下面的命令安装 `grokevt`：

```
sudo aptitude -y install grokevt
```

### 如何使用 Grokevt 的不同工具

1. **`Grokevt-addlog`**：运行以下命令，使用此工具将原始事件日志添加到现有的 `grokevt` 数据库中：

```
grokevt-addlog -h
```

2. **`Grokevt-builddb`**：运行以下命令，在 Windows 系统上构建一个数据库树，以转换事件日志：

```
grokevt-builddb -h
```

3. **`Grokevt-ripdll`**：使用此工具从 PE 格式文件中提取消息源；为此，请使用以下命令：

```
grokevt-ripdll -h
```

4. **`Grokevt-dumpmsgs`**：使用此实用程序，转储之前由 `grokevt-ripdll` 创建的消息数据库的内容；为此，运行以下命令：

```
man grokevt-dumpmsgs
```

5. **`Grokevt-findlogs`**：运行以下命令，在原始二进制文件中查找日志文件片段，如内存转储和磁盘映像：

```
grokevt-findlogs --help
```

6. **`Grokevt-parselog`**：你可以解析 Windows 事件日志，并根据数据库中存储的消息源生成可读的输出。使用下面的命令：

```
grokevt-parselog -h
```

## 常见问题解答

[sp _ easy agreement]

## 结论

在本文中，我们介绍了 `Grokevt`——一组安装在一个或多个分区上并协同工作的脚本——并学习了如何在 Kali Linux 上安装它。我们还回顾了 `grokevt` 的不同工具以及如何使用它们。
