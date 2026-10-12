
系统安全性有许多维度。整个系统的安全性取决于单个组件的安全性，例如电子邮件、文件、网络、登录和远程访问方法，以及主机本身的物理安全。这些维度经常相互重叠，它们的边界并不是静态或清晰的。例如，电子邮件安全性受到文件和网络安全性的影响。如果你发送和接收电子邮件的介质（网络）是不安全的，那么你必须采取额外步骤来确保消息的安全。

对于位于本地系统文件中的加密电子邮件的安全性，你依赖于文件系统和主机访问策略来确保文件安全。这些领域中的任何一个环节失败都可能引发多米诺骨牌，削弱其他领域的可靠性和完整性，并可能影响整体安全性。

这个简短的附录无法深入涵盖系统安全性的所有方面，但它提供了设置和维护安全系统复杂性的概述。本附录提供了一些具体的细节、概念、需要考虑的指南，以及许多安全资源索引（第 1140 页的表 C-1）。

对于任何不是完全与其他机器和用户隔离的系统来说，安全性都是其基础的重要部分。安全性的某些方面即使在隔离的机器上也有用武。这些措施的示例包括定期的系统备份、BIOS 或开机密码，以及自动锁定屏幕保护程序。

## Other sources of security

Depending on how important security is, you might want to compare algorithms based only on the number of bits. In some cases an algorithm that uses 64-bit can be more secure than an algorithm that uses 128-bit.

加密的主要分类是公钥（非对称）加密和对称（秘密）加密。公钥加密，也称为非对称加密，使用两个密钥：一个公钥和一个私钥。对称加密，也称为对称或秘密加密，使用一个与你通信的人（以下称为朋友）共享的密钥。对称加密通常用于加密大量数据，因为它速度很快。

非对称算法和对称算法互补。非对称算法擅长提供数字签名和身份验证，但速度较慢。对称算法擅长加密大块数据，且速度更快。算法通常结合使用以提供最佳特性：文本首先可以使用对称加密和随机密钥进行处理。然后该密钥可以使用朋友的公钥进行加密（以便朋友读取），并使用你的私钥进行签名（以证明其来自你）。后面的章节将详细介绍这些概念。

当你选择加密方案时，要意识到安全性是有代价的。在安全性和管理易用性之间通常存在权衡。

安全解决方案的实用性是加密中一个更重要的因素，在安全领域也是如此，大多数人意识到通过时间和努力，几乎每个算法都可以被破解。事实上，你可以通过查阅加密书籍

`Asymmetric algorithms use a number of bits. Each bit added to the length effectively doubles the key space.`

# How much time and money should you spend on encryption?

When the cost of obtaining the information exceeds the value realized by its possession, the solution is an effective one.

# PUBLIC KEY (ASYMMETRIC) ENCRYPTION

To use encryption, you must generate two keys: a public key and a private key. You keep the private key for yourself and give the public key to the world. Public key encryption is marked by two distinct features:

## 附录 C 安全

1. 当你使用某人的公钥加密时，只有该人的私钥可以解密。

2. 当你使用私钥加密数据时，任何人都可以用公钥进行解密。

你可能会好奇为什么第二个点很有用：为什么别人能够解密你刚刚加密的内容？答案在于加密的用途。虽然加密将原始消息变为不可读的密文，但其目的是提供数字签名。如果消息可以用你的公钥正确解密，说明你确实用私钥加密过它。这两种模式的结合产生了机密性和真实性。你可以用私钥签名消息以验证真实性，然后用朋友的公钥加密它，这样只有你的朋友才能解密。

公钥加密有三个缺点：

1. 公钥加密算法通常比对称算法慢得多，并且通常需要更大的尺寸以及生成大数的方法，使得它们更消耗资源。

2. 私钥必须安全地存储并保护其完整性。如果他人获得了某人的私钥，他们就可以加密并伪装该消息的所有者。如果私钥丢失或损坏，任何用它加密的消息也随之丢失，并且必须生成新的密钥对。

3. 验证密钥的来源——即所谓的密钥分发问题——是像 `VerSign`（`www.verisign.com`）等公司面临的问题。
