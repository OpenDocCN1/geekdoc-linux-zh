![](bbox=[0.06, 0.09, 0.48, 0.42])

在较长的页面上，你仍然可以看到关于所有可用标签的提示。这些可以是版本号，也可以是像 latest 这样的代码名称或标识符。如果你想要将排序顺序更改为 A-Z，你会看到最旧的版本排在第一个（见图 3）。如果你知道映像的名称，也可以直接构造一个 URL，例如 https://hub.docker.com/~/image-/<tags>。

Listing 6 中的 Bash 函数是这个代码片段的一种替代方案。将 ~/.bashrc 文件和 post-install 脚本中的 skopeo 和 jq 工具（在 Ubuntu 软件包中名称相同）安装。

你可以在所有新的 shell 中使用 dfind 命令来搜索 Docker Hub 上的版本（Listing 7）。

# 文件访问

在容器中运行程序通常只有在你可以访问主机上的文件时才有意义。你可以通过使用虚拟机（VM）轻松使用 Docker，或者简单地使用一种额外的选项形式：

```
`-v <FolderHost>:<FolderContainer>`
```

当调用 Docker 时，在主机上，将你的主目录 /var/home/dir/ 共享给容器，如 Listing 8 的第一行所示。你会看到包括主目录在内的整个目录树，以及 /var/home/dir/ 下的所有子文件夹。

![](bbox=[0.06, 0.42, 0.48, 0.92])

```
Listing 6: dfind
dfind () {
    skopeo inspect docker://$1 \\
    | jq '.RepoTags' | tr -d '\n"'
    | echo;
}
```

```
Listing 7: 调用 dfind
$ dfind fedora
["20", "21", "22", "23", "24", "25", "26", "20-modular", "27", "28", "29", "30", "31", "32", "33", "34", "35", "36", "37", "branched", "heisenbugs", "latest", "modular", "rawhide"]
```