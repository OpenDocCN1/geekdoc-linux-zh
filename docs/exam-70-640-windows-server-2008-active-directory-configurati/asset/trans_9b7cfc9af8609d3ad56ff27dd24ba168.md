
安装 Windows Server 2008 后，如果不重新安装，则无法更改其版本。

## 如何在不激活的情况下安装 Windows Server 2008

- 运行 Windows Server 2008 安装程序。
- 当提示输入产品密钥以激活时，请勿输入密钥。当安装程序询问是否确认您的选择时，单击“否”。
- 系统可能会提示您选择要评估的 Windows Server 2008 版本。请选择您要安装的版本。
- 当出现提示时，请阅读 Microsoft 软件许可条款中的评估条款，然后接受这些条款。
- 当 Windows Server 2008 安装程序完成后，您的初始 60 天评估期即开始。要检查当前评估期剩余的时间，请运行 System32 文件夹中的 Slmgr.vbs 脚本。使用 -dl 开关运行此脚本。slmgr.vbs -dl 命令会显示当前 60 天评估期剩余的天数。

## 如何重置评估期

本节介绍如何延长（或重新设置）Windows Server 2008 的评估期。评估期也被称为“激活宽限期”。

当初始的 60 天评估期接近尾声时，您可以运行 Slmgr.vbs 脚本来重置评估期。要执行此操作，请按照以下步骤操作：

1. 单击**开始**，然后单击**命令提示符**。
2. 输入 `slmgr.vbs -dl`，然后按 **ENTER** 键以检查当前评估期的状态。
3. 要重置评估期，请输入 `slmgr.vbs -rearm`，然后按 **ENTER** 键。
4. 重启计算机。

这将重置评估期为 60 天。

## 如何自动化评估期的延长

您可能希望设置一个流程，自动每 60 天重置一次评估期。自动化此流程的一种方法是使用任务计划程序。您可以配置任务计划程序在特定时间运行 Slmgr.vbs 脚本并重启服务器。要执行此操作，请按照以下步骤操作：

1. 单击**开始**，指向**管理工具**，然后单击**任务计划程序**。
2. 将以下示例任务复制到服务器，然后将其保存为 .xml 文件。例如，您可以将该文件保存为 `Extend.xml`。

```xml
<xml version="1.0" encoding="UTF-16"?>
<Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
  <RegistrationInfo>
    <Date>2007-09-17T14:26:04.433</Date>
    <Author>Microsoft Corporation</Author>
  </RegistrationInfo>
  <Triggers>
    <TimeTrigger id="18c4a453-d7aa-4647-916b-af0c3eal6a6b">
      <Repetition>
        <Interval>PT90d</Interval>
        <StopAtDurationEnd>false</StopAtDurationEnd>
      </Repetition>
      <StartBoundary>2007-10-05T02:23:24</StartBoundary>
      <EndBoundary>2008-09-17T14:23:24.777</EndBoundary>
    </TimeTrigger>
  </Triggers>
  <Principals>
    <Principal id="Author">
      <UserId>domain\alias</UserId>
      <LogonType>Password</LogonType>
      <RunLevel>HighestAvailable</RunLevel>
    </Principal>
  </Principals>
  <Settings>
    <IdleSettings>
      <Duration>PT10M</Duration>
      <WaitTimeout>PT1H</WaitTimeout>
      <StopOnIdleEnd>true</StopOnIdleEnd>
      <RestartOnIdle>false</RestartOnIdle>
    </IdleSettings>
    <MultipleInstancesPolicy>IgnoreNew</MultipleInstancesPolicy>
    <DisallowStartIfOnBatteries>true</DisallowStartIfOnBatteries>
    <StopIfGoingOnBatteries>true</StopIfGoingOnBatteries>
    <AllowHardTerminate>true</AllowHardTerminate>
    <StartWhenAvailable>false</StartWhenAvailable>
    <RunOnlyIfNetworkAvailable>false</RunOnlyIfNetworkAvailable>
    <AllowStartOnDemand>true</AllowStartOnDemand>
    <Enabled>true</Enabled>
    <Hidden>false</Hidden>
    <RunOnlyIfIdle>false</RunOnlyIfIdle>
    <WakeToRun>true</WakeToRun>
    <ExecutionTimeLimit>P3D</ExecutionTimeLimit>
    <DeleteExpiredTaskAfter>PT05</DeleteExpiredTaskAfter>
    <Priority>7</Priority>
    <RestartOnFailure>
      <Interval>PT1M</Interval>
      <Count>3</Count>
    </RestartOnFailure>
  </Settings>
  <Actions Context="Author">
    <Exec>
      <Command>C:\Windows\System32\slmgr.vbs</Command>
      <Arguments>-rearm</Arguments>
    </Exec>
    <Exec>
      <Command>C:\Windows\System32\shutdown.exe</Command>
      <Arguments>/r</Arguments>
    </Exec>
  </Actions>
</Task>
```

