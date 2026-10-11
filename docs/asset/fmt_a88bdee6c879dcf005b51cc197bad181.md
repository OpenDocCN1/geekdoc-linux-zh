
- 点击选择你想要同步的目录（安卓上允许你选择下载文件夹以外的任何目录）。

- 3. **确保在你点击想要同步的目录处开启了“接收 (RECEIVE)”开关，这样它才能进行备份。**

动态连接失败：我选择“dynamic”作为一个例子，说明了在知道自己位置的情况下使用自动发现 更好。我选择了动态，它连接了并正常工作。当断开网络时，安卓同步 App 中的设备显示我已断开连接，“文件夹”选项卡显示设备为空闲，而 Web GUI 同步显示“未同步”，且远程设备显示我的手机为“已断开”。

如果你遵循了我用于同步的设置，请在添加设备时填写“地址 (Address)”。

```
tcp://192.168.5.5:22000
```

或者

```
tcp://androidstuff.home.arpa:22000
```

格式为 `tcp://`，然后是你的 IP 地址，最后的 `:22000` 是端口号。

不需要勾选“引入新设备 (Introduce new devices)”。

你是否在开头使用了 `tcp://` 并在结尾使用了 `:22000` 作为端口？你这样做效果会更好！

![](img/63f12be029370b8891d876ebe7b9f412_240_0.png)

保存并继续。

## 8. 在 Ubuntu 服务器上批准连接

- 返回 Ubuntu 服务器 Web 界面。

- 你应该看到一个添加新设备的提示。

- 验证设备 ID 与你的安卓设备匹配。

- 点击“添加设备 (Add Device)”。

- 为安卓设备设置一个名称（例如，“Android Phone”）。

- 点击“保存 (Save)”。

## 9. 检查连接

- 在设备上，检查另一个设备是否显示为已连接。连接可能需要几秒钟才能建立。

> 注意：确保 Ubuntu 服务器的防火墙已开放端口 `22000`（或你配置的 Synthing 端口），以允许来自本地局域网的入站连接。默认情况下，首次启动 Ubuntu Server 时 `ufw` 不运行也不会拦截内容，但以后可能会发生变化，就像他们偷偷引入预装某个版本 Docker 的建议一样。真美 : )

现在你已经将你的 Ubuntu 服务器 Syncthing 实例添加到了手机上：无需开启端口，只要你连接了 WiFi 并开启 VPN，端口就会同步，并持续备份你的手机。

记住——**不要将“地址 (ADDRESSES)”设置为“动态 (DYNAMIC)”——点击“DYNAMIC”并将其替换为 `tcp://youripaddress:22000`，将 `youripaddress:22000` 中的 `youripaddress` 替换为运行同步服务的虚拟机的 IP 地址。**

![](img/63f12be029370b8891d876ebe7b9f412_241_0.png)

## 步骤 6：为有序的安卓备份配置 Syncthing

### 6.1 配置安卓 Syncthing App

- 1. 在安卓设备上打开 Syncthing。

- 2. 在应用文件夹部分，点击每个文件夹右上角的加号图标。

- 点击应用文件夹部分右上角的加号。

- 点击文件夹标签并命名。

- 点击选择你想要同步的目录（安卓上允许你选择下载文件夹以外的任何目录）。

- 3. **确保在你点击想要同步的目录处开启了“接收 (RECEIVE)”开关，这样它才能进行备份。**

## 0.4 安装 Docker Compose

Ubuntu 的 `docker-compose-plugin` 是安全的，它不是 snap 粘合剂。

```bash
sudo apt install docker-compose-plugin -y
sudo systemctl enable --now docker
```

## 0.5 验证安装

运行 `docker compose version` 并确保版本为 2.0 或更高。运行 `docker --version` 并确保版本为 24.0.0。

## 0.6 设置权限：

