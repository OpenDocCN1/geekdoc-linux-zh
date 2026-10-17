
- Taiga 主页 [taiga.io](https://taiga.io)

软件已经渗透到日常生活中几乎一切事物中。但软件开发也存在其自身的问题，其中一个主要问题是度量——其无形输出使得管理变得困难。一项任务看起来可能很容易，但很难判断在编码时可能会遇到哪些问题，尤其是在拥有多个组件的分布式架构中。那么，如何才能克服这一难题呢？

随着敏捷开发方法的出现，这个问题得到了解答。敏捷方法专注于最终产品，但缺乏优秀的开源且专注于敏捷的工具——大多数现有工具较旧，只是经过简单修改以支持双峰模型（`biome`）。直到 Taiga 的出现。Taiga 是一款基于开源的敏捷项目管理（`PM`）工具。其名称源自一种森林生态系统（`biome`），旨在成为生态系统——即你的项目和你的团队——的中心，并采用其全新的用户界面和基于敏捷的布局。让我们从在 Ubuntu 14.04 上安装它开始本教程，然后进一步了解其内部结构。此处的安装适用于开发服务器。Taiga 网站上另有不同的生产服务器安装流程。

## 01 安装

Taiga 有三个主要组件需要分别安装。

- `Taiga-back`：后端部分（同时也支持 API）。
- `Taiga-front`：前端部分。
- `Taiga-events`：WebSocket 网关。完全可选，对于一般的项目管理目的并非必需。我们将跳过这一部分。

在开始进行 Web 前端操作之前，我们需要后端运行起来。Taiga 的后端有多个依赖项，如开发头文件、C 编译器以及其他包。首先，运行以下命令来安装所有依赖项。

```bash
sudo apt-get install -y build-essential binutils-doc autoconf flex bison libjpeg-dev
sudo apt-get install -y libfreetype6-dev zlib1g-dev libwmf-dev libgdmb-dev libncurses5-dev
sudo apt-get install -y automake libtool libffi-dev curl git tcl tcl-dev
```

Taiga 使用 PostgreSQL 9.3+ 作为数据库，因此请安装数据库：

```bash
sudo apt-get install -y postgresql-9.3 postgresql-contrib-9.3
sudo apt-get install -y postgresql-doc-9.3 postgresql-server-dev-9.3
```

现在设置初始用户和数据库。此命令将创建一个名为 `taiga` 的用户，然后在 `taiga` 用户下创建一个名为 `taiga` 的数据库。

```bash
sudo -u postgres createuser taiga
sudo -u postgres createdb taiga -O taiga
```

## 02 安装 Taiga-back

现在让我们设置 Python 环境。您还需要安装 `virtualenvwrapper` —— 一组扩展，通过在隔离的虚拟环境中运行第三方库，确保您的系统不会杂乱无章。

运行以下命令来安装 Python 和 `virtualenvwrapper`。然后重启您的 shell 以重新加载包含 `virtualenvwrapper` 变量和函数的 bash。

```bash
sudo apt-get install -y python3 python3-pip python-dev python3-dev python-pip virtualenvwrapper
sudo apt-get install libxml2-dev libxslt-dev
```

从 GitHub 下载 Taiga 后端代码并运行以下命令。当前目录将更改为 `taiga-back`：

```bash
cd ~
git clone https://github.com/taigaio/taiga-back.git taiga-back
cd taiga-back
git checkout stable
```

使用以下命令创建一个名为 `taiga` 的新虚拟环境：

```bash
mkvirtualenv -p /usr/bin/python3.4 taiga
```

然后安装后端的依赖项：

```bash
pip install -r requirements.txt
```

用示例数据填充数据库；这还将创建一个密码为 `123123` 的管理员用户 `admin`：

```bash
python manage.py migrate --noinput
python manage.py loaddata initial_user
python manage.py loaddata initial_project_templates
python manage.py loaddata initial_role
python manage.py collectstatic --noinput
python manage.py sample_data
```

现在您可以运行服务器了。请记住，`workon` 命令会启用 `taiga` 虚拟环境：

```bash
workon taiga
python manage.py runserver
```

完成后，您应该能够通过以下地址查看代表完整端点列表的 JSON：`http://localhost:8000/api/v1/`。

## 03 安装 Taiga-frontend

现在让我们完成 Taiga 前端的安装。Taiga 在前端使用了除了 CSS/HTML/JavaScript 以外的语言，因此在浏览器能够完全理解之前，确实需要对其进行构建。

下载 Ruby 和 Gems。在使用最后一个命令设置路径后，使用以下命令重启 shell：

```bash
sudo apt-get install --ruby
gem install --user-install sass scss-lint
export PATH=~/gem/ruby/1.9.1/bin:$PATH
```

现在使用以下命令完成 NodeJS 的安装：

```bash
sudo apt-get install --nodejs npm
```

然后运行 `node` 命令以检查该命令是否被识别。如果没有，请运行：

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

现在安装 `gulp` 和 `bower`：

```bash
sudo npm install -g gulp bower
```

…然后获取代码并编译 `taiga-frontend`：

```bash
cd ~
git clone https://github.com/taigaio/taiga-frontend.git taiga-frontend
cd taiga-frontend
git checkout stable
```

使用以下命令进行编译：

```bash
npm install
bower install
gulp
```

现在运行 `gulp`：

```bash
cd ~/taiga-frontend
npm install
```

如果在运行 `gulp` 时遇到 `npm` 错误，请清除临时文件并重新安装所有依赖项。

```bash
rm -rf ./npm*
rm -rf node_modules
npm install
bower install
gulp
```

如果成功，您现在应该能够在 `http://localhost:9001` 看到 Taiga。

## 04 创建项目和用户故事

既然 Taiga 现在已在您的浏览器中运行，下一步是创建一个项目。我们已经有创建的 `admin` 用户，密码为 `123123`，因此使用这些凭据登录 Taiga 并单击“创建项目”。然后选择 Scrum 模板并单击“下一步”。最后，填写相关详细信息（名称和描述）并单击“创建”。这将带您进入项目待办事项列表（`Project Backlog`）页面。在页面的上半部分，您有燃尽图；下半部分是用户故事列表。在右侧边栏中，您可以看到 Sprint（冲刺）部分。按照通常的做法，让我们先开始创建用户故事，因为对于初学者来说，敏捷开发方法论要求从用户的角度将软件功能分解为更小的单元。这些单元在敏捷术语中称为用户故事。

> Sprints 具有预定义的时间段，通常是两到三周

要添加用户故事，只需单击页面下半部分的“添加新的用户故事”。在下一页中，填写详细信息。请注意，您可以通过此页面为用户故事分配项目点数。您也可以使用批量插入按钮（位于“添加新的用户故事”按钮旁边）一次添加多个故事，并且不要忘记将您的 `admin` 密码更改为易于记住的内容！

## 05 创建 Sprints

既然用户故事已经可用，让我们规划一下 Sprints（冲刺）。如您所知，sprints 是预定义的时间段，通常是两到三周。在 sprint 开始之前，开发人员承诺在 sprint 结束时完成一组用户故事。当 sprint 结束时，scrum 主管审视情况并决定下一个 sprint 的用户故事，此周期继续。
