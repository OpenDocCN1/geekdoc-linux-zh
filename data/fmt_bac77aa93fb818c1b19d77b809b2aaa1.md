
GitLab 是一个基于 Ruby 的 Web 应用程序，为你的 Git 仓库提供集中化托管服务。我们使用 Omnibus 安装程序安装了开源版本的 GitLab。它是一个集成安装包，结合了所有依赖项和默认设置。安装程序整合了 `Nginx`、`Redis`、`Sidekiq`、`Unicorn` 和 `PostgreSQL`。遗憾的是，带有 Omnibus 安装程序的社区版不支持切换到 `MySQL` 数据库服务器。要使用 `MySQL`，你需要遵循手动安装过程并从源码编译 `GitLab`，以及其他依赖项。

配置文件位于 `/etc/gitlab/gitlab.rb`。这是一个非常长的文件，包含许多参数，并按组件进行分隔。需要关注的重点设置包括 `external_url`（你可以在此设置你的域名）、数据库设置（用于设置外部 `PostgreSQL` 部署）以及邮件服务器设置。如果你选择修改任何设置，将需要使用 `gitlab-ctl reconfigure` 命令重新配置安装。你可以使用 `gitlab-ctl show-config` 命令获取已启用配置列表。

`GitLab Omnibus` 附带了一些额外组件：`GitLab CI`（一种持续集成服务）和 `GitLab mattermost`（`mattermost` 的集成安装版本，提供带有聊天服务器和文件共享的内部通信功能）。`GitLab CI` 默认启用，可以通过 `http://ci.domain.com` 访问。你可以从配置文件中启用 `mattermost`，然后通过 `http://mattermost.your-gitlab-domain.com` 访问它。

## Git 托管

### 更多...

Git 提供了一个内置的 Web 界面来浏览你的仓库。你只需要一个仓库、Web 服务器以及以下命令：

```bash
$ git instaweb --httpd apache2 # 默认使用 lighttpd
你可以在 http://server-ip:1234 访问页面
```

请查看 `GitWeb` 文档获取更多详情：`https://git-scm.com/docs/gitweb`。

### 另见

查看 `GitLab` 安装要求说明：`https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/requirements.md`。

## 向 GitLab 服务器添加用户

我们已经使用 `GitLab` 搭建了我们自己的托管服务器，但它仍然包含一个管理员账户。你可以开始使用该设置并用管理员账户创建新仓库，但设置一个独立的非 `root` 账户是一个好主意。在这份食谱中，我们将涵盖 `GitLab` 服务器的用户管理和访问控制功能。

### 准备工作

确保你已经遵循之前的食谱并安装了 `GitLab` 服务器。

使用你的 `root` 或管理员账户登录 `GitLab`。

在创建用户账户之前，你需要配置邮件服务器。你可以使用外部邮件服务器，例如 `sendgrid` 或 `mailgun`。更新你的 `GitLab` 服务器配置并重新配置服务器使更改生效。

### 如何操作...

`GitLab` 的默认页面是项目页面。即使以 `root` 登录，也会列出相同的页面。要创建一个新用户，我们需要访问管理员区域：

- 要打开管理员控制台，点击屏幕右上角的管理员区域图标。或者，你可以在基础 URL 后添加 `/admin` 来访问管理员区域。

管理员仪表板将向你展示安装详情以及功能和组件列表。左侧菜单将列出所有可用选项。

2. 点击“`Users`”（用户）菜单获取用户账户相关的选项。

3. 接下来，点击大绿色“`New User`”（新建用户）按钮打开新用户表单。

现在填写所需的详细信息，如姓名、用户名和电子邮件。表单看起来如下：

| | |
|---|---|
| `New user` | |
| `Account` | |
| `Name` | * 必填 |
| `Username` | * 必填 |
| `Email` | * 必填 |

4. 你无法在创建用户表单上为新用户账户设置密码。重置密码的链接将发送到指定的电子 ID。新用户可以通过该链接设置密码：

| | |
|---|---|
| `Password` | |
| `Password` | 将生成重置链接并发送给用户。 |
| 用户将在首次登录时强制设置密码。 |

