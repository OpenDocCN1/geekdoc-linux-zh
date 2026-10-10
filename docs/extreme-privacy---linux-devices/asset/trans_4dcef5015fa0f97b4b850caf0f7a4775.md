

# 第九章：自定义脚本

我详细介绍过许多加固和清理新 Linux 系统的方法。本章之前所有内容都依赖手动配置。接下来，让我们通过创建自己的 Linux 维护脚本，自动化许多日常或每周任务。我理解有些读者可能只想直接下载一个配置好的脚本并立即使用。以下终端命令将下载该脚本，使其在你的 Linux 机器上可执行，下载快捷方式文件，并将两者移动以在“应用程序”菜单中创建一个“Maintenance”快捷方式。本章的其余部分将解释如何创建你自己的脚本。

```bash
wget https://inteltechniques.com/data/maintenance.sh
chmod +x maintenance.sh
wget https://inteltechniques.com/data/maintenance.desktop
sudo mv maintenance* /usr/share/applications/
```

下一页显示该脚本的完整文本。它标识该文件为 bash 脚本；清除屏幕；并提供一个包含七个可选菜单项的菜单。下图显示了脚本完成并执行后的样子。您需要输入想要执行的功能对应的数字，然后按下 Enter 键。在任何提示符下不输入数字而直接按 Enter 键，会再次显示原始菜单。每个选项对应本指南前面介绍的命令。如果您想修改此脚本，请选择选项“6”以管理员权限启动文件查看器，导航到 `/usr/share/applications` 并编辑 `maintenance.sh` 文件。

![](img/451a8c416cafc58e46802d06b4bc7b1a_81_0.png)

现在，让我们理解如何手动构建这个脚本。使用您自己 Linux 机器上的文本编辑器应用程序，将下一页中展示的所有代码（Courier New 11 点字体）复制到一个新文件中，并将该文件保存为“文档”文件夹内的 `maintenance.sh`。

```bash
#!/bin/bash
clear
COLUMNS=12
PS3='Selection: '
options=(
"Show Hidden Files"
"Hide Hidden Files"
"Start NextDNS"
"Stop NextDNS"
"Restart NextDNS"
"Launch Files with Admin"
"Apply Updates" )
select opt in "${options[@]}"
do
case $opt in
"Show Hidden Files")
gsettings set org.gnome.nautilus.preferences show-hidden-files true
gsettings set org.gtk.Settings.FileChooser show-hidden true
;;
"Hide Hidden Files")
gsettings set org.gnome.nautilus.preferences show-hidden-files false
gsettings set org.gtk.Settings.FileChooser show-hidden false
;;
"Start NextDNS" )
nextdns start
;;
"Stop NextDNS" )
nextdns stop
;;
"Restart NextDNS" )
nextdns restart
;;
"Launch Files with Admin" )
sudo nautilus
;;
"Apply Updates")
sudo apt update
sudo apt upgrade -y
sudo apt full-upgrade -y
pop-upgrade release upgrade
sudo apt autoremove -y
sudo apt autoclean -y
flatpak update -y
;;
esac
done
```

这是一个相当基础的 Bash 脚本，但让我们逐步解析每个部分，以便理解其功能，以便将来可以复制此类脚本。

- `#!/bin/bash`: 第一行被称为'she-bang'。它将文本文件标识为待执行的命令脚本。
- `clear`: 该命令简单清除屏幕，以便呈现干净的菜单。虽然在此脚本中不是必需的，但我喜欢在呈现任何内容前清除屏幕。这消除了可能让观众困惑的其他文本。
- `COLUMNS=12`: 该命令在列中显示内容。它防止菜单选项被显示为单条水平线。如果菜单项不符合预期，您可以修改此数字。
- `PS3='Selection: '`: PS 是 Prompt Statement（提示语句）的缩写。PS3 显示一个选择菜单，您可以选择对应的数字来执行选项。这基本上为脚本中未来项目的选择创建了一个选项。
- `options=("Restart NextDNS")`: 这是放置菜单选项的地方。这些选项的措辞应与我们希望它们在终端中出现的样子完全一致。没有数量限制，且每个选项都应置于各自的引号中。
- `select opt in "${options[@]}"`: 这继续菜单功能。
- `do`: 这开始执行我们的菜单过程。
- `case $opt in`: 这用作 if/then 风格语句的替代方案。它是一种更简单的方式，用于在一个脚本中呈现多个执行的选择，该脚本可以无限循环。
- `"Restart NextDNS" )`: 这标识我们将为其指定命令或命令序列的菜单选项。它应与前面部分列出的选项逐字匹配。
- `nextdns restart`: 这是我们希望在选择菜单项时执行的终端命令。
- `;;`: 这标识所选菜单项内命令的结束。
- `esac`: 该命令（case 的反向拼写）结束我们的 case 语句。
- `done`: 这是脚本的结束。

