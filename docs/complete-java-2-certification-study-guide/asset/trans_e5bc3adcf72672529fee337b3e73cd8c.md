

# 复习题

- 1. 下面哪些陈述是正确的？（选择所有适用项）
A. UTF 字符都是 8 位。
B. UTF 字符都是 16 位。
C. UTF 字符都是 24 位。
D. Unicode 字符都是 16 位。
E. 字节码字符都是 16 位。
F. 以上都不是。

- 2. 下面哪些陈述是正确的？（选择所有适用项）
A. 当你构造 `File` 实例时，如果没有使用本地机器的文件命名语义，构造函数将抛出 `IOException`。
B. 当你构造 `File` 实例时，如果本地文件系统中不存在相应的文件，则会创建一个文件。
C. 当 `File` 实例被垃圾回收时，本地文件系统上的相应文件会被删除。
D. 以上都不是。

- 3. 下面哪些陈述是正确的？（选择所有适用项）
A. 要更改当前工作目录，请调用 `File` 类的 `setWorkingDirectory()` 方法。
B. 要更改当前工作目录，请调用 `File` 类的 `cd()` 方法。
C. 要更改当前工作目录，请调用 `File` 类的 `changeWorkingDirectory()` 方法。
D. 以上都不是。

- 4. 如何使用 `File` 类列出目录的内容？
A. `String[] contents = myFile.list();`
B. `File[] contents = myFile.list();`
C. `StringBuilder[] contents = myFile.list();`
D. `File` 类没有提供列出目录的方法。

- 5. 下面代码向文件 `dest` 写入了多少字节？
```java
try {
  FileOutputStream fos = new FileOutputStream("dest*");
  DataOutputStream dos = new DataOutputStream(fos);
  dos.writeInt(3);
  dos.writeDouble(0.0001);
  dos.close();
  fos.close();
} catch (IOException e) { }
```
A. 2
B. 8
C. 12
D. 16
E. 字节数取决于底层系统。

- 6. 下面代码片段在第 9 行打印什么？
```java
FileOutputStream fos = new FileOutputStream("xx*");
for (byte b=0; b<50; b++)
  fos.write(b);
fos.close();
RandomAccessFile raf = new RandomAccessFile("xx", "r*");
raf.seek(10);
int i = raf.read();
raf.close();
System.out.println("i = " + i);
```
A. 输出是 i = 30。
B. 输出是 i = 20。
C. 输出是 i = 10。
D. 没有输出，因为代码在第 1 行抛出了异常。
E. 没有输出，因为代码在第 5 行抛出了异常。

- 7. 使用以下代码创建一个文件：
```java
FileOutputStream fos = new FileOutputStream("datafile*");
DataOutputStream dos = new DataOutputStream(fos);
for (int i=0; i<500; i++)
  dos.writeInt(i);
```
你想写代码从该文件中读取数据。哪些解决方案是有效的？（选择所有适用项）

A. 构造一个 `FileInputStream`，传入文件名。在 `FileInputStream` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。
B. 构造一个 `FileReader`，传入文件名。调用文件读取器的 `readInt()` 方法。
C. 构造一个 `PipedInputStream`，传入文件名。调用管道输入流的 `readInt()` 方法。
D. 构造一个 `RandomAccessFile`，传入文件名。调用随机访问文件的 `readInt()` 方法。
E. 构造一个 `FileReader`，传入文件名。在 `FileReader` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。

- 8. 下面哪个是正确的？
A. `Readers` 有可以读取并返回 `float` 和 `double` 的方法。
B. `Readers` 有可以读取并返回 `float` 的方法。
C. `Readers` 有可以读取并返回 `double` 的方法。
D. `Readers` 有可以读取并返回 `int` 的方法。
E. 以上都不是。

- 9. 你在一个空目录下执行以下代码。结果是什么？
```java
File f1 = new File("dirname");
File f2 = new File(f1, "filename");
```
A. 在当前工作目录下创建一个名为 `dirname` 的新目录。
B. 在当前工作目录下创建一个名为 `dirname` 的新目录。在 `dirname` 目录下创建一个名为 `filename` 的新文件。
C. 在当前工作目录下创建一个名为 `dirname` 的新目录和一个名为 `filename` 的新文件。
D. 在当前工作目录下创建一个名为 `filename` 的新文件。
E. 没有创建目录，也没有创建文件。

- 10. 尝试编译并执行以下代码片段的结果是什么？假设该代码片段是一个在当前工作目录具有写权限的应用程序的一部分。
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

- 6. 下面代码片段在第 9 行打印什么？
```java
FileOutputStream fos = new FileOutputStream("xx*");
for (byte b=0; b<50; b++)
  fos.write(b);
fos.close();
RandomAccessFile raf = new RandomAccessFile("xx", "r");
raf.seek(10);
int i = raf.read();
raf.close();
System.out.println("i = " + i);
```
A. 输出是 i = 30。
B. 输出是 i = 20。
C. 输出是 i = 10。
D. 没有输出，因为代码在第 1 行抛出了异常。
E. 没有输出，因为代码在第 5 行抛出了异常。

