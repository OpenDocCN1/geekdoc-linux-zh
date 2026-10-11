
27. Olaf Kirch. *Linux Network Administrator's Guide*. SSC, Seattle, WA, 1994.

28. Leslie Lamport. A fast mutual exclusion algorithm. *ACM Transactions on Computer Systems*, 5(1):1–11, February 1987.

29. B.W. Lampson and K. Pier. A processor for a high-performance personal computer. Technical Report CS1-81-1, Xerox Palo Alto Research Center, Jan 1981.

30. Samuel J. Leffler, Marshall Kirk McKusick, Michael J. Karels, and John S. Quarterman. *The Design and Implementation of the 4.3BSD UNIX Operating System*. Addison-Wesley Publishing Company, Reading, Massachusetts, 1988.

31. Henry Levy and Peter H. Lipman. Virtual memory management in the VAX/VMS operating system. *IEEE Computer*, March 1982.

32. John Lions. *A Commentary on the UNIX Operating System*. Department of Computer Science, University of New South Wales, 1977.

33. H. Lycklama and D.L. Bayer. The MERT operating system. *Bell System Technical Journal*, 57(6):2049–2086, July-August 1978.

34. Mamoru Maekawa, Rod Oldehoeft, and Arch Oldehoeft. *Operating Systems: Advanced Concepts*. Benjamin/Cummings, 1987.

35. M.D. McIlroy, E.N. Pinson, and B.A. Tague. Foreword. *Bell System Technical Journal*, 57(6):1899–1904, July-August 1978.

36. Hans-Peter Messmer. *The indispensable PC hardware book: your hardware questions answered*. Addison-Wesley Publishing Company, Reading, Massachusetts, 1995.

37. Elliott I. Organick. *The Multics System: An Examination of Its Structure*. MIT Press, Cambridge, Massachusetts, 1972.

38. G.L. Peterson. Myths about the mutual exclusion. *Information Processing Letters*, 12(3):115–116, Jun 1981.

39. Rob Pike. The Blit: A multiplexed graphics terminal. *AT&T Bell Laboratories Technical Journal*, 63(8, part2), October 1982.

40. John S. Quarterman, Abraham Silberschatz, and James L. Peterson. 4.2BSD and 4.3BSD as Examples of the UNIX System. *Computing Surveys*, 17(4), December 1985.

41. D.M. Ritchie. The evolution of the UNIX time-sharing system. *AT&T Bell Laboratories Technical Journal*, 63(8), October 1984.

42. D.M. Ritchie. A stream input-output system. *AT&T Bell Laboratories Technical Journal*, 63(8), October 1984.

43. D.M. Ritchie and K. Thompson. The UNIX time-sharing system. *Bell System Technical Journal*, 57(6), July-August 1978.

44. Peter H. Salus. *A Quarter Century of Unix*. Addison-Wesley Publishing Company, Reading, Massachusetts, 1994.

45. Curt Schimmel. *UNIX systems for modern architectures: symmetric multiprocessing and caching for kernel programmers*. Addison-Wesley Publishing Company, Reading, Massachusetts, 1994.

## 参考文献

[46] Abraham Silberschatz 和 Peter B. Galvin。**《操作系统概念（第四版）》**。Addison-Wesley 出版社，马萨诸塞州列丁市，1994 年。

[47] Mark Sobell。**《Unix 系统实用指南（第三版）》**。Benjamin/Cummings 出版社，加利福尼亚州红木城，1994 年。

[48] L. Svobodova. 基于网络的分布式系统文件服务器。*Computing Surveys*，16(4):353–398，1984 年 12 月。

[49] Andrew S. Tanenbaum。**《操作系统：设计与实现》**。Prentice-Hall，新泽西州恩格尔伍德克利夫斯，1987 年。

[50] C. Thacker 等. Alto：一台个人计算机。技术报告 CSL-79-11，Xerox 帕洛阿尔托研究中心，1979 年 8 月。

[51] Ken Thompson. UNIX 实现。*The Bell System Technical Journal*，57(6)，1978 年 7 月-8 月。

[52] B. Walker 等. LOCUS 分布式操作系统。*Operating Systems Review*，17(5):49–70，1983 年 10 月。

[53] Matt Welsh 和 Lar Kaufman。**《运行 Linux》**。O'Reilly & Associates，加利福尼亚州塞巴斯托波尔，1995 年。

## 附录 B

### 系统调用

大多数系统调用最终都是通过内核中跳转表里的入口点来访问的，但用户是通过运行时库中的入口点来了解它们的。（这里涉及一些不确定的领域。隐藏的调用可以绕过运行时库并直接执行陷阱指令。这是在测试某些新调用时的常见操作。当被证明正确且有用后，入口点将被添加到运行时库中。）目前，跳转表中有 162 个入口点，运行时库中有 172 个有文档记录的入口点。（但我的库稍显过时，因此某些系统调用确实有运行时库等效物。）

#### I/O

尽管简短描述中常提到“一个文件”，但该文件实际上可能是一个目录、外围设备、命名管道（fifo）或其他此类对象的引用。

- **通用**
  - `access` - 检查用户对文件的权限
  - `chmod`, `fchmod` - 更改文件权限
  - `chown`, `fchown` - 更改文件所有权
  - `close` - 关闭文件描述符
  - `dup`, `dup2` - 复制文件描述符
  - `fcntl` - 操纵文件描述符
  - `link` - 为文件创建新名称
  - `open`, `creat` - 打开并可能创建文件或设备
  - `read` - 从文件描述符读取
  - `rename` - 更改文件或位置名称
  - `stat`, `fstat`, `lstat` - 获取文件状态
  - `umask` - 设置文件创建掩码
  - `unlink` - 删除名称及可能删除其所引用的文件
  - `utime`, `utimes` - 更改 inode 的访问和/或修改时间
  - `write` - 写入文件描述符

#### 文件

- `flock` - 在打开的文件上应用或移除建议锁