接下来，您需要在“文档”文件夹中创建一个“maintenance.desktop”文件，该文件告诉操作系统从您的应用程序菜单启动脚本。以下是我使用的代码。

```ini
[Desktop Entry]
Type=Application
Name=Maintenance
Categories=Application;Maintenance
Exec=/usr/share/applications/maintenance.sh
Terminal=true
```

现在，您需要使脚本可执行，并将这两个文件移动到操作系统能够访问且不会碍事的位置。我使用了以下命令。

```bash
cd Documents
chmod +x maintenance.sh
sudo mv maintenance* /usr/share/applications/
```

您现在应该在应用程序菜单中看到一个新的快捷方式选项，标题为“Maintenance”。下图显示了我的示例。点击此快捷方式将启动脚本。我每周启动此脚本来应用所有更新，如下一章所述。

![](img/451a8c416cafc58e46802d06b4bc7b1a_84_0.png)

![](img/451a8c416cafc58e46802d06b4bc7b1a_84_1.png)

### Twilio 清理脚本

我之前解释了 Twilio 是我首选 VoIP 提供商的原因。如果您经常使用 Twilio 号码，手动清理存储在 Twilio 服务器上的数据相当耗时。我拥有一个自动化脚本，代表我执行所有操作，并在需要时提供关于我账户的信息，所有这些都无需登录我的 Twilio 账户。让我们从使用以下步骤安装 Twilio CLI 工具开始。这仅适用于您拥有 Twilio 账户的情况。

- 导航到 `https://github.com/twilio/twilio-cli/releases`。
- 展开最新的“Assets”区域，直到找到一个包含“amd64.deb”文件的条目。
- 下载该文件，例如“`twilio-5.10.0-amd64.deb`”。
- 右键点击下载的文件，选择“Open with Eddy”（使用 Eddy 打开），然后点击“Install”（安装）。

安装完成后，在终端中执行以下命令。

```bash
twilio login
```

这将要求您提供 Twilio SID 和 Token，可以在您的门户中找到。提示时，请提供名称为“CLI”。接下来，执行以下命令。

```bash
twilio profiles:use CLI
```

这将生成适当的配置文件，告诉您的计算机在所有后续命令中使用此配置文件和提供的凭据。现在，您可以使用以下终端命令手动与 Twilio CLI 进行交互。

```bash
twilio phone-numbers:list
twilio api:core:calls:list
twilio api:core:messages:list --properties='sid,from,body'
twilio api:core:recordings:list
twilio api:core:transcriptions:list
```

我们现在可以在一个脚本中自动化清理步骤，该脚本可以使用以下终端命令下载和安装。

```bash
cd ~/Documents
wget https://inteltechniques.com/data/twilio.sh
chmod +x twilio.sh
wget https://inteltechniques.com/data/twilio.desktop
sudo mv twilio* /usr/share/applications/
```

脚本内容显示在下一页中。

```bash
#!/bin/bash
COLUMNS=12
PS3='Selection: '
options=("Fetch Numbers" "Fetch Calls" "Fetch Messages" "Fetch Recordings" "Fetch Transcriptions" "Delete All")
select opt in "${options[@]}"
do
case $opt in
"Fetch Numbers")
twilio phone-numbers:list
;;
"Fetch Calls")
twilio api:core:calls:list
;;
"Fetch Messages")
twilio api:core:messages:list --properties="sid,from,body"
;;
"Fetch Recordings")
twilio api:core:recordings:list
;;
"Fetch Transcriptions")
twilio api:core:transcriptions:list
;;
"Delete All")
twilio api:core:calls:list > ~/Desktop/calls.txt
cd ~/Desktop/ && sed -i '/^SID/d' calls.txt
sed -i 's/ .*//' calls.txt
sed 's/\twilio api\:core\:calls\:remove \\-\-sid /' calls.txt > calls.sh
chmod +x calls.sh && ./calls.sh
rm calls.txt && rm calls.sh
twilio api:core:messages:list > ~/Desktop/messages.txt
cd ~/Desktop/ && sed -i '/^SID/d' messages.txt
sed -i 's/ .*//' messages.txt
sed 's/\twilio api\:core\:messages\:remove \\-\-sid /' messages.txt > messages.sh
chmod +x messages.sh && ./messages.sh
rm messages.txt && rm messages.sh
twilio api:core:recordings:list > ~/Desktop/recordings.txt
cd ~/Desktop/ && sed -i '/^SID/d' recordings.txt
sed -i 's/ .*//' recordings.txt
sed 's/\twilio api\:core\:recordings\:remove \\-\-sid /' recordings.txt > recordings.sh
chmod +x recordings.sh && ./recordings.sh
;;
esac
done
```

