

客户满意和 IT 员工满意的要求有一些共同因素。然而，有些事情似乎是正交的，甚至直接冲突。老板必须确保所有这些不同的期望能够兼容且可实现。

SLA 有助于使终端用户和支持人员保持一致。写得好的 SLA 解决了以下各节讨论的每一个问题。

## 服务范围和描述

本节是 SLA 的基础，因为它描述了组织可以从 IT 部门期望的内容。它应该用非技术人员能够理解的术语来写。一些示例服务可能是

- Email
- Internet and web access
- File servers
- Business applications
- Printing

IT 在提供这些服务时将遵守的标准也必须定义。例如，可用性部分将定义运营时间、商定的维护窗口，以及 IT 员工提供现场支持的可用时间预期。一个组织可能会决定常规支持应在工作日上午 8:00 至下午 6:00 提供，但紧急支持必须 24/7 可用。另一个组织可能会决定需要全天候的标准现场支持。

以下是记录标准时需要考虑的问题清单：

- Response time
- Service (and response times) during weekends and off-hours
- House calls (support for machines at home)
- Weird (unique or proprietary) hardware
- Upgrade policy (ancient hardware, software, etc.)
- Supported operating systems
- Standard configurations
- Expiration of backup tapes
- Special-purpose software
- Janitorial chores (cleaning screens and keyboards, vacuuming grilles)

在考虑服务标准时，请记住，如果软件没有被钉死以防止这种情况，许多用户会想要自定义他们的环境（甚至系统）。典型的 IT 反应是禁止所有用户修改，但尽管这种政策让 IT 更容易，但不一定是对组织最好的政策。

在您的 SLA 中解决这个问题，并尝试标准化为几种特定的配置。否则，您关于易于维护和随组织增长而扩展的目标将会遇到严重的阻碍。鼓励您那些富有创造力、喜欢折腾操作系统的员工提出他们工作中需要的修改，并勤勉且慷慨地将这些建议纳入您的标准配置中。如果您不这样做，您的用户会努力规避您的规则。

## 队列管理政策

除了知道提供哪些服务外，用户还必须了解用于管理工作队列的优先级方案。优先级方案总是有一些弹性，但请尝试设计一个能够覆盖大多数情况且例外很少或没有的方案。下面列出了一些与优先级相关的变量：

- The importance of the service to the overall organization
- The security impact of the situation (has there been a breach?)
- The service level the customer has paid or contracted for
- The number of users affected
- The importance of any relevant deadline
- The loudness of the affected users (squeaky wheels)
- The importance of the affected users (this is a tricky one, but let’s be honest: some people in your organization have more pull than others)

尽管所有这些因素都会影响您的排名，但我们建议采用一套简单的规则，再加上一些常识来处理例外情况。基本上，我们使用以下优先级：

- Many people cannot work
- One person cannot work
- Requests for improvements

如果两个或多个请求具有最高优先级且请求无法并行处理，我们根据问题的严重程度来决定先处理哪个问题（例如，电子邮件无法使用会让几乎所有人不满意，而 Web 服务暂时不可用可能只会妨碍少数人）。较低优先级的队列通常以先进先出方式处理。

用户通常认为他们所有的重要数据都存储在将永久归档的备份磁带上。但备份介质不会无限期保存；特别是磁性介质有有限的使用寿命，之后读取数据会变得困难。 （如果您想长期保存数据，则必须定期重写数据，可能转移到更新的介质上。）备份磁带也可能被传票调取，因此您的组织可能不希望旧数据永远可用。与负责此类决策的人员合作制定书面协议，规定备份必须保存多长时间，是否需要制作多个副本（必需？允许？绝不？），以及这些副本必须存储在哪里，这最好。

