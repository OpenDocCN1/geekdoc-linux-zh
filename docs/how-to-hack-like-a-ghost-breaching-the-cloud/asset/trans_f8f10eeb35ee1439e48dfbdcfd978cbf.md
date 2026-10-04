
接下来，我们执行 terraform fmt 命令来格式化 main.tf，然后执行 plan 指令以构建即将对基础设施进行的更改列表，如下所示。你可以看到我们的服务器已安排好使用我们之前定义的属性启动。相当不错。

```
root@Bounce:~/infra# terraform fmt && terraform plan
Terraform will perform the following actions:

  # aws_instance.basic_ec2 will be created
  + resource "aws_instance" "basic_ec2" {
      + ami             = "ami-0039c41a10b230acb"
      + arn             = (known after apply)
      + associate_public_ip_address = (known after apply)
      + instance_type   = "t2.micro"
  }
--snip--

Plan: 1 to add, 0 to change, 0 to destroy.
```

一旦我们验证了这些属性，我们就调用 terraform apply 在 AWS 上部署服务器。此操作还会本地创建一个状态文件，描述我们刚刚创建的当前资源——一台服务器。

如果我们在 AWS 上手动终止服务器并重新启动 terraform apply，它将检测到本地状态文件与我们 EC2 实例当前状态之间的差异。它将通过重新创建服务器来解决此类差异。如果我们想再启动九台具有相同配置的服务器，我们将 count 属性设置为 10 并再次运行 apply。

尝试手动在 AWS（或任何云提供商）上启动和管理 10 台或 20 台服务器，你很快就会把头发染成绿色，把脸涂成白色，并在纽约市街头跳舞。使用 Terraform 的我们其他人只需更新一个数字，如 Listing 3-4 所示，然后在理智中继续我们的生活。

```
# main.tf launching 10 EC2 servers
resource "aws_instance" "basic_ec2" {
  ami          = "ami-0039c41a10b230acb"
  count        = 10
  instance_type = "t2.micro"
}
```

Listing 3-4: 使用 Terraform 创建 10 个 EC2 实例的最小代码

## 调整服务器

我们的服务器到目前为止相当基础。让我们通过设置以下属性来微调它：

- 我们可以通过 SSH 密钥远程管理它，这转化为一个名为 aws_key_pair 的 Terraform 资源。
- 一组防火墙规则——在 AWS 术语中称为安全组——用于控制哪些服务器可以相互通信以及如何通信。这由 Terraform 资源 aws_security_group 定义。安全组需要附加到虚拟私有云（VPC），即一种虚拟化网络。我们只需使用 AWS 创建的默认 VPC。
- 分配给每个服务器的公网 IP。

Listing 3-5 显示了设置了这些属性的 main.tf。

```
# main.tf - compatible with Terraform 0.12 only

# We copy-paste our SSH public key
① resource "aws_key_pair" "ssh_key" {
  key_name  = "mykey"
  public_key = "ssh-rsa AAAAB3NzaC1yc2EAAA..."
}

# Empty resource, since the default AWS VPC (network) already exists
resource "aws_default_vpc" "default" {
}

# Firewall rule to allow SSH from our bouncing server IP only
# All outgoing traffic is allowed
② resource "aws_security_group" "SSHAdmin" {
  name        = "SSHAdmin"
  description = "SSH traffic"
  vpc_id      = aws_default_vpc.default.id
  ingress {
    from_port   = 0
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["123.123.123.123/32"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# We link the SSH key and security group to our basic_ec2 server

resource "aws_instance" "basic_ec2" {
  ami           = "ami-0039c41a10b230acb"
  instance_type = "t2.micro"

  vpc_security_group_ids  = aws_security_group.SSHAdmin.id
  ③ key_name             = aws.ssh_key.id
  associate_public_ip_address = "true"
  root_block_device {
    volume_size = "25"
  }
}
```

```
# We print the server's public IP
output "public_ip" {
  value = aws_instance.basic_ec2.public_ip
}
```

## Listing 3-5: 向 main.tf 添加一些属性

如前所述，aws_key_pair 在 AWS 上注册 SSH 密钥 ①，该密钥在首次启动时注入到服务器中。Terraform 上的每个资源之后都可以通过其 ID 变量引用，该变量在运行时填充——在这种情况下为 aws.ssh_key.id ③。这些特殊变量的结构始终相同：resourceType.resourceName.internalVariable。

aws_security_group 没有什么新颖之处 ②，或许除了对默认 VPC 的引用外，默认 VPC 是 AWS 创建的默认虚拟网络段（如果愿意，可以类比为路由器的接口）。防火墙规则仅允许来自我们的跳板服务器的入站 SSH 流量。

我们启动另一个 plan 命令，以便确保所有属性和资源都符合我们的预期结果，如 Listing 3-6 所示。

