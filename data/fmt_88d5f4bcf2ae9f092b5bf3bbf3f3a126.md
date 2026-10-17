
确保 Docker Compose 正确安装并可访问，对于高效管理多容器应用程序至关重要。系统 `PATH` 的配置错误可能会导致命令无法被识别，即使安装是有效的。通过验证二进制文件位置并在时调整 `PATH`，用户可以避免常见的执行错误。此外，由于较新的 Docker 版本将 Compose 集为子命令（使用 `docker compose` 而不是 `docker-compose`），适应这一变化可确保与现代设置的兼容性。定期更新 Docker 并检查系统配置有助于维护稳定且功能完备的环境。

4. **访问应用程序：** 打开浏览器并访问 `http://localhost:8080`。我们应该能看到“Hello from Nginx and Redis!”的消息。

## 管理应用程序

Docker Compose 提供了多个命令来有效管理我们的应用程序：

**停止应用程序：**要停止运行的容器，请使用：

- `cd myapp`
- `docker-compose down`

**启动应用程序：**要启动运行的容器，请使用：

- `sudo docker compose up -d`

如果显示警告，这是因为 `docker-compose.yml` 文件包含了过时的版本字段。将完成额外的步骤以缓解任何新的错误消息。

## 修复警告：

1. 从 `docker-compose.yml` 中删除版本字段：

   使用 `nano /home/username/myapp/docker-compose.yml` 打开文件

   a. 找到并删除此行（或类似的内容）：

`version: '3.8'`

   b. 保存并退出（CTRL+X，然后 Y，最后是 Enter）。

2. 验证修复：建议运行：`docker compose logs`

警告将不再出现。

## 额外的故障排除步骤：

现在还需要一些额外的步骤：

1. 要检查容器服务是否运行，运行此命令：`sudo docker ps`

如果容器没有运行，这解释了为什么没有日志。

2. 必要时启动容器。如果没有运行的容器，请使用 `sudo docker compose up -d` 启动它们。然后再次检查日志：`sudo docker compose logs`

3. 检查 Compose 文件中的错误。如果容器无法启动，验证 `docker-compose.yml` 文件：`sudo docker compose config`

4. 验证日志命令，正确的命令是：`sudo docker compose logs`

   - **查看日志：**要查看服务的日志，运行：

   - **扩展服务：** 我们可以通过指定实例数量来扩展服务。例如，运行两个 web 服务实例：`docker-compose up --scale web=2`

## 网络与卷

Docker Compose 自动为应用程序创建一个网络，允许容器使用其服务名称相互通信。我们还可以在 `docker-compose.yml` 文件中定义自定义网络和卷。

例如，要创建自定义网络和用于持久数据的卷，请如下所示修改 `docker-compose.yml`：`sudo nano docker-compose.yml`

```yaml
version: "3.8"
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - /html/share/nginx/html
    networks:
      - my_network
    depends_on:
      - redis
  redis:
    image: redis:latest
    networks:
      - my_network
    volumes:
      - redis_data:/
```

在此配置中：

- 为服务创建了一个名为 `my_network` 的自定义网络。

- 为 Redis 服务定义了一个名为 `redis_data` 的卷，用于持久化数据。

-   **测试：** 在部署到生产环境之前，定期在分阶段环境中测试 Docker Compose 设置，以确保一切运行均符合预期。

Docker Compose 是管理多容器应用程序的不可价值的工具，特别是在 Rocky Linux 9 等平台上。通过在单个 YAML 文件中定义我们的应用程序，我们可以轻松地部署、管理和扩展服务。本章提供了一个使用 Nginx 和 Redis 设置简单 Web 应用程序的实用示例，展示了 Docker Compose 提供的易用性和灵活性。

当我们继续探索 Docker Compose 时，可以考虑将其与 CI/CD 流水集成以实现自动化部署，或者通过额外的服务扩展我们的应用程序以满足需求。可能性是无限的，而 Docker Compose 是现代应用程序开发和部署的关键组件。

## 引入 CI/CD 集成章节

为了增强第 12 章的实用性，请包含一个使用 GitHub Actions 将 Docker 集成到 CI/CD 流水的章节。该章节提供了一个示例工作流，用于构建、测试和部署 Docker 化应用程序。

- **定义章节目标：** 在 Docker Compose 章节（第 18 页）之后添加一个名为“将 Docker 与 CI/CD 流水中集成”的新子节。目标是演示如何自动化 Docker 镜像的构建和部署。

- **创建示例应用程序：** 使用 Docker Compose 章节中现有的 Nginx 和 Redis 示例。确保 `docker-compose.yml` 文件存储在 GitHub 仓库中。

- **编写 GitHub Actions 工作流：** 创建一个工作流文件来构建 Docker 镜像推送到 Docker Hub。以下是一个示例工作流：

```yaml
name: CI/CD Pipeline for Docker
on:
  push:
    branches:
      - main
jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Build and push Docker image
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: user/myapp:latest
      - name: Run tests
        run: docker-compose -f docker-compose.yml up -d && docker-compose -f docker-compose.yml logs
      - name: Clean up
        run: docker-compose -f docker-compose.yml down
```

## 列表 2：用于 Docker CI/CD 的 GitHub Actions 工作流

列表2 展示了一个 GitHub Actions 工作流文件，旨在自动化 Docker 化应用程序的 CI/CD 过程。该工作流在代码推送到主分支时触发，并执行一系列步骤，包括检出仓库、登录 Docker Hub、构建 Docker 镜像、进行适当标记并将其推送到远程 Docker 注册表。通过利用 GitHub Actions，此设置确保了最新更改被自动容器化并发布，促进了一致的部署并减少了人工干预。这种集成形成了现代 DevOps 流线的关键部分，增强了应用程序交付的效率、可追踪性和可靠性。

- **4. 将工作流添加到章节：** 在新子节的代码块中包含上述 YAML 文件。解释每一步：

    - Checkout code：克隆仓库。

    - Log in to Docker Hub：使用机密进行身份验证。

    - Build and push：构建并推送 Docker 镜像。

    - Run tests：启动容器并检查日志。

    - Clean up：停止容器以释放资源。

- **5. 提供设置说明：** 指导读者：

    - 创建包含 `docker-compose.yml` 和 `Dockerfile` 的 GitHub 仓库。
