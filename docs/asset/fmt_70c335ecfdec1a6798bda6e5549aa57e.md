
```
Get27 http://archive.ubuntu.com/jammy-backports/universe/amd64 Packages [28.1 KB]
Get25 http://packagecloud.io/github/lfs/ubuntu-jammy-amd64 Packages [1,654 B]
Get28 http://apt.ln.org/jammy-ltb-colchain-jammy-17 Inleases [6,823 B]
Fetched 5.9 MB in 3 s (2.0 MB/s)
Reading dependency tree ...
Building dependency tree ...
Reading information...
85 packages can be upgraded. Run 'apt list --upgradable' to see them.
sudo apt install linux-for-OSINT-21-day (main) sudo apt-get install poppler-utils --fix-missing
Reading dependency tree ...
Building dependency tree ...
Reading information...
The following additional packages will be installed:
libpopper18
libpopper18-utils
0 upgraded, 0 newly remove, 85 not upgraded.
After this operation, 1.2 KB of additional disk space will be used.
Need to get of archives.
Do you want to continue? [Y/n]
Get1 http://archive.ubuntu.com/jammy-updates/main/libpopper18-amd64 22.02.0-ubuntu0.3 [1,072 KB]
Get2 http://archive.ubuntu.com/jammy-updates/main/libpopper18-utils-amd64 22.02.0-ubuntu0.3 [186 KB]
Fetched 1.25 KB in 1 s (1,533 KB/s)
Setting up configuration, since apt-utils is not installed
Selecting previously unselected package poppler18:amd64
(Metadata for libpopper18:amd64 22.02.0-ubuntu0.3 is already installed.)
Preparing to unpack...
libpopper18:amd64 (22.02.0-ubuntu0.3)...
Unpacking libpopper18:amd64 (22.02.0-ubuntu0.3).
Setting up libpopper18:amd64 (22.02.0-ubuntu0.3)...
Setting up poppler-utils (22.02.0-ubuntu0.3).
Processing triggers for libc-bin (2.35-ubuntu0.3)...
```

首先，让我们安装 `poppler-utils`：

```
sudo apt clean
sudo apt autoclean
sudo apt update
sudo apt-get install poppler-utils --fix-missing
```

## `pdftotext result.txt`

你现在可以回到第 6 天和第 7 天使用那里描述的命令来处理提取的文本。某些情况下，直接使用 `grep` 在 PDF 中更方便。

## 从 PDF 提取图像

此外，`poppler-utils` 允许你从文档中提取图像。

```
$ sudo apt update
sudo apt-get install poppler-utils --fix-missing
Reading dependency tree ...
Building dependency tree ...
Reading information...
The following additional packages will be installed:
libpopper18
libpopper18-utils
0 upgraded, 0 newly remove, 85 not upgraded.
After this operation, 1.2 KB of additional disk space will be used.
Need to get of archives.
Do you want to continue? [Y/n]
Get1 http://archive.ubuntu.com/jammy-updates/main/libpopper18-amd64 22.02.0-ubuntu0.3 [1,072 KB]
Get2 http://archive.ubuntu.com/jammy-updates/main/libpopper18-utils-amd64 22.02.0-ubuntu0.3 [186 KB]
Fetched 1.25 KB in 1 s (1,533 KB/s)
Setting up configuration, since apt-utils is not installed
Selecting previously unselected package poppler18:amd64
(Metadata for libpopper18:amd64 22.02.0-ubuntu0.3 is already installed.)
Preparing to unpack...
libpopper18:amd64 (22.02.0-ubuntu0.3)...
Unpacking libpopper18:amd64 (22.02.0-ubuntu0.3).
Setting up libpopper18:amd64 (22.02.0-ubuntu0.3)...
Setting up poppler-utils (22.02.0-ubuntu0.3).
Processing triggers for libc-bin (2.35-ubuntu0.3)...
```

你现在可以回到第 6 天和第 7 天使用那里描述的命令来处理提取的文本。某些情况下，直接使用 `grep` 在 PDF 中更方便。让我们尝试从 PDF 文件中提取文本并将其保存到单独的文件。我们将使用 `pdftotext` 命令，它是 `poppler-utils`（https://popper.js.org/docs/v2/utils/）的一部分。

# 从 PDF 提取文本

```
$ sudo apt update
sudo apt-get install poppler-utils --fix-missing
Reading dependency tree ...
Building dependency tree ...
Reading information...
...
```

此外，`poppler-utils` 允许你从 PDF 中提取图像。让我们尝试：

$ apt update 

``` 某些情况下，直接使用 `grep` 在 PDF 中更方便。让我们尝试：

```

$ gitpod/workspace/linux-for-OSINT-21-day (main) exiftool Day_12/result.pdf

ExifTool Version : 12.40

File Name : result.pdf

Directory : Day_12

File Size : 1112 Kib

File Modification/Time : 2023-12-17 13:10:51

File Access/Time : 2023-12-17 17:31:59

File Change/Time : 2023-12-17 17:31:59

File Permissions : -rw-r--

File Type : PDF

File Extension : pdf

MIME Type : application/pdf

PDF Version : 1.7

Linearized : Yes

Author : 

Create Date : 2023-12-17 11:43:55

Modify Date : 2023-12-17 13:10:49

Language : en

MP Toolkit : 2.9-3, framework 1.6

Producer : pikeepdf 8.10

Creator Tool : ocrmymdf 15.4 / Tesseract OCR 4.1
