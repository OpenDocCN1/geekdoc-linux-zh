
# 高级 Web 攻击与利用实战

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_0_0.png)

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_1_0.png)

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_2_0.png)

### 4 ATutor LMS 类型混淆漏洞

- 4.1 概述
- 4.2 入门
- 4.3 PHP 松散与严格比较
- 4.4 PHP 字符串转数字
- 4.4.1 练习
- 漏洞发现
- 4.5 攻击松散比较
- 4.6.1 魔法哈希
- 4.6.2 ATutor 与魔法邮箱地址
- 4.6.3 练习
- 4.6.4 进阶
- 4.7 总结

### 5 ManageEngine Applications Manager `AMUserResourcesSynclet` SQL 注入 RCE

- 5.1 概述
- 5.2 入门
- 5.3 漏洞发现
  - 5.3.1 Servlet 映射
  - 5.3.2 源码恢复
  - 5.3.3 源码分析
  - 5.3.4 开启数据库日志
  - 5.3.5 触发漏洞
  - 5.3.6 练习
- 5.4 绕过字符限制
  - 5.4.1 使用 `CHR` 和字符串拼接
  - 5.4.2 它在词法上是合理的
- 5.5 盲注
  - 5.5.1 练习
- 5.6 访问文件系统
  - 5.6.1 练习
  - 5.6.2 通过 `Copy To` 获取反弹 Shell
  - 5.6.3 练习
  - 5.6.4 进阶挑战
- 5.7 `PostgreSQL` 扩展
  - 5.7.1 编译环境
  - 5.7.2 测试扩展
  - 5.7.3 从远程位置加载扩展
  - 5.7.4 练习
- 5.8 UDF 反弹 Shell
  - 5.8.1 练习
- 5.9 更多 Shell
  - 5.9.1 `PostgreSQL` 大对象
  - 5.9.2 大对象反弹 Shell
  - 5.9.3 练习
  - 5.9.4 进阶挑战
- 5.10 总结

## 6 Bassmaster `NodeJS` 任意 `JavaScript` 注入漏洞

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_6_0.png)

- 6.1 概述
- 6.2 入门
- 6.3 Bassmaster 插件
- 6.4 漏洞发现
- 6.5 触发漏洞
- 6.6 获取反弹 Shell
  - 6.6.1 练习
  - 6.6.2 进阶挑战
- 6.7 总结

## 7 `DotNetNuke` Cookie 反序列化 RCE

- 7.1 概述
- 7.2 入门
- 7.3 简介
- 7.4 序列化基础
  - 7.4.1 `XmlSerializer` 的局限性
  - 7.4.2 `XmlSerializer` 示例
  - 7.4.3 练习
  - 7.4.4 扩展 `XmlSerializer` 示例
  - 7.4.5 练习
  - 7.4.6 观察你的类型
  - 7.4.7 练习
- 7.5 `DotNetNuke` 漏洞分析
  - 7.5.1 漏洞概述
  - 7.5.2 调试 `DotNetNuke`
  - 7.5.3 练习
  - 7.5.4 我们是如何变成这样的
- 7.6 载荷选项
  - 7.6.1 `FileSystemUtilsPull` 方法
  - 7.6.2 `ObjectDataProvider` 类
  - 7.6.3 `ObjectDataProvider` 实例使用
  - 7.6.4 练习
  - 7.6.5 `ObjectDataProvider` 的序列化
  - 7.6.6 进入龙穴 (`ExpandedWrapper` 类)
