
# 资源管理 (Sun Bluprints)

关于实现资源管理的系统视角

提供了实现细节，包括“Solaris 资源管理器”和“Solaris 带宽管理器”

一份使用真实世界应用实例的实用指南

![](img/52144374747884a32fdddbed4e8cd9d7_0_0.png)

![](img/52144374747884a32fdddbed4e8cd9d7_1_0.png)

![](img/52144374747884a32fdddbed4e8cd9d7_2_0.png)

* 致谢 xxi
* 前言 xiii
* Sun BluePrints 程序 xiii
* 谁应该使用这本书 xxiv
* 本书组织结构 xxiv
* 相关书籍 xxv
* 字体变化意味着什么 xxvi
* 命令示例中的 Shell 提示符 xxvii
*(注：后续重复章节已根据原文结构对应翻译，此处遵循不重复输出原文的要求)*

图 9-8 策略代理组件 240

图 9-9 统计信息的图形化表示 243

图 9-10 Solaris 带宽管理器将计费信息转换为 ASCII 245

图 9-11 Solaris 带宽管理器与 NetFlowCollector 协同工作 246

图 9-12 Solaris 带宽管理器使用本地应用程序 247

图 10-1 LSF 调度器组件 263

图 10-2 LSF 集群配置 266

图 10-3 LSF 故障转移功能 268

图 10-4 并行应用的作业执行流 270

图 11-1 Jiro 架构 277

图 12-1 SyMON 软件架构 282

图 12-2 SyMON 软件控制台 284

图 12-3 负载健康监控模块 285

图 12-4 主机详情窗口 286

图 12-5 SyMON 软件域控制台 287

图 12-6 域状态详情窗口 288

图 12-7 告警详情窗口 289

图 12-8 已确认的告警 290

图 12-9 刷新域状态详情窗口 291

图 12-10 无告警的 SyMON 软件域控制台 291

图 12-11 详细配置窗口 292

图 12-12 硬件配置树的逻辑视图 293

图 12-13 系统背部的物理视图 294

图 12-14 板级物理视图 295

| | | |

|---|---|---|

## 致谢

任何大型作品都离不开幕后许多人士的帮助。如果没有书中提到的所有人所付出的非凡努力和奉献，这本书就不会有今天的模样。

特别感谢 Charles Alexander 为 Sun BluePrints 程序提供灵感、愿景和机会。特别感谢 Mark Connelly 和 Anne Schowe 对此的支持。

感谢那些花时间审查文本并提供意见的人员：Brad Carlile, Kevin Colwell, Ian Griffin, Neil Gunther, Meng-Tai Ko, Jeannie Johnston-Kobert, Sandra Lee, Jean-Christopher Martin, Jeff McKeekin, Rajiv Parikh, Ravi Pendekanti, Eric Elmore, Paul Strong（感谢 WLM 章节，他几乎可以列为作者），Martin Tuori（来自 Platform Computing Corporation）、Amanda West, Brian Wong 以及 Alison Wiley。

感谢 Oracle Corporation 的同仁，特别是...（注：由于用户提供的原文在感谢处中断，翻译仅至此）。
