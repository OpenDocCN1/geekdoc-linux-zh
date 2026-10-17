
你将看到配置脚本安装并配置 Oracle Linux Manager，在几分钟内，你就可以将浏览器指向为虚拟访问 Oracle Linux Manager 定义的 IP 地址了。最棒的部分是一切都是通过代码定义的。此配方中创建的所有内容仅为 6 KB！Vagrant 在解决经典的“在我的机器上可以运行”问题方面非常出色。你可以将这 6 KB 代码部署在任何机器（Mac、Windows、Linux 等）上——你只需要 Vagrant 和 VirtualBox。我们可以自动化一些步骤来使其更有用。例如，我们可以自动化创建 Oracle Linux Manager 的第一个用户，自动创建存储库和激活密钥，然后为 OLM 创建客户端并连接到它们。详细介绍所有细节超出了此配方的范围，但如果你感兴趣查看如何实现，我已经将解决方案发布在 GitHub 上——你可以在这里找到：https://github.com/Oracle-Cookbook

# 使用 Packer 修改镜像

Packer 是一个用于创建机器镜像的工具。在此配方中我们将使用 Packer 引用 Oracle Linux 8 作为基础镜像，使用提供程序安装内容，并将带有这些更改的新 OCID 镜像推送到 OCI。

> 注意
> 尽管 OCI 提供了“始终免费”资源，但不包含存储镜像的能力。如果你想遵循此配方，将需要使用付费账户。

## 准备工作

对于此配方，你需要以下内容：

- Oracle Linux own- Packer

## 如何进行

Packer 经常被忽略，因为它看起来如此简单——然而，Packer 是极其强大的。1. 首先，我们将 `oracle` 类型的 `type` 定义在 `packer` 块中。`packer` 的 `type` 如下：

```bash
packer {
  type = "oracle"
}
```

2. 接下来，我们将 `oracle-oci` 的配置到 OCI。详情可以通过 `https://github.com/Oracle-Cookbook` 获取。

图 8.26 – oracle-oci

- 然后，我们需要在 `variables.hcl` 文件中声明所有变量。在这个文件中，我们定义 `type` 如下：

```hcl
variable {
  type = "string"
}
```

图 8.27 – Packer 中引用变量

- 最后，我们在 `variables.hcl` 文件中声明这些变量。输入 `type` 如下：

```hcl
variable "tenancy_oid" {
  type        = string
  description = "OCID of tenancy"
}
variable "compartment_oid" {
  type        = string
  description = "OCID of compartment"
}
variable "fingerprint" {
  type        = string
  description = "Fingerprint for the key pair used: 12:34:56:78:90:ab:cd:ef"
```

图 8.28 – Packer 中的变量声明

- 最后，我们将为变量赋值。我们将它们放在 `variables.auto.pkrvars.hcl` 文件中。它看起来像这样：

```hcl
tenancy_oid           = "ocid1.tenancy.oc1.aaaaaaaaaaaa"
compartment_oid      = "ocid1.compartment.oc1.aaaaaaaaaaaa"
user_oid              = "ocid1.user.oc1.aaaaaaaaaaaa"
subnet_oid            = "ocid1.subnet.oc1.aaaaaaaaaaaa"
availability_domain = "Uoc:US-ASHBURN-AD-3"
region               = "us-ashburn-1"
key_file             = "../oci_api_key.pem"
fingerprint          = "12:34:56:78:90:ab:cd:ef"
```

图 8.29 – Packer 中的变量赋值

- 另一种方法是在 `./oci/config` 中配置你的 OCI CLI。它看起来像这样：

```ini
[DEFAULT]
user=ocid1.user.oc1.<unique_ID>
fingerprint=<your_fingerprint>
key_file=./oci_api_key.pem
tenancy=ocid1.tenancy.oc1.<unique_ID>
region=us-ashburn-1
```

```
user=ocid.user.ocl.<unique_ID>
fingerprint=<your_fingerprint>
key_file=keys/admin.key
pass_phrase=<your_passphrase>
```

## 注意

关于配置 OCI CLI 的完整细节，请参阅此处：https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm

3. 一旦配置好身份验证，就可以开始定义基础镜像。它看起来如下：

```
source "oracle-oci" = "example" {
  ...
  base_image_ocid = "ocid1.image.oc1.iad.aaaaaaaaaaaa"
  image_name = "Oracle Linux 8.8"
  shape = "VM.Standard.E4.Flex"
  shape_config {
    ocpus = 2
    memory_in_gbs = 4
  }
  ssh_username = "opc"
}
```

图 8.30 – 在 Packer 中定义基础镜像

## 注意

要获取 Oracle Linux 8，请访问以下 URL：https://docs.oracle.com/en-us/iaas/images/oracle-linux-8x/。此具有特定区域和特定架构，因此您需要找到适用于 x86 的最新 Oracle Linux 8 镜像（换句话说，寻找名称中不包含 aarch64 的镜像）。

4. 一旦定义了源，您就可以继续在 Packer 上安装并决定在构建过程中要执行的操作。在这种情况下，我们将调用一个配置器（provisioner），以便我们运行一个 shell 命令来安装 Git：

```
build {
  ...
  name = "Oracle Linux 8.8 with Git"
  sources = ["source.oracle-oci.example"]
  provisioner = "shell" {
    inline = ["sudo dnf install -y git"]
  }
}
```

图 8.31 – Packer 配置器

5. 此时，我们已经告诉了 Packer 我们想要使用什么作为我们的源，并描述了我们在构建时想要执行的操作。您的整个文件应该看起来像：

```
packer {
  required_plugins {
    oracle-oci = {
      version = ">> 1.0.4"
      source = "github.com/hashicorp/oracle"
    }
  }
}
source "oracle-oci.ol8u8" {
  tenancy_oid = "${var.tenancy_oid}"
  compartment_oid = "${var.compartment_oid}"
  user_oid = "${var.user_oid}"
  fingerprint = "${var.fingerprint}"
  key_file = "${var.key_file}"
  subnet_oid = "${var.subnet_oid}"
  availability_domain = "${var.availability_domain}"
  region = "${var.region}"
  base_image_oid = "ocid.image.oci1.iad.aaaaaaaaaaaa"
  image_name = "Oracle Linux 8.8"
  shape = "VM.Standard.E4.Flex"
  shape_config {
    ocpus = 2
    memory_in_gbs = 4
  }
  ssh_username = "opc"
}
```
