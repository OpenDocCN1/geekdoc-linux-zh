
Resque 使用 `fork(2)` 来确保其工作进程的内存占用不会膨胀。让我们回顾一下 Resque 工作进程 `fork` 时发生了什么，以及它如何影响 Ruby 虚拟机。

你可能还记得 `fork(2)` 会创建一个原始进程的精确副本新进程。在这种情况下，原始进程已经加载了应用程序环境且没有其他内容。因此我们知道在 `fork` 之后，我们将有一个只加载了应用程序环境的新进程。

然后子进程将开始处理任务。这就是内存使用可能出现问题。后台任务可能需要将图像文件加载到主内存中处理，或者从数据库获取大量的 `ActiveRecord` 对象，或者任何需要使用大量主内存的操作。

一旦子进程完成任务，它就会退出，从而将其所有内存释放给操作系统进行清理。然后原始进程就可以恢复运行，此时再次只加载了应用程序环境。

所以，每当 Resque 执行一个任务时，你在内存使用方面都回到了一个干净的起点。这意味着在处理任务时，内存占用可能会飙升，但它应该总是回到那个良好的基准线。

## GC（垃圾回收）不就帮我们清理的吗？

嗯，是的，但它做得并不完美。它做得还可以。事实是，`MRI` 的 `GC` 很难释放它不再需要的内存。

当 Ruby 虚拟机启动时，内核会为它分配某块主内存。当它用完所有可用内存时，它需要向内核请求另一块主内存。

由于 Ruby `GC` 的许多问题（天真的方法、磁盘碎片化），虚拟机很少能将内存块释放回内核。因此，Ruby 进程的内存占用可能会随时间推移而增长，而不是缩小。现在 Resque 的方法开始变得合理起来了！

如果 Resque 工作进程简单地按可用顺序处理每个任务，它将无法维持那个良好的内存使用基准水平。一旦它处理一个需要大量主内存的任务，这些内存就会一直被工作进程占用，直到它退出。

即使随后的任务需要的内存少得多，Ruby 也很难将这些内存还给内核。因此，工作进程不可避免地随着时间推移而变大，永不缩小。

得益于 `fork(2)` 的威力，Resque 工作进程是可靠的，在处理一定数量的任务后不需要重启。

## 附录：Unicorn 如何收割工作进程

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 事实上的收割

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

- ¹See http://www.unicorn-server.org/

```ruby
def reap_all
  begin
    wpid, status = Process.waitpid(-1, Process::WNOHANG)
    return unless wpid
    
    if status.success?
      logger.info "reaped worker #{wpid}"
    else
      logger.error "worker #{wpid} exited with status #{status}"
    end
    
    reap_all
  rescue Errno::ECHILD
  end
end
```

```ruby
wpid or return
```

这一行看起来可能有点奇怪，但它实际上是一个条件返回语句。如果 `wpid` 为 `nil`，那么我们最后一行返回了 `nil`。这意味着没有子进程退出并将其状态返回给我们。

如果是这样，那么此方法将返回，它的任务就完成了。

```ruby
if reexec_pid == wpid
  logger.error "reaped #{status.inspect} exec()-ed"
  self.reexec_pid = 0
  self.pid = pid.chomp('.oldbin') if pid
  proc_name = 'master'
```

我不想花很多时间来讨论这部分。'reexec' 相关内容与 Unicorn 的内部实现有关，特别是它是如何处理零停机重启的。也许我可以在未来的报告中介绍这个过程。

我想要引起你注意的是对 `proc_name` 的调用。这类似于 Resque 章节中的 `procline` 方法。Unicorn 也有一个更改当前进程显示名称的方法。这是与软件用户通信的一个至关重要的部分。

```ruby
else
  worker = WORKERS.delete(wpid) and worker.close rescue nil
```

Unicorn 在其 `WORKERS` 常量中存储了当前活跃的 worker 进程列表。`WORKERS` 是哈希，键是 worker 进程的 `pid`，值是 `Unicorn::Worker` 的实例。

因此，这一行从 Unicorn 的内部跟踪列表 `(WORKERS)` 中移除 worker 进程，并在 worker 实例上调用 `#close`，关闭其不再需要的心跳机制。

```ruby
m = "reaped #{status.inspect} worker=#{worker.nr} rescue 'unknown'"
```

这一行根据 `Process.waitpid2` 调用返回的 `status` 构建了日志消息。

该字符串是通过首先检查 `status` 变量构建的。它看起来像什么？类似于这样：

```
#<Process::Status: pid=32227, exited(0)>
# or
#<Process::Status: pid=32308, signaled(SIGINT=2)>
```
