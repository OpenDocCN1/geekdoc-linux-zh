

然而，批处理作业的调度并不是 z/VM 或 Linux 中的常见概念。实际上，要运行多个 *batch* 进程，你可以为此创建一个脚本，或者一次性全部运行，知道它们最终会竞争 I/O 资源。

以下部分概述了与 z/OS 作业输入子系统（JES）类似的工具。你可以通过使用这些调度工具并创建脚本来模拟批处理队列。

## 5.4.1 作业调度

本节比较了 z/VM 和 Linux 中的作业调度。

### z/VM 中的作业调度

调度作业通常使用无需人工干预的任务来完成，例如操作日志和创建备份。在 z/VM 中调度作业并不是一项常规任务，因为管理员通常使用来宾系统中的可用工具来执行这些任务。

为了完整性，作者在网上搜索并找到了一些产品，例如 CA VM:Schedule for z/VM、IBM Operations Manager for z/VM，以及随 z/VM 提供的两个免费工具（PROP 和 WAKEUP），它们可以实现作业调度。

### Linux 中的作业调度

Linux 系统有一个名为 cron 的实用工具，用于定期调度程序运行。调度信息放在 /etc/crontab 文件中，使用以下格式：

```
minute hour day month year username command
```

你可以将每个时间组件指定为整数。例如，使用 1 到 12 的数字表示一月到十二月。或者使用星号 (*) 字符指定一个或多个组件，它们被视为通配符。例如，月份组件中的 * 表示命令将在每个月的指定日期和时间运行。username 参数应为执行命令的用户的名称，出于安全或权限原因，该名称可能不同。例如，备份进程必须由可以读取所有目录中所有文件的用户运行。每个用户还可以在主目录中放置一个 crontab 文件。有关更多信息，请参阅：

http://www.linuxdoc.org

in batch mode. The system operator generates the batch machine by either of the following methods:

- Entering the BATCH parameter in the PARM field of the IPL command
- Specifying the NOSPROF parameter of the IPL command and entering the CMSBATCH command when the VM READ status appears.

After each job is executed, the batch facility IPLs itself, thereby providing a continuously processing batch machine. The batch processor IPLs itself by using the PARM option of the CP IPL command followed by a character string that CMS recognizes as peculiar to a batch virtual machine performing its IPL. Jobs are sent to the batch machine's virtual card reader from user terminals and executed sequentially. When no jobs are waiting for execution, the CMS batch facility remains in a wait-state, ready to execute a user job. The CMS batch facility is particularly useful for compute-bound jobs such as assemblies and compilations and for execution of large user programs, because interactive users can continue working at their terminals while their time-consuming jobs are run in another virtual machine. The system programmer controls the batch facility virtual machine environment by resetting the CMS batch facility machine's system limits, by writing routines that handle special installation input to the batch facility, and by writing exec procedures that make the CMS batch facility easier to use.

> Note: For in-depth information about how to use the CMS Batch Facility, refer to the CMS Planning and Administration, SC24-6078 at:
> http://publibz.boulder.ibm.com/epubs/pdf/hcsq2b10.pdf

## 在 Linux 中模拟批处理作业

本节为你提供了如何使用脚本模拟类似批处理的处理的非常简单的概述。你还可以安排 cron 在夜间运行脚本，例如运行每日销售报告。

本节中的场景使用了 shell 脚本⁷，一种被许多 Linux shell 解释的语言，来控制进程的批处理行为。此控制脚本一次运行一个程序。我们编写了两个简单的程序来对文本文件中的单词进行排序：一个按自然顺序，另一个按逆序。

脚本显示在第 278 页的示例 5-52 中。它调用 ./batch 文件夹中找到的所有程序，我们的排序程序。每个程序在我们的 ./input 文件夹中都有对应的输入文件（我们放置了用于排序的文件），每个输出都发送到我们的 ./output 文件夹。唯一的限制是

⁷ Shell 是一个解释用户输入、调用相应系统命令并显示该命令输出的程序。它是你在 Linux 控制台登录后看到的用户界面。