某些操作需要以 root 身份运行 Docker，但你可以将你的用户添加到 docker 组以避免一直使用 `sudo`。说明一下，mailcow 的文档（https://docs.mailcow.email/started/install/#ck-selinux-specific）和社区（https://community.mailcow.email/d/59-mailcow-containers-running-as-root）建议从 root 或 sudo 开始，你对他们的信任程度应该超过对我的。引用 mailcow 开发者的话：“作为非 root 用户控制 Docker 守护进程不会为你提供额外的安全性。无权限用户同样会以 root 身份启动容器。栈的行为是完全相同的。”运行此命令添加你的用户：

```bash
sudo usermod -aG docker $USER
```

注销并重新登录，或者运行：`newgrp docker`

## 步骤 1：仅安装 ONLYOFFICE Workspace 社区版

遵循正确的步骤非常重要。ONLYOFFICE 网站是一片文档的雷区，会导致像这样这样的安装失败，即使你遵循了他们的指令：

![](img/63f12be029370b8891d876ebe7b9f412_245_0.png)

或者

## 这就是你遵循他们的安装说明后受到的惩罚，结果不仅不起，而且它还建议你等待，尽管按下 F12 并查看控制台可以清楚看到这永远不会加载。

请不要刷新页面或关闭你的电脑。

![](img/63f12be029370b8891d876ebe7b9f412_246_0.png)

你正在处理了，别撒谎了兄弟

![](img/63f12be029370b8891d876ebe7b9f412_246_1.png)

## louis_androidstuff:-/programs$ sudo bash workspace-install.sh -md "louishomeserver r.com"

## 这个命令看起来熟悉吗？

ONLYOFFICE Workspace

在云端尝试

正在运行 ONLYOFFICE Workspace 的完整安装

> 备注：请注意，所有安装操作必须以 root 权限执行。

> 你可以一次安装所有 ONLYOFFICE Workspace 组件和模块。要这样做，请运行以下命令：

```bash
bash workspace-install.sh -md "yourdomain.com"
```

为了避免上述的开源地狱，我们通过安装以下内容 SSH 登录：

- SSH 登录到我们在 `192.168.5.5` 创建的 androidstuff 虚拟机

```bash
ssh username@192.168.5.5
```

- 下载 ONLYOFFICE Workspace 安装脚本：

```bash
wget https://download.onlyoffice.com/install/workspace-install.sh
```

3.  true脚本具有可执行权限：

```bash
chmod +x workspace-install.sh
```

这更改了文件权限以允许执行。

4. 运行安装脚本：

```bash
sudo bash workspace-install.sh -it WORKSPACE -md fakedomainname.com
```

将 `fakedomainname` 替换为你在邮箱部分实际的域名。你也可以省略 `-md` 且不安装它。

> 警告：OnlyOffice 网站文档中的指令会导致安装失败。请使用上面的命令行以便它能够正常工作。

5. 一旦完成，访问 http://192.168.5.5 (http://192.168.5.5/) 登录。

6. 它将提示你创建一个用户名和密码。去操作吧。

7. 登录后，制作一个 HTTPS SSL 证书，以便我们可以通过 HTTPS 登录：

进入控制面板，主屏幕上的大图标。

- 进入左侧菜单顶部 HTTPS。

- 点击生成并应用（Generate and apply）。

- 享受吧。

## 步骤 2：本地文件访问

一旦进入，你就可以设置一切了。根据许可条款输入密码，就可以使用了。我建议进入管理设置并设置 HTTPS - 它将为你生成一个自签名证书！

## 2.1 深入“开源化”软件

你可以打开一个示例文档。但如果我想让这个工作空间访问存储在服务器上的文件呢？？我想打开这台电脑上的文档；这正是有趣开始的地方。）

![](img/63f12be029370b8891d876ebe7b9f412_248_0.png)

## 2.2 用于本地文件访问的兔子洞

那么，你要去哪里呢？“与我共享”、“收藏”、“理由”、“私有房间”、“项目常用”以及“邀请用户加入门户”。也许是设置？让我们试试看。管理员配置设置、控制面板，以及……噢，看，“存储”！

> 开源：你无法从你的服务器打开文档。这不是一个功能。你需要一个 WebDAV 服务器。欢迎来到开源世界！
