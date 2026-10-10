

## 环境变量

*GIT_NOTES_REF*

指定操作笔记所用的引用，以替代 refs/notes/commits。此设置会覆盖 core.notesRef 配置。

*GIT_NOTES_DISPLAY_REF*

以冒号分隔的引用或通配符列表，指示在显示提交信息时，除了 core.notesRef 或 *GIT_NOTES_REF* 的默认值外，还要从哪些引用读取笔记。此设置会覆盖 notes.displayRef 配置。

对于不存在的引用，会发出警告；但未匹配到任何引用的通配符将被静默忽略。

*GIT_NOTES_REWRITE_MODE*

在重写过程中复制笔记时，如果目标提交已经存在笔记，应如何处理。必须是 overwrite、concatenate 或 ignore 之一。此设置会覆盖 core.rewriteMode 配置。

*GIT_NOTES_REWRITE_REF*

在重写提交时，指定从原始提交复制到重写提交的笔记。必须是一个以冒号分隔的引用或通配符列表。

如果未通过环境变量设置，则要复制的笔记列表取决于 notes.rewrite.<命令> 和 notes.rewriteRef 配置。

## 笔记

1. 允许的路径名形式为 $ab/cd/ef/.../abcdef...$：由多个各含两个十六进制字符的目录名序列，后跟一个包含对象 ID 剩余部分的文件名组成。

# GIT-PACK-OBJECTS

**名称**

git-pack-objects - 创建对象的打包存档

## 概要

```
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied] [--no-reuse-delta] [--delta-base-offset] [--non-empty] [--local] [--incremental] [--window=<n>] [--depth=<n>] [--revs [--unpacked | --all]] [--stdout | base-name] [--shallow] [--keep-true-parents] < object-list
```

## 描述

从标准输入读取对象列表，并写入具有指定基名的打包存档，或写入标准输出。

打包存档是将在两个存储库之间传输一组对象的高效方式，也是一种访问高效的归档格式。在打包存档中，对象要么作为整体压缩存储，要么作为与其他对象的差异存储。后者通常称为 delta（增量）。

打包存档格式（.pack）旨在自包含，因此无需额外信息即可解包。因此，delta 所依赖的每个对象必须包含在 pack 中。

会生成 pack 索引文件（.idx）以便快速随机访问 pack 中的对象。将索引文件（.idx）和打包存档（.pack）放入 $GIT_OBJECT_DIRECTORY（或 $GIT_ALTERNATE_OBJECT_DIRECTORIES 中的任何目录）的 pack/ 子目录中，即可使 Git 从 pack 存档中读取数据。

git unpack-objects 命令可以读取打包存档，并将 pack 中包含的对象扩展为“一文件一对象”格式；这通常由智能拉取命令在对端为高效网络传输即时创建 pack 时执行。

## 选项

- **base-name**

  写入一对文件（.pack 和 .idx），使用 <base-name> 来确定创建文件的名称。使用此选项时，这两个文件将写入为 <base-name>-<SHA-1>.{pack,idx} 文件。<SHA-1> 是基于 pack 内容生成的哈希值，并写入命令的标准输出。

- **—stdout**

  将 pack 内容（本应写入 .pack 文件的内容）输出到标准输出。

- **—revs**

  从标准输入读取修订参数，而不是单个对象名称。修订参数的处理方式与带有 —objects 标志的 git rev-list 相同，它使用其提交参数来构建其输出对象列表。结果列表中的对象将被打包。除了修订参数外，还接受 —not 或 —shallow <SHA-1> 行。

- **—unpacked**

  这隐含 —revs。在处理从标准输入读取的修订参数列表时，限制打包的对象为那些尚未被打包的对象。

- **—all**

  这隐含 —revs。除了从标准输入读取的修订参数列表外，还假装所有 refs/ 下的引用都被指定为要包含在内。

- **—include-tag**

  如果它们引用的对象已包含在生成的 packfile 中，则包含未被请求的注释标签。这在向原生 Git 客户端发送新标签时很有用。

- **—window=<n>, —depth=<n>**

  这两个选项影响 pack 中使用 delta 压缩存储对象的方式。对象首先按类型、大小和可选的名称内部排序，并与 —window 内的其他对象进行比较，以查看使用 delta 压缩是否能节省空间。—depth 限制最大 delta 深度；设置得过高会影响解包端的性能，因为必须应用那么多次的 delta 数据才能获取必要的对象。—window 的默认值为 10，—depth 的默认值为 50。

