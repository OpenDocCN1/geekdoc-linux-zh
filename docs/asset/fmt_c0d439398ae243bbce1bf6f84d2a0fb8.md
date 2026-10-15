
```groovy
pipeline {

  agent any

  stages {

    stage('Build') {

      steps {

        sh 'make'

      }

    }

    stage('Test') {

      steps {

        sh 'test'

      }

    }

    stage('Deploy') {

      steps {

        sh 'deploy'

      }

  }

  }

}
```

上述 `Jenkinsfile` 指示 Jenkins 在任何代理上准备工作空间。`Build`、`Test` 和 `Deploy` 阶段对应了 CI/CD 的概念步骤。`Deploy` 阶段运行一个脚本处理整个部署。在实践中，部署通常会分为多个阶段以获得更好的可见性和控制。

## 26.4 实践

我们现在转向一个假设的示例来说说明到目前介绍的概念。我们构思了一个简单的应用程序 `UlsGo`，它比现实世界中的任何东西都要多。它是完全自包含的，不依赖其他应用程序。

- 工作空间是代理本地磁盘上的位置，包含构建所需的文件，包括源代码和依赖项。每个构建都有私有的工作空间。

### 实践 965

我们的示例包括：

- `UlsGo` Web 应用程序，仅包含一个小功能
- 应用程序的单元测试
- 包含应用程序的 `DigitalOcean` 虚拟机
- 按需创建的单服务器开发环境
- 按需创建的负载多服务器阶段环境
- 将所有部分连接在一起的 CI/CD 流水线

我们在示例中使用了许多流行的工具和服务：

- `GitHub` 作为代码仓库
- `DigitalOcean` 虚拟机和负载均衡器
- `HashiCorp Packer` 用于制作 `DigitalOcean` 镜像
- `HashiCorp Terraform` 创建部署环境
- `Jenkins` 用于管理 CI/CD 流水线

你的应用程序可能使用不同的技术栈，但无论工具如何，通用原理是相似的。

图 C 展示了示例流水线的初始阶段。图表显示了轮询 `GitHub` 以获取 `UlsGo` 项目的新提交。当发现提交时，`Jenkins` 运行单元测试套件。如果测试失败，`Jenkins` 构建二进制文件。如果二进制文件构建成功，流水线继续创建部署产物——`DigitalOcean` 机器镜像。如果任何阶段失败，流水线将报告错误。

### 图 C 展示流水线（第一部分）

![](img/d87305f54c4a442cf382141acae4b84f_1012_0.png)

我们稍后会详细描述部署阶段。但在那时，我们应该回顾初始阶段。

# UsahGo，一个简单的 Web 应用程序

我们的示例应用程序是一个具有单一功能的 Web 服务。它以 JSON 格式返回与本书特定版本关联的作者。例如，以下查询显示了该版本的作者：

```
$ curl usahgo.admin.com/?edition=5

{
  "authors": [
    "Evi",
    "Garth",
    "Trent",
    "Ben",
    "Dan"
  ],
  "number": 5
}
```

我们进行了一些完整性检查，以确保用户不会请求得太离谱，例如请求不合理的版本：

```
$ curl -vs usahgo.admin.com/?edition=6
< HTTP/1.1 404 Not Found
< Content-Type: application/json
{
  "error": "6th edition is invalid"
}
```

我们的应用程序还有一个健康检查端点。健康检查是监控系统询问应用程序“嘿，你运行正常吗？”的一种简单方法。

```
$ curl usahgo.admin.com/health
{
  "health": "true"
}
```

开发者通常与管理员紧密合作，创建 CI/CD 流水线的构建和测试阶段。在这种情况下，由于应用程序是用 Go 编写的，我们可以在流水线中使用标准的 Go 工具（`go build` 和 `go test`）。

# UsahGo 单元测试

单元测试是第一个运行的测试，因为它们在源代码层级运行。单元测试涉及在尽可能细致的粒度上测试应用程序的功能：即它的函数和方法。大多数语言都有提供对单元测试原生支持的测试框架。

