
```c
#pragma omp task shared(array) firstprivate(lower,tupper)

if (lower < tupper) { quick_sort_range(array, lower, tupper); }

#pragma omp task shared(array) firstprivate(tlower,tupper)

if (tlower < upper) { quick_sort_range(array, tlower, upper); }

}

void quick_sort(int *array, int elements) {

#pragma omp parallel

#pragma omp single nowait

quick_sort_range(array, 0, elements);

}
```

# 第 9 章 使用多核处理器进行扩展

总结这些讨论，某些算法在本质上是串行的，因此为了使应用程序并行化，可能需要对算法进行更改。并不是并行算法都同样有效。关键特征是算法扩展到的线程数，以及算法引入的开销大小。

在之前讨论的背景下，冒泡排序是串行的，但可以泛化为奇偶排序（odd-even sort）。这更好地利用了多个线程，但仍然不是一种高效的算法。将算法改为快速排序可以提供一种更高效的算法，并且仍然能够扩展到许多线程。

在特殊情况下，我们很幸运，我们的并行算法恰好比串行版本更高效。情况并非总是如此。有时会出现并行算法扩展良好，但代价是串行性能的降低。在这些情况下，值得考虑是否需要实现多种算法并在运行时进行选择，以决定哪种更高效。

算法还有另一种方法，这在某些应用领域并不少见，特别是在跨集群进行计算且节点间通信开销巨大的情况下。这种方法是使用一种迭代收敛的算法。所需的迭代次数取决于计算的准确性要求。这为算法的并行化提供了一个有趣的调优机制。

用一个例子来描述可能最简单。假设问题是模拟流体沿受阻管道的流动。可以很容易将管道分成多个部分，并为每个部分分配一组线程来执行计算。然而，一个部分的结果将取决于相邻部分的结果。因此，真正的计算需要在各个交汇处交换大量数据。

这种数据交换会使应用程序串行，并限制可以实现的扩展程度。一种解决办法是近似相邻部分的值，并在相邻部分完善其结果时对这些近似值进行优化。通过这种方式，可以使计算几乎相互独立。这种近似的代价是求解器需要更多迭代才能收敛到正确答案。

这种方法通常用于集群上的程序，因为两个节点之间交换数据的开销非常大。近似使得每个节点能够继续进行并行处理。尽管迭代次数增加，这种方法仍然可以带来更快的求解时间。

## 扩展的硬件限制

硬件的设计和实现对运行其上的应用程序的扩展产生实质影响。有三个关键领域会对扩展产生巨大影响。缓存和内存的带宽将由系统上的活动线程分。。缓存的设计决定了由于容量和冲突引起的缓存缺失会导致丢失多少时间。处理器核心流水线在活动软件线程之间的共享方式决定了指令发射率如何随着活动线程数量的而变化。

## 核心之间的带宽共享

带宽是线程间共享的另一个资源。系统的带宽容量取决于处理器和内存系统的设计，以及内存芯片在系统中的位置。其结果是，两个系统可能包含相同的处理器和主板，但带宽测量值却不同。通常，一个配置以获得最佳性能的系统会使用昂贵的内存芯片。

处理器可以消耗的带宽是待处理内存请求数量以及这些请求返回速率的函数。这些内存请求可能来自硬件或软件预取，也可能来自加载或存储操作。由于每个线程都可以发布内存请求，处理器运行的线程越多，处理器能消耗的带宽就越多。

许多像 `strlen()` 和 `memset()` 等字符串处理程序可能是内存带宽的大消耗者。由于这些程序作为操作系统的一部分提供的，因此通常经过了优化，以为特定系统提供最佳性能。列表 9.17 中的代码使用多个线程对内存的不离交区域调用 `memset()`，以估计系统上可用的内存带宽。带宽可以通过访问内存量除以完成访问所需的时间来测量。

### 列表 9.17 使用 memset 测量带宽

```c
#include <stdio.h>
#include <stdlib.h>
#include <strings.h>
#include <pthread.h>
#include <sys/time.h>
#define BLOCKSIZE 1024*25
int nthreads = 8;
char * memory;
double now(){
    struct timeval time;
    gettimeofday(&time, NULL);
    return (double)time.tv_sec + (double)time.tv_usec / 1000000.0;
}
```

```c
void *experiment( void *id ) {
  unsigned int seed = 0;
  int count = 20000;
  for(int i=0; i<count; i++) {
    memset(&memory[(long)id * BLOCKSIZE], 0, BLOCKSIZE);
    if (seed == 1) printf(" ");
  }
}
int main(int argc, char *argv[]) {
  pthread_t threads[64];
  memory = (char*)malloc(64*BLOCKSIZE);
  if (argc > 1) nthreads = atoi(argv[1]);
  double start = now();
  for(int i=0; i<nthreads; i++) {
    pthread_create(&threads[i], NULL, experiment, (void*)i);
  }
  for ( int i=0; i<nthreads; i++) {
    pthread_join(threads[i], NULL);
  }
  double end = now();
  printf("%d Threads Time %f Bandwidth %f GB/s\n", nthreads,
    (end - start),
    ((double)nthreads * 20000.0) / (end - start) / 1000000.0);
  return 0;
}
```
