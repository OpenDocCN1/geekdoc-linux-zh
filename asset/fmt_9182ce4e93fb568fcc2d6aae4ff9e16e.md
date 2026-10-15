
当你完成容器操作后，清理是一个良好的习惯。你可以使用 `podman rm webserver` 删除停止的容器，并使用 `podman rmi httpd-24` 删除其对应的镜像。

## 无根容器与有根容器

到目前为止，我们一直一直在以无根（rootless）模式运行容器。（注：此处提供的原始 OCR 文本存在重复/损坏，此处已根据提供的文本进行处理。）

# 构建与使用容器 417

图 10-6 `podman search` 命令的输出摘录

| 名称 | 描述 |
| --- | --- |
| registry.access.redhat.com/openshift/python-33-rhel | 用于构建和运行...的 Python 3.3平台 |
| registry.access.redhat.com/ubi8/python-27 | 用于构建和运行 Python 2.7 的平台... |
| registry.access.redhat.com/ubi8/python-36 | 用于构建和运行 Python 3.6 的平台... |
| registry.access.redhat.com/ubi8/python-38 | 用于构建和运行 Python 3.8 的平台... |
| registry.access.redhat.com/ubi8/python-39 | 用于构建和运行 Python 3.9 的平台... |
| registry.access.redhat.com/coderna/ubi9-python | rcrhy. registry.access.redhat.com,ubi9/python... |
| registry.access.redhat.com/ubi8/python-31 | registry.access.redhat.com,ubi8/python... |
| registry.access.redhat.com/ubi8/python-31 | 可作为容器镜像... |
| registry.access.redhat.com/hcl7/python-35-rhel | 用于构建和运行...的 Python 3.5 平台 |
| registry.access.redhat.com/hcl7/python-37-rhel | 用于构建和运行 Python 3.7 的平台... |
| registry.access.redhat.com/hcl7/python-34-rhel | 用于构建和运行...的 Python 3.4 平台 |
| registry.access.redhat.com/ubi8/python-30 | 用于构建和运行 Python 3.0 的平台... |
| registry.access.redhat.com/ubi8/python-32 | 用于构建和运行 Python 3.2 的平台... |
| registry.access.redhat.com/coderna/workspaces-python | "Red Hat Codeworks: Python Stack... |
| registry.access.redhat.com/coderna/workspaces-python-ubi8-base | "Red Hat Codeworks: Python Stack... |
| registry.access.redhat.com/rhel7-atomic | Red Hat Linux Atomic Image 是一个... |
| registry.access.redhat.com/rhel7-atmic | Red Hat Linux Atomic Image 是一个... |
| registry.access.redhat.com/rhel7-minimal | Red Hat Linux Minimal Image 是一个... |
| registry.access.redhat.com/rhel7-minimal | Red Hat Linux Minimal Image 是一个... |
| registry.access.redhat.com/rhel7-rhel2 | 包含基本库和工具的基础镜像 |
| registry.redhat.com/ubi8/x61-base | 包含基本库和工具的基础镜像 |
| registry.redhat.io/openshift/python-33-rhel | 用于构建和运行...的 Python 3.3 平台 |

列表中的两个仓库是 `registry.access.redhat.com` 和 `registry.redhat.io`。这些仓库主要包含相同的容器镜像，但某些镜像需要订阅，且仅在 `registry.redhat.io` 中提供。

列表中的另一个常用仓库是 `docker.io`，俗称为 Docker Hub。Docker Hub 拥有一个庞大的公共 Docker 镜像库，适用于多种应用程序和服务，并供全球用户共享。

`podman search` 命令是一个用于在仓库列表中查找镜像的实用工具。例如，执行 `podman search python` 将指示 Podman 在配置的仓库中搜索名称或元数据中包含字符串“python”的镜像。默认情况下，Podman 会搜索所有未配置的仓库。该命令生成的输出部分显示在图 10-6 所示。

为了更深入地了解特定镜像，`inspect` 命令就派上用场了。例如，该命令提供了关于 `httpd-24` 的详细信息：

```
inspect docker://registry.access.redhat.com/ubi9/httpd-24
```

图 10-7 显示了 `inspect` 命令输出的片段落内容。这些数据对于评估特定镜像是否符合你的需求至关重要。

# 418 第 10 章 容器简介

图 10-7 `skopeo inspect` 的部分输出

```
{
  "Created": "2023-07-17T09:45:25.08616492Z",
  "DockerVersion": "",
  "Label": {
    "architecture": "x86_64",
    "build-date": "2023-07-17T09:26:42.51Z",
    "com.redhat.license": "https://www.redhat.com/"
  }
}
```

# 构建与使用容器 419

一个 Containerfile

```
COPY index.html /app/index.html
EXPOSE 8000
WORKDIR /app
CMD ["python", "-m", "http.server"]
```