# CI/CD 实践

让我们查看 `UsahGo` 的一个单元测试。考虑以下函数：

```go
func ordinal(n int) string {
  suffix := "th"
  switch n {
  case 1:
    suffix = "st"
  case 2:
    suffix = "nd"
  case 3:
    suffix = "rd"
  }
  return strconv.Itoa(n) + suffix
}
```

该函数接受一个整数作为输入，并确定对应的序数表达式。例如，当传入 `1` 时，函数返回 `"1st"`。`UsahGo` 使用该函数来格式化错误信息的文本。单元测试证明了给定某些输入，函数将返回预期输出。这里是执行该函数的单元测试：

```go
func TestOrdinal(t *testing.T) {
  ord := ordinal(1)
  exp := "1st"
  if ord != exp {
    t.Error("expected %s, got %s", exp, ord)
  }
  ord = ordinal(10)
  exp = "10th"
  if ord != exp {
    t.Error("expected %s, got %s", exp, ord)
  }
}
```

该函数接受一个整数作为输入，并确定对应的序数表达式。例如，当传入 `1` 时，函数返回 `"1st"`。`UsahGo` 使用该函数来格式化错误信息的文本。我们可以通过 Go 的内置框架运行测试：

```
$ go test
PASS
ok github.com/bwhaley/ulsahgo 0.006s
```

如果未来应用程序的某些发生了变化——例如对 `ordinal()` 函数进行了更新——测试将报告与预期的偏差。开发者负责在调整代码时更新单元测试。经验丰富的设计的代码是易于测试的。他们的目标是实现每个方法和函数的完全覆盖。

`ordinal()` 函数实现了三个特殊情况和一个通用情况。全套单元测试将执行代码中的这些可能路径。

# 开始使用 Jenkins 流水线

代码准备就绪且单元测试已到位后，CI/CD 之旅的第一步是在 `Jenkins` 中配置项目。GUI 界面引导了这一过程。以下是我们的选择：

- 我们的新项目是一个 `Pipeline` 项目，通过代码定义，而不是通过用户界面定义的传统的“自由风格”项目。
- 我们希望通过 `Jenkinsfile` 与源码仓库一起跟踪流水线，因此在 `Pipeline` 定义中选择“来自 SCM 的 Pipeline脚本”。
- 我们通过轮询 `GitHub` 提交来触发构建。添加凭据以便 `Jenkins` 访问 `UsahGo` 仓库，并配置 `Jenkins` 每五分钟轮询一次 `GitHub`。

初始设置只需要几分钟。在现实生活中，我们将使用 `GitHub Hook` 通知 `Jenkins` 有新提交，从而避免对其 API 进行不调用。

通过这种设置，每当向 `GitHub` 推送新提交时，`Jenkins` 都会执行仓库中 `Jenkinsfile` 描述的流水线。

考虑你的仓库组织方式。在这个项目中，我们选择将 CI/CD 和代码组合在同一个仓库中，并将所有 CI/CD 相关文件保留在 `pipeline` 子目录下。`UsahGo` 仓库的布局如下：

```
$ tree usahgo
ulsahgo
- pipeline
  - Jenkinsfile
    - packer
    - provisioner.sh
    - usahgo.json
    - usahgo.service
  - production
    - tf_prod.sh
    - usahgo.tf
  - testing
    - tf_testing.sh
    - usahgo.tf
ulsahgo.go
ulsahgo_test.go
```

对于像这样的的小型项目，集成结构非常有效。`Jenkins`、`Packer`、`Terraform` 等工具都可以查看 `pipeline` 目录。

# CI/CD 实践

`UlsahGo` 镜像模板仅有一个构建器：

```json
"builders": [
  "type": "digitalocean",
  "api_token": "qj8FsrMI17vqT1B8qqBn9f7XqedJkkJZ7cqJcB105nm06ihz",
  "region": "sfo2",
  "size": "512mb",
  "image": "ubuntu-16-04-x64",
```