5. 在“`Access`”（访问）部分下，你可以将此用户标记为管理员，并对他创建的项目设置限制：

| | |
|---|---|
| `Projects limit` | `10` |
| `Can create group` | ☑ |
| `Admin` | |

## Git 托管

6. 接下来，在配置文件下，你可以启用某些功能。

7. 现在，点击“`Save`”（保存）按钮。这将你重定向到用户页面。

8. 如果你想编辑用户，点击页面上的“`Edit`”（编辑）按钮。

9. 如果你想删除用户，点击页面上的“`Delete`”（删除）按钮。

10. 如果你想停用用户，点击页面上的“`Deactivate`”（停用）按钮。

## 使用 GitLab 创建仓库

`GitLab` 中常见的任务之一是创建仓库。有两种方法可以：使用 Web 界面或使用命令行。

### 使用 Web 界面

1. 登录你的 `GitLab` 实例。

2. 点击右上角的“`New project`”（新建项目）按钮。

3. 选择“`Create blank project`”（创建空白项目）。

4. 填写项目名称、可见性和描述。

5. 点击“`Create project`”（创建项目）。

### 使用命令行

你也可以在本地创建仓库然后推送到 `GitLab`：

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin@username/project.git
git push -u origin master
```

## 使用 Git hooks 自动化常用任务

Git 最有趣的之一是 hooks。通过 hooks，你可以将任意脚本绑定到各种 Git 事件。当特定事件（例如 `git commit` 或 `git push`）发生时，绑定到该事件的脚本就会执行。

通常，一个事件由多个步骤组成，每个事件都可以附加一个脚本。最常见的步骤是事件前（`pre-event`）和事件后（`post-event`），hooks 在事件前执行，post hooks 在事件后执行。pre 钩（例如 `pre-commit`）通常用于交叉检查更新并可以批准或拒绝实际事件。post 钩（例如 `post-merge`）用于在事件后执行额外的活动，例如在接收到新推送时运行构建过程或发送通知。

每个仓库都包含一个 `.git/hooks` 目录，其中包含示例脚本。你可以通过移除文件名中的 `.sample` 扩展来开始使用这些 hooks。此外，hooks 脚本属于单个仓库实例，不会随着仓库克隆而复制。你需要手动在远程复制这些脚本。内置的示例 hooks 通常使用 shell 脚本，但你可以使用任何脚本语言，例如 `Python` 或 `PHP`。

### 准备工作

我们需要安装一个本地 Web 服务器。我使用的是 `Apache` 安装；你也可以使用你喜喜欢的服务器：

1. 在 `Apache` 下设置一个新的虚拟主机并启用它：

   ```bash
   $ cd /var/www/
   $ sudo mkdir git-hooks-demo
   $ sudo clone ubuntu:ubuntu git-hooks-demo
   $ cd git-hooks-demo
   ```

2. 创建 `index.html` 并向其中添加以下内容：

   ```bash
   $ vi index.html
   ```

   ```html
   <!DOCTYPE html>
   <html>
   <head><title>Git hooks demo</title></head>
   <body>
     <h2>Deployed Manually</h2>
   </body>
   </html>
   ```

3. 创建虚拟主机配置：

   ```bash
   $ cd /etc/apache2/sites-available
   $ sudo cp 000-default.conf git-hooks-demo.conf
   ```

4. 打开虚拟主机配置 `git-hooks-demo.conf`，并将其内容替换为以下内容：

   ```apache
   <VirtualHost :80>
   DocumentRoot /var/www/git-hooks-demo/html
   </VirtualHost>
   ```

5. 在浏览器中访问你的 IP 地址以检查初始版本。

6. 在主目录下初始化 Git 仓库：

   ```bash
   $ cd /
   $ mkdir git-hooks-repo
   $ cd git-hooks-repo
   $ git init
   ```

7. 将 `index.html` 从 根目录拷贝到仓库：

   ```bash
   $ cp /var/www/git-hooks-demo/index.html .
   ```

现在我们已经具备了创建 Git hook 的基本要求。

### 如何实现...
