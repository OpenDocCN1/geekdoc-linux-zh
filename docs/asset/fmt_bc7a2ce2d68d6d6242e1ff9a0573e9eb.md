
这种方法为任何部署在 LinuxONE 上的 MongoDB 容器方案提供了一个快速、高可扩展的环境来开展工作。

## 8.4 在 LinuxONE 上部署 Hyperledger (区块链)

随着开源 Linux 操作系统的出现，带来了极其丰富的开源资源。开源领域的最新创新是区块链。区块链是一种特定的网络，成员在其中跟踪和交换数字资产。共享账本包含了所有网络交易的单一记录，并在所有网络成员中进行复制。区块链应用程序包含自执行合约以及通过 SDK 或 API 与网络进行交互的客户端应用程序。

由于 LinuxONE 是最安全的平台，它允许用户围绕开源技术的尖端解决方案进行 DevOps 创新。LinuxONE 提供了卓越的安全性、性能以及持续更高的交易编码速度。在为链生成数字签名或哈希加密时，LinuxONE 使用加密加速器。

本节介绍如何在 LinuxONE 环境上部署 Hyperledger Fabric。

### 8.4.1 环境

本节描述了如何为 Hyperledger Fabric 开发设置一个自包含的开发环境。此示例使用 LinuxONE 上的 Ubuntu 16.04 LTS 作为部署 Hyperledger fabric 的操作系统。

可以使用两种方法部署 Hyperledger 及其安全服务：

- 将 Hyperledger Fabric 和成员服务作为守护进程部署在宿主机系统中。
- 将 Hyperledger Fabric 及其成员服务作为 Docker 容器部署在宿主机系统中。

本节展示了将 Hyperledger Fabric 作为 Docker 容器部署。Hyperledger 需要安装以下组件：

字体 Go 编程语言
- RocksDB
- Hyperledger Fabric:
  - peer 守护进程
  - 成员与安全服务

## Docker 部署

Hyperledger fabric 依赖 Docker 在 peer 节点上部署和启动链码。Docker 部署见第 139 页第 8.2 节“在 Ubuntu 16.04 LTS 上设置 Docker”，本节假设 Docker 已成功部署并配置。如前，Docker 需要使用存储驱动程序进行管理。示例 8-15 显示了 docker 部署验证命令。

示例 8-15 Docker 部署验证

```
itsoadmin@itsblockchain:$ sudo usermod -aG docker itsoadmin

itsoadmin@itsblockchain:$ docker version

Docker version 1.12.1, build 87cff1
```

## Docker Compose

对于 Hyperledger 容器，我们使用 `docker-compose` 命令运行 Hyperledger 和成员并启动本地环境，如示例 8-17 所示。

示例 8-17 Docker Compose

```
itsoadmin@itsblockchain:$ docker-compose --version

docker-compose version 1.8.1, build 87c6
```

```
*) echo "No Architectural Images Available for Architecture: $arch - Please call ibm service"
return
esac

cat baseimage/Dockerfile.in | sed -e "s/$_ARCH_TAG/\$ARCH_TAG/g" > baseimage/Dockerfile
root@blockchain:/opt/fabric-images/docker-compose#
```

```
root@blockchain:/opt/fabric-images/docker-compose# setenv.sh
```

# 部署 Hyperledger docker 镜像

为 hyperledger docker 容器设置好环境变量后，如示例 8-21 所示执行 `docker-compose` 命令。

示例 8-21 从 GitHub 克隆 Hyperledger 代码

```
root@blockchain:/opt/fabric-images/docker-compose# docker-compose -f single-peer-ca.yaml up

Creating "docker-compose_default"

Pulling membersrvc from ibmchain/fabric-membersrc:s390x-0.6.1-preview...

s390x-0.6.1-preview: Pulling from ibmchain/fabric-membersrc

9398b634d3: Already exists

49fed44906a: Already exists

19041918bb72: Already exists

elac9a102ef2: Already exists

de63481df23: Already exists

8e573d68bt7a: Already exists

5cbd557c1aeae: Already exists

f643e2ad6f3: Already exists

al2b60e47f41: Already exists

5c487fe8680: Already exists

e8d30cc691c: Already exists

Digest: sha256:b62d3f0e326b6648b9e66bbb9c4c43e8e208a9fc280b9287e03146f2e6a3b

Status: Downloaded newer image for ibmchain/fabric-membersrc:s390x-0.6.1-preview

Pulling up from ibmchain/fabric-peer:s390x-0.6.1-preview...

s390x-0.6.1-preview: Pulling from ibmchain/fabric-peer

: Already exists

49fed44906a: Already exists

19041918bb72: Already exists

elac9a102ef2: Already exists

de63481df23: Already exists

8e573d68bt7a: Already exists

5cbd557c1aeae: Already exists

f643e2ad6f3: Already exists

al2b60e47f41: Already exists

5c487fe8680: Already exists

0ffd252fd19: Already exists

Digest: sha256:82e3200e13b3if6fba5aad9f2c4c43e8e208a9fc280b9287e03210346f2e6a3b

Status: Downloaded newer image for ibmchain/fabric-peer:s390x-0.6.1-preview
```

```
Building image

Step 1/1 FROM ibmchain/fabric-peer:s390x-0.6.1-preview

---> 7412ad95128
```

由于 base 服务已存在，因此已成功构建。若要重新构建此镜像，警告：你必须使用 "`docker-compose build`" 或 "`docker-compose up --build`"。

Creating dockercompose_baseimage_1
Creating dockercompose_membersrvc_1
Creating dockercompose_vp_1
Attaching to dockercompose_baseimage_1, dockercompose_membersrvc_1, dockercompose_vp_1

`docker-compose` 命令会自动启动节点和 membersrvc 的 peer 验证。除了 peer membersrvc 可执行文件外，还创建了用于开发的 Docker 镜像（参见示例 8-22）。

示例 8-22 Hyperledger fabric 和 membersrvc 执行日志

```
membersrvc_1 | 11:39:24.946 [server] -> INFO 001 CA Server

(0.6.1-preview-snapshot-e4ab47)

membersrvc_1 | 11:39:24.954 [caCa] -> INFO 002 Fresh start; creating databases, key pairs, and certificates.
```
