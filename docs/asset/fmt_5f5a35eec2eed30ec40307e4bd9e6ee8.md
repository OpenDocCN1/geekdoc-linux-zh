
## 第 9 章：I/O 流

- **6.** 下面代码片段在第 9 行打印什么？

```java
FileOutputStream fos = new FileOutputStream("xx*");
for (byte b=0; b<50; b++) {
  fos.write(b);
}
fos.close();

RandomAccessFile raf = new RandomAccessFile("xx", "r");
raf.seek(10);
int i = raf.read();
raf.close();
System.out.println("i = " + i);
```

A. 输出是 `i = 30`。
B. 输出是 `i = 20`。
C. 输出是 `i = 10`。
D. 没有输出，因为代码在第 1 行抛出了异常。
E. 没有输出，因为代码在第 5 行抛出了异常。

- **7.** 使用以下代码创建一个文件：

```java
FileOutputStream fos = new FileOutputStream("datafile*");
DataOutputStream dos = new DataOutputStream(fos);
for (int i=0; i<500; i++) {
  dos.writeInt(i);
}
```

你想写代码从该文件中读取数据。哪些解决方案是有效的？（选择所有适用项）

A. 构造一个 `FileInputStream`，传入文件名。在 `FileInputStream` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。
B. 构造一个 `FileReader`，传入文件名。调用文件读取器的 `readInt()` 方法。
C. 构造一个 `PipedInputStream`，传入文件名。调用管道输入流的 `readInt()` 方法。
D. 构造一个 `RandomAccessFile`，传入文件名。调用随机访问文件的 `readInt()` 方法。
E. 构造一个 `FileReader`，传入文件名。在 `FileReader` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。

- **8.** 下面哪个是正确的？

A. `Readers` 有可以读取并返回 `float` 和 `double` 的方法。
B. `Readers` 有可以读取并返回 `float` 的方法。
C. `Readers` 有可以读取并返回 `double` 的方法。
D. `Readers` 有可以读取并返回 `int` 的方法。
E. 以上都不是。

- **9.** 你在一个空目录下执行以下代码。结果是什么？

```java
File f1 = new File("dirname");
File f2 = new File(f1, "filename");
```

A. 在当前工作目录下创建一个名为 `dirname` 的新目录。
B. 在当前工作目录下创建一个名为 `dirname` 的新目录。在 `dirname` 目录下创建一个名为 `filename` 的新文件。
C. 在当前工作目录下创建一个名为 `dirname` 的新目录和一个名为 `filename` 的新文件。
D. 在当前工作目录下创建一个名为 `filename` 的新文件。
E. 没有创建目录，也没有创建文件。

- **10.** 尝试编译并执行以下代码片段的结果是什么？假设该代码片段是一个在当前工作目录具有写权限的应用程序的一部分。

```java
try {
  FileOutputStream fos = new FileOutputStream("datafile*");
  DataOutputStream dos = new DataOutputStream(fos);
  RandomAccessFile raf = new RandomAccessFile("xx", "rw");
  BufferedOutputStream bos = new BufferedOutputStream(raf);
  dos.writeInt(3);
  dos.close();
  fos.close();
  raf.close();
} catch (IOException e) { }
```

A. 2
B. 8
C. 12
D. 16
E. 字节数取决于底层系统。