- **—window-memory=<n>**

  此选项在 —window 之上提供额外的限制；窗口大小将动态缩小，以确保在内存中不超过 <n> 字节。这对于具有大对象和小对象混合的存储库很有用，可以避免因窗口过大而导致内存不足，同时仍然能够利用大窗口对较小对象的优化优势。大小后缀可以是 “k”、“m” 或 “g”。—window-memory=0 表示内存使用无限制，这是默认值。

- **—max-pack-size=<n>**

  每个输出 pack 文件的最大大小。大小后缀可以是 “k”、“m” 或 “g”。允许的最小大小限制为 1 MiB。如果指定，可能会创建多个 packfile。默认是无限制的，除非设置了配置变量 pack.packSizeLimit。

- **—honor-pack-keep**

  此标志会导致忽略本地 pack 中已有 .keep 文件的对象，即使它们原本会被打包。

- **—incremental**

  此标志会导致忽略已经在 pack 中的对象，即使它们原本会被打包。

- **—local**

  此标志会导致忽略从替代对象存储库借用的对象，即使它们原本会被打包。

- **—non-empty**

  仅当打包存档至少包含一个对象时才创建该存档。

- **—progress**

  默认情况下，如果标准错误流附加到终端，则会在标准错误流上报告进度状态，除非指定了 -q。此标志强制显示进度状态，即使标准错误流未指向终端。

- **—all-progress**

  当指定 —stdout 时，进度报告在对象计数和压缩阶段显示，但在写入阶段被抑制。原因在于某些情况下，输出流直接链接到另一个命令，该命令在处理传入的 pack 数据时可能希望显示其自身的进度状态。此标志类似于 —progress，但即使使用 —stdout，也强制在写入阶段显示进度报告。

- **—all-progress-implied**

  这用于在激活进度显示时隐含 —all-progress。与 —all-progress 不同，此标志本身并不实际强制显示任何进度。

- **-q**

  此标志使命令不在标准错误流上报告其进度。

- **—no-reuse-delta**

  在具有现有 pack 的存储库中创建打包存档时，该命令会重用现有 delta。这有时会导致 pack 略次优。此标志告诉命令不重用现有 delta，而是从头开始计算。

- **—no-reuse-object**

  此标志告诉命令完全不重用现有对象数据，包括非 delta 化的对象，强制重新压缩所有内容。这隐含 —no-reuse-delta。仅在需要强制对打包数据应用不同压缩级别这种罕见情况下有用。

- **—compression=<n>**

  指定生成的 pack 中新压缩数据的压缩级别。如果未指定，pack 压缩级别首先由 pack.compression 确定，然后由 core.compression 确定，如果两者都未设置，则默认为 -1（zlib 默认值）。如果需要强制对所有数据应用统一的压缩级别，无论来源如何，请添加 —no-reuse-object。

- **—thin**

  通过省略发送方和接收方之间的公共对象来创建“thin” pack，以减少网络传输。此选项仅与 —stdout 配合使用时才有意义。

  > 注意：thin pack 通过省略必需对象违反了打包存档格式，因此 Git 无法直接使用，除非使其自包含。使用 git index-pack —fix-thin（参见 (1)）来恢复自包含属性。

- **—shallow**

  优化提供给浅层存储库客户端的 pack。此选项与 —thin 结合使用，可以以速度为代价生成更小的 pack。

- **—delta-base-offset**

  打包存档可以将 delta 的基础对象表示为 20 字节对象名称或流中的偏移量，但古老版本的 Git 无法理解后者。默认情况下，*git pack-objects* 仅使用前一种格式以获得更好的兼容性。此选项允许命令使用后一种格式以获得更紧凑性。取决于平均 delta 链长度，此选项通常会将生成的 packfile 缩小 3-5 个百分点。

  > 注意：如 *git gc*（参见 (1)）、*git repack*（参见 (1)）等 Porcelain 命令在现代 Git 中将对象放入存储库的 pack 文件时，默认会传递此选项。*git bundle*（参见 (1)）在创建 bundle 时也会传递此选项。

- **—threads=<n>**

  指定在搜索最佳 delta 匹配时生成的线程数。这需要 *pack-objects* 是使用 pthreads 编译的，否则该选项将被忽略并发出警告。这旨在减少多处理器机器上的打包时间。