- 7. 使用以下代码创建一个文件：
```java
FileOutputStream fos = new FileOutputStream("datafile*");
DataOutputStream dos = new DataOutputStream(fos);
for (int i=0; i<500; i++)
  dos.writeInt(i);
```
你想写代码从该文件中读取数据。哪些解决方案是有效的？（选择所有适用项）
A. 构造一个 `FileInputStream`，传入文件名。在 `FileInputStream` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。
B. 构造一个 `FileReader`，传入文件名。调用文件读取器的 `readInt()` 方法。
C. 构造一个 `PipedInputStream`，传入文件名。调用管道输入流的 `readInt()` 方法。
D. 构造一个 `RandomAccessFile`，传入文件名。调用随机访问文件的 `readInt()` 方法。
E. 构造一个 `FileReader`，传入文件名。在 `FileReader` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。

- 8. 下面哪个是正确的？
A. `Readers` 有可以读取并返回 `float` 和 `double` 的方法。
B. `Readers` 有可以读取并返回 `float` 的方法。
C. `Readers` 有可以读取并返回 `double` 的方法。
D. `Readers` 有可以读取并返回 `int` 的方法。
E. 以上都不是。

- 9. 你在一个空目录下执行以下代码。结果是什么？
```java
File f1 = new File("dirname");
File f2 = new File(f1, "filename");
```
A. 在当前工作目录下创建一个名为 `dirname` 的新目录。
B. 在当前工作目录下创建一个名为 `dirname` 的新目录。在 `dirname` 目录下创建一个名为 `filename` 的新文件。
C. 在当前工作目录下创建一个名为 `dirname` 的新目录和一个名为 `filename` 的新文件。
D. 在当前工作目录下创建一个名为 `filename` 的新文件。
E. 没有创建目录，也没有创建文件。

- 10. 尝试编译并执行以下代码片段的结果是什么？假设该代码片段是一个在当前工作目录具有写权限的应用程序的一部分。
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

## 第 9 章：I/O 流

- 6. 下面代码片段在第 9 行打印什么？
```java
FileOutputStream fos = new FileOutputStream("xx*");
for (byte b=0; b<50; b++)
  fos.write(b);
fos.close();
RandomAccessFile raf = new RandomAccessFile("xx", "r");
raf.seek(10);
int i = raf.read();
raf.close();
System.out.println("i = " + i);
```
A. 输出是 i = 30。
B. 输出是 i = 20。
C. 输出是 i = 10。
D. 没有输出，因为代码在第 1 行抛出了异常。
E. 没有输出，因为代码在第 5 行抛出了异常。

- 7. 使用以下代码创建一个文件：
```java
FileOutputStream fos = new FileOutputStream("datafile*");
DataOutputStream dos = new DataOutputStream(fos);
for (int i=0; i<500; i++)
  dos.writeInt(i);
```
你想写代码从该文件中读取数据。哪些解决方案是有效的？（选择所有适用项）
A. 构造一个 `FileInputStream`，传入文件名。在 `FileInputStream` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。
B. 构造一个 `FileReader`，传入文件名。调用文件读取器的 `readInt()` 方法。
C. 构造一个 `PipedInputStream`，传入文件名。调用管道输入流的 `readInt()` 方法。
D. 构造一个 `RandomAccessFile`，传入文件名。调用随机访问文件的 `readInt()` 方法。
E. 构造一个 `FileReader`，传入文件名。在 `FileReader` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。

- 8. 下面哪个是正确的？
A. `Readers` 有可以读取并返回 `float` 和 `double` 的方法。
B. `Readers` 有可以读取并返回 `float` 的方法。
C. `Readers` 有可以读取并返回 `double` 的方法。
D. `Readers` 有可以读取并返回 `int` 的方法。
E. 以上都不是。

- 9. 你在一个空目录下执行以下代码。结果是什么？
```java
File f1 = new File("dirname");
File f2 = new File(f1, "filename");
```
A. 在当前工作目录下创建一个名为 `dirname` 的新目录。
B. 在当前工作目录下创建一个名为 `dirname` 的新目录。在 `dirname` 目录下创建一个名为 `filename` 的新文件。
C. 在当前工作目录下创建一个名为 `dirname` 的新目录和一个名为 `filename` 的新文件。
D. 在当前工作目录下创建一个名为 `filename` 的新文件。
E. 没有创建目录，也没有创建文件。

- 10. 尝试编译并执行以下代码片段的结果是什么？假设该代码片段是一个在当前工作目录具有写权限的应用程序的一部分。
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

