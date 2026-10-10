
`sudo mount -t efs fs-08945546ab24ce0a5:/ efs`

`sudo mount -t nfs -o nfsvers=4.1,size=104856,wsize=104856,hard,timeout=600,retries=2,nport fs-08945546ab24ce0a5.efs-us-east-1.amazonaws.com: /efs`

接下来，我们将登录 EC2 服务，并使用之前的挂载命令挂载 EFS 数据存储。

- 28. 如果你使用的是 Windows 系统，可以使用 puTTY 软件连接到 AWS EC2 服务实例。首先运行 puTTY generator，将 AWS PEM 文件转换为 puTTY 需要的 PPK 文件。确保 Type Of Key Generate 为 RSA，点击 Load，选择 PEM 文件，然后点击 Save Private Key。给它一个与 PEM 文件相同的文件，但带有 `.ppk` 后缀。

## 第8章 处理测序数据

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_219_0.png)
图 8.34: 选择 EFS 存储

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_219_1.png)
图 8.35: 挂载 EFS 卷

## 第8章 处理测序数据

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_220_0.png)
图 8.36: 关于挂载卷的信息

- 29. 启动 puTTY。在 puTTY 屏幕的 Host Name（或 IP address）字段中输入 `ubuntu@` 符号和 EC2 实例当前的 IPv4 地址。在我们的示例中，它是 `ubuntu@44.203.117.199`（见图 8.37）。

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_220_1.png)
图 8.37: 在 puTTY 中指定主机

- 30. 在 Category 面板中，选择 Connection，然后是 SSH，最后是 Auth。浏览并选择刚从 PEM 文件创建的 PPK 文件（见图 8.38）。

## 第8章 处理测序数据

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_221_0.png)
图 8.38: 在 puTTY 中选择 PPK 文件

- 31. 使用 puTTY 连接 EC2 实例。如果询问 IP 地址，Yes 现在将出现在 EC2 服务的命令行中（见图 8.39）。

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_221_1.png)
图 8.39: 通过 puTTY 成功连接到远程 EC2 实例

- 32. 运行以下命令为 EFS 创建目录：

```bash
sudo mkdir efs
```

- 33. 安装访问 EFS 所需软件：

```bash
sudo apt-get -y nfs-common
```

## 第8章 处理测序数据

屏幕上会出现关于安装进度的消息；完成后，光标将返回提示符。

- 运行第 27 步的挂载命令。每次停止和重启 EC2 服务，都需要重新运行此命令：

```bash
sudo mount -t nfs -o nfsvers=4.1,size=104856,hard,timeout=600,retries=2,nport fs-08945546ab24ce0a5.efs-us-east-1.amazonaws.com/: efs
```
如果安全规则有问题，将收到错误消息：

```
mount nfs: Connection timed out
```
如果 EFS 挂载成功，你收到 Linux Linux 提示符。

- 运行以下命令确认 EC2 现在可以看到并访问 EFS：

```bash
df -h
```
返回以下内容：

```
fs-08945546ab24ce0a5.efs-us-east-1.amazonaws.com: 8G 0% /home/ubuntu/efs
```
命令：

```bash
ls -l
```
返回以下内容：

```
drwx-xr-x 2 root root 6144 Mar 5 02:58 efs
```

- 通过尝试编辑 EFS 上的文件来确保可以写入 EFS：

```
nano efs/test.txt
```
向文件中添加一些文本：

```this is a test
```
按 Ctrl+X 完成文本，要求保存缓冲区时按 Ctrl+Y，然后再次按 Enter 保存到文件名 `efs/test.txt`。如果无法向 EFS 写入或保存文件，请更改权限：

```bash
sudo chmod +w efs/
```

- 创建 `efs/test.txt` 作为写入测试。确认你可以读取写入 EFS 的内容：

```bash
cat efs/test.txt
```

## 第8章 处理测序数据

它应该返回你输入并保存的内容：

```
this is a test
```

从我们的 EC2 实例，我们现在可以成功访问 EFS 文件存储。

### 复制 FASTQ 文件

FASTQ 文件包含来自测序提供者的测序数据。在本次练习中，我们将获取一个公开访问的全基因组测序 FASTQ 文件。该个体是来自 1000 Genomes 项目的项目 NA12878，称为 Utah Woman。该个体的测序数据现在是全球测序中心和生物信息学进行质量控制和基准测试的标准。如果你有想要处理的测序双端 FASTQ 文件，可以使用它们代替获取 NA12878 的数据。

使用 PuTTY ssh 到你的 EC2，挂载 EFS 并输入以下命令：

```bash
cd efs
mkdir -p data/fastq
cd data/fastq
wget -ftp http://ftp.sra.ebi.ac.uk/vol/fastq/SRR622/SRR622457/SRR622457_1.fastq.gz
wget -ftp http://ftp.sra.ebi.ac.uk/vol/fastq/SRR622/SRR622457/SRR622457_2.fastq.gz
```

这些命令将获取 NA12878 全基因组测序的双端序列读取文件。下载将需要几个小时，因为文件很大。在下载期间，你将看到下载进度报告：

```
SRR622457_1.fastq.gz 0%[ ] 0 --KB/s
SRR622457_1.fastq.gz 1<>794.44MB 8.62MB/s eta 1h 55m
```

你可以打开另一个 PuTTY 终端并登录实例，在使用第一个终端下载 FASTQ 时下载第二个 FASTQ 文件。几个小时后下载完成后，你可以看到文件的大小：

```bash
ls -lh
```
显示第一个 fastq 文件为 48 GB，第二个为 67 GB。
```
-rw-rw-r-- 1 ubuntu ubuntu 48G Mar 5 17:36 SRR622457_1.fastq.gz
-rw-rw-r-- 1 ubuntu ubuntu 67G Mar 5 17:22 SRR622457_2.fastq.gz
```

## 第 8 章处理测序数据

| 计费大小 | 监控 | 标签 | 文件系统策略 | 访问点 | 网络 | Ra |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 计费大小：总大小: 6.00 KiB <br> 标准/单可用区大小: 6.00 KiB (100%) 标准-IA/单可用区-IA大小: 0 Bytes (0%) | | | | | | |

![](img/f11d8c1d6b76e74ec2235e2ddebf829b_224_0.png)

图 8.40：观察 EFS 卷的内容

### 安装 Docker 和容器

我们想要运行的一些基因组学软件已经在 Docker 容器中可用。这意味着，我们不需要像在本章之前所示那样安装软件及其依赖项，而是可以直接使用已经安装了软件的现有 Docker 容器。

让我们安装 Docker 以以便可以使用 Docker 容器。在您正在运行的 EC2 服务中，使用以下命令。当询问是否要安装软件包时，输入 Y 表示是。

```
sudo apt update
sudo apt install docker.io
sudo chmod 666 /var/run/docker.sock
```

确保 Docker 已安装。以下命令

```
docker --version
```

应该显示类似于下所示的内容：

```
Docker version 20.10.7, build 20.10.7-ubuntu5-20.04.2
```

运行以下命令

```
docker run hello-world
```

应该显示几行消息，包括这些：
