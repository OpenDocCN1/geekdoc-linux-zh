
## 第 5 章 工作负载测量

报告的命令按 `KOREMIN` 排序，`KOREMIN` 是命令运行期间 CPU 时间和所用内存的乘积。`CPU-MIN` 是 CPU 运行次数。`REAL_MIN` 是进程在整个生命周期内 RSS 的平均值。此读取器不包含进程未实际运行的时间。（在 `Solaris 2` 和早期版本中，存在一个导致此项测量无效的 bug。）`HOG FACTOR` 是 `CPU-MIN` 与 `REAL-MIN` 的比值；高因子意味着命令在运行时会一直占用 CPU。`CHRS TRANSF` 使用从每次读取中获取的块数据。

`Solaris` 以及更多
