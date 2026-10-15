
## LaTeX 数学与特殊符号说明

一对 ``` `` ``` 标记表示数学上下文。许多特殊字符仅在 ``` math ``` 上下文中可用。例如，尝试一下希腊字母表：

### 小写
$$
\alpha \beta \gamma \delta \epsilon \varpsilon \zeta \eta
$$

$$
\theta \vartheta \sigma \tau \iota \kappa \lambda \mu \nu \xi \o \varpi
$$

$$
\rho \omega \upsilon \tau \phi \varpi
$$

$$
\chi \psi \omega
$$

### 大写
$$
A B \Gamma \Delta E Z H \Theta H I K \Lambda M \Xi \Pi P
$$

$$
\Sigma T \Upsilon \Phi X \Psi \Omega
$$

尝试一些方程：
$$
x^{n}(y+1) + x^*(tq)=z_{\{try\scripts\}}
$$

```latex
\center
$\frac{x \times y}(x/2)=\frac{1}{3}$
\end{center}
```

``` LaTeX ``` 数学命令与旧版 ``` Word Perfect ``` 公式编辑器中的命令非常相似。

使用 ``` verbatim ``` 打印 ``` LaTeX ``` 中通常具有特殊含义的10个特殊符号：``` \verb{\$\#^\~} ```。特殊符号必须包含在两个相同的字符之间，示例中的字符是 ``` | ```。这些特殊符号大部分也可以通过在字符前加反斜杠来打印：``` \% ```、``` \_ ```、``` \# ```、``` ^ ```、``` \~ ```。

```%``` 此命令结束文档 ```$``` (这是第三个*必须*出现在每个文档中的符号)

```latex
\end{document}
```

## 7.10 刻录 CD-Rs (``` cdrecord ``` 和 ``` cdparanoia ```)

**免责声明**：复制受版权保护的是非法的。请勿将下面的说明用于任何非法活动。

### 简介

设置 CD 刻录机可能很复杂。欲了解良好信息请参阅 http://www.guug.de/~wenni/linux/cdr/html/CD-Writing-3.html。

我使用上述文档在运行 ``` RH6.0 ``` 的 PC 上设置了一个廉价的无品牌 ``` IDE-ATAPI ``` CD 刻录机。它可以正常工作，而且在最近升级到 ``` RH6.1 ``` 后，我的设置无需进行任何更改。

以下是我遵循的步骤（几乎所有操作都要以 ``` root ``` 执行）：

### 设置

1. 在文件 ``` /etc/lilo.conf ``` 的 Linux ``` "image" ``` 部分末尾添加一行：
   ```
   append="hdb=ide-scsi",
   ```

   如果你的 CD 刻录机不是 ``` "hdb" ```（第一个 ``` IDE ``` 接口上的第二个驱动器），请调整上面的行。这会让你的 ``` IDE-ATAPI ``` ``` CD-W(R) ``` 在 Linux 系统中被识别为 ``` SCSI ``` 设备。（它实际上不是 ``` SCSI ``` 设备，而是一个 ``` IDE ``` 设备，它伪装成 ``` SCSI ```。）在对 ``` /etc/lilo.conf ``` 进行任何更改后，运行 ``` lilo ```。如果你使用 Linux 内核 ``` 2.2.x ```，则上述更改对于启用 ``` IDE-ATAPI ``` ``` CD-R(W) ``` 上的 ``` SCSI ``` 是必须的。

2. 将循环设备添加到 ``` /dev/ ``` 目录中。这并非强制性的，但它是你创建自己的 CD 时可以享受的一项实用功能。循环设备允许你挂载 CD 镜像（如果它已经是文件系统）以检查其内容。在安装 Linux ``` RedHat ``` 后，我的硬盘上并不存在循环设备，所以我创建了它们：
   ```bash
   cd /dev/
   mknod loop
   ```

3. 在文件 ``` /etc/rc.d/rc.local ``` 的末尾添加两行，以便在系统设置时自动加载内核模块：
   ```bash
   /sbin/insmod ide-scsi
   /sbin/insmod loop
   ```

   这两个内核模块分别用于 ``` IDE ``` 驱动器的 ``` SCSI ``` 仿真以及支持循环设备。

4. 创建或修改设备 ``` /dev/cdrom ```，使其指向正确的设备，最可能是：
   ```bash
   ln -s /dev/sr0 /dev/cdrom
   ```

   你需要这样做是因为你的 ``` "dev/cdrom" ``` 之前指向的是一个 ``` IDE ``` 设备（很可能是 ``` /dev/hdb ```），但现在这些更改将使你的 ``` CD-R ``` 进入 ``` SCSI ``` 仿真模式。

5. 重启系统使 ``` /etc/lilo.conf ``` 生效。检查你的 ``` CD-R(W) ``` 是否仍能正常读取。

6. 从你喜爱的 Linux 软件仓库下载 ``` "cdrecord" ```（例如，``` http://fdirect.linux.org/ ```）。然后安装源码、编译它、安装程序，并创建易于运行的符号链接（如果你能找到二进制 ``` *.rpm ``` 文件，安装将变得简单得多）：
   ```bash
   cd /usr/local
   tar -xvzf /the_path_to_which_you_downloaded/cdrecord-1.6.1.tar.gz
   ls
   cd cdrecord-1.6.1
   make

   make install
   ls /opt/schily/bin/
   ln -s /opt/schily/bin/* /usr/local/
   ```

   程序 ``` cdrecord ``` 是一个刻录 CD 的简易命令行工具。它有几个 ``` GUI ``` 前端，但如果底层的 ``` cdrecord ``` 不支持，这些前端将毫无用处。

7. 检查你的 ``` CD-R ``` 是否处于 ``` SCSI ``` 仿真模式。

### 工具说明

程序 ``` cdrecord ``` 是一个刻录 CD 的简易命令行工具。它有几个 ``` GUI ``` 前端，但如果底层的 ``` cdrecord ``` 不支持，这些前端将毫无用处。

```bash
cdparanoia -B -p "1-2"
```