```
root@Bounce:~/infra# terraform fmt && terraform plan
Terraform will perform the following actions:

  # aws_instance.basic_ec2 will be created
  + resource "aws_key_pair" "ssh_key2" {
      + id         = (known after apply)
      + key_name   = "mykey2"
      + public_key = "ssh-rsa AAAAB3NzaC1yc2..."
    }

  + resource "aws_security_group" "SSHAdmin" {
      + arn         = (known after apply)
      + description = "SSH admin from bouncer"
      + id          = (known after apply)
--snip--
    }

  + resource "aws_instance" "basic_ec2" {
      + ami                         = "ami-0039c41a10b230acb"
      + arn                         = (known after apply)
      + associate_public_ip_address = true
      + id                          = (known after apply)
      + instance_type               = "t2.micro"
--snip--

Plan: 3 to add, 0 to change, 0 to destroy.
```

## Listing 3-6: 检查属性是否定义良好

Terraform 将创建三个资源。很好。
作为最后一个细节，我们需要指示 AWS 在机器启动并运行时安装 Docker 并启动我们的容器 Nginx。AWS 利用安装在大多数 Linux 发行版上的 cloud-init 包在机器首次启动时执行脚本。这实际上就是 AWS 注入我们之前定义的公钥的方式。此脚本称为“用户数据”。

修改 main.tf 以添加安装 Docker 并执行容器的 bash 命令，如 Listing 3-7 所示。

```
resource "aws_instance" "basic_ec2" {
--snip--
① user_data = <<EOF

#!/bin/bash
DOMAIN="www.linux-update-packets.org";
C2IP="172.31.31.13";

sleep 10
sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
apt update
apt install -y docker-ce
docker run -dti -p80:80 -p443:443 \
 -e DOMAIN="www.customdomain.com" \
 -e C2IP="$C2IP" \
 -v /opt/letsencrypt:/etc/letsencrypt \
 sparcflow/nginx

EOF
}
```

### Listing 3-7: 从 main.tf 启动容器

EOF 块 ① 包含一个多行字符串，使得注入由其他 Terraform 资源产生的值的环境变量变得容易。在此示例中我们对 C2 的 IP 和域名进行了硬编码，但在现实生活中这些将是负责启动后端 C2 服务器的其他 Terraform 资源的输出。

**NOTE** 除了在 Listing 3-7 中对域名进行硬编码外，我们还可以进一步扩展 Terraform 以使用 Namecheap 提供程序自动创建和管理 DNS 记录，例如：https://github.com/adamdecaf/terraform-provider-namecheap。

## 推送到生产环境

我们现在准备好通过简单的 terraform apply 将其推送到生产环境，这将再次输出计划并在联系 AWS 创建请求的资源之前请求手动确认：

```
root@Bounce:~/infra# terraform fmt && terraform apply

aws_key_pair.ssh_key: Creation complete after 0s [id=mykey2]
aws_default_vpc.default: Modifications complete after 1s [id=vpc-b95e4bdf]
--snip--
aws_instance.basic_ec2: Creating...
```

```
aws_instance.basic_ec2: Creation complete after 32s [id=i-089f2eff84373da3d]

Apply complete! Resources: 3 added, 0 changed, 0 destroyed.
Outputs:

public_ip = 63.xx.xx.105
```

太棒了。我们可以使用默认的 ubuntu 用户名和私有 SSH 密钥通过 SSH 连接到实例，以确保一切运行顺畅：

```
root@Bounce:~/infra# ssh -i .ssh/id_rsa ubuntu@63.xx.xx.105

Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-1044-aws x86_64)

ubuntu@ip-172-31-30-190:~$ docker ps
CONTAINER ID   IMAGE          COMMAND
5923186ffda5   sparcflow/ngi...   "/bin/bash /sc..."
```

完美。现在我们已经完全自动化了服务器的创建、设置和调优，我们可以释放内心的野人，复制这段代码以根据需要生成任意数量的服务器，具有不同的防火墙规则、用户数据脚本和其他设置。当然，更文明的方法是将我们刚刚编写的代码封装在 Terraform 模块中，并根据需要传递不同的参数。详情请参阅书籍仓库中 infra/ec2_module，网址为 www.nostarch.com/how-hack-ghost。

我不会在本已密集的章节中逐步介绍重构过程。重构大多是外观上的，例如在单独文件中定义变量、创建多个安全组、在用户数据脚本中将私有 IP 作为变量传递等等。我相信到现在为止你已经具备足够的实践知识，可以从 GitHub 仓库中提取最终的重构版本并尽情使用。

本章的主要目标是向你展示我们如何在恰好 60 秒内启动一个完全功能齐全的攻击基础设施，因为这就是整个操作的威力：自动化可重复性，这是任何点按操作都无法提供的。

我们只需几个命令即可部署攻击服务器：

```
root@Bounce:~# git clone your_repo
root@Bounce:~# cd infra && terraform init
# update a few variables
root@Bounce:~# terraform apply
--snip--

Apply complete! Resources: 7 added, 0 changed, 0 destroyed.
Outputs:

nginx_ip_address = 63.xx.xx.105
c2_ip_address = 63.xx.xx.108
```

我们的基础设施终于准备就绪！