3. 在示例任务中，更改以下 "UserID" 标签的值，使其包含您的域名和别名：
   `<UserId>domain\alias</UserId>`
4. 在任务计划程序中，单击**操作**菜单上的**导入任务**。
5. 单击示例任务的 .xml 文件。例如，单击 **Extend.xml**。
6. 单击**导入**。
7. 单击**触发器**选项卡。
8. 单击**一次性**触发器，然后单击**编辑**。
9. 将任务的开始日期更改为您当前评估期结束前不久的一日期。
10. 单击**确定**，然后退出任务计划程序。

任务计划程序现在将在您指定的日期运行评估重置操作。

## 为参加 Microsoft 认证技术专家 (MCTS) 考试做准备

Microsoft 认证技术专家 (MCTS) 认证使专业人员能够针对特定技术，并通过展示其在专业技术领域的深入知识和专业知识来脱颖而出。Microsoft 认证技术专家始终具备实施、构建、排查故障和调试特定 Microsoft 技术的能力。

对于组织而言，新一代 Microsoft 认证提供了更好的技能验证工具，有助于评估不仅限于 Windows Server 的高需求技能，还包括快速完成工作任务的能力。个人将更容易找到并努力实现符合其个人和专业目标的认证资格。

要了解有关成为 Microsoft 认证专业人士以及考试可用性的更多信息，请访问 www.microsoft.com/learning/mcp。

### 面向 IT 专业人员的 Microsoft 认证

新的 Microsoft 认证技术专家 (MCTS) 和 Microsoft 认证 IT 专业人员 (MCITP) 资质为 IT 专业人员提供了一个更简单、更具针对性的框架，除了展示特定开发人员职位所需的技能外，还可以展示他们的技术技能。

Microsoft 认证数据库管理员 (MCDBA)、Microsoft 认证桌面支持技师 (MCDST)、Microsoft 认证系统管理员 (MCSA) 以及 Microsoft 认证系统工程师 (MCSE) 资质继续为使用 Microsoft SQL Server 2000、Windows XP 和 Windows Server 2003 的 IT 专业人员提供行业认可，并验证其 IT 技能和经验。

### Microsoft 认证技术专家

新的 Microsoft 认证技术专家 (MCTS) 资质突显了您使用特定 Microsoft 技术的技能。您可以展示自己作为 IT 专业人员或开发人员的能力，对目前使用或计划部署的 Microsoft 技术拥有深入的知识。

MCTS 认证使专业人员能够针对特定技术，并通过展示其在专业技术领域的深入知识和专业知识来脱颖而出。Microsoft 认证技术专家始终具备实施、构建、排查故障和调试特定 Microsoft 技术的能力。

您可以在 www.microsoft.com/learning/mcp/mcts 了解更多关于 MCTS 计划的信息。

### Microsoft 认证 IT 专业人员

新的 Microsoft 认证 IT 专业人员 (MCITP) 资质让您能够突显您的特定专业领域。现在，您可以轻松地将自己确立为数据库管理、数据库开发、商业智能或支持领域的专家。

通过获得认证，您向雇主证明，您不仅在 *Windows Server* 操作系统的操作方面达到了可预见的技能水平，而且在一系列全面的 Microsoft 技术方面也达到了该水平。雇主通常要求作为就业或在公司或其他组织内晋升的条件进行认证。

您可以在 http://www.microsoft.com/learning/mcp/mcitp 了解更多关于 MCITP 计划的信息。

认证考试由 Microsoft 赞助，但通过 Microsoft 的考试交付合作伙伴 Prometric 进行管理。

### 为参加考试做准备

除非您是非常有经验的用户，否则您需要使用考试准备课程来准备在规定时间内正确地完成测试。*Microsoft Official Academic Course* 系列旨在为您具备所有考试主题的扎实知识做好准备，并经过一些额外的自行复习和练习，您应该对自己的能力通过相应考试感到自信。

