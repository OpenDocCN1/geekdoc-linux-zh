

## 本地 CDROM

如果您从包装盒中的软盘启动，并使用本地驱动器中的 Red Hat Linux CD-ROM 进行安装，接下来您会看到 **Welcome**（欢迎）对话框；请参见第 10.8 节，*Welcome*（欢迎）。

## NFS 映像

如果您通过网络或 PCMCIA 启动盘启动，并正在从导出 Red Hat Linux CD-ROM（或其镜像）的 NFS 映像服务器进行安装，接下来您会看到 **NFS Setup**（NFS 设置）对话框；请参见第 10.7 节，*Installing over a Network*（通过网络安装）。

## FTP

如果您通过网络或 PCMCIA 启动盘启动，并直接从 FTP 服务器进行安装，接下来您会看到 **FTP Setup**（FTP 设置）对话框；请参见第 10.7 节，*Installing over a Network*（通过网络安装）。

## HTTP

如果您通过网络或 PCMCIA 启动盘启动，并直接从 HTTP Web 服务器进行安装，接下来您会看到 **HTTP Setup**（HTTP 设置）对话框；请参见第 10.7 节，*Installing over a Network*（通过网络安装）。

## 硬盘

如果您从包装盒中的软盘启动，并正在从您先前复制到本地硬盘的 Red Hat Linux 文件进行安装，接下来您会看到 **Select Partition**（选择分区）对话框；请参见第 10.6 节，*Identify Disk Partition to Install From*（确定安装源磁盘分区）。

## 10.6 确定安装源磁盘分区

**Select Partition**（选择分区）屏幕（图 10–6，*Selecting Partition Dialog for Hard Drive Installation*（硬盘安装的选择分区对话框））仅适用于从磁盘分区进行安装的情况（即您在 **Installation Method**（安装方法）对话框中选择了 **Hard Drive**（硬盘））。此对话框允许您命名正在从中安装的磁盘分区。

![](img/eda1471ab4ce718c791c97a85559a478_214_0.png)

输入包含 RedHat 目录树的分区的设备名称。还有一个标有 **Directory holding Red Hat**（包含 Red Hat 的目录）的字段。如果 RedHat 目录不在该分区的根目录中，请输入指向 RedHat 目录的路径（例如，如果 RedHat 目录位于 /test/new/RedHat，则输入 /test/new）。

确定磁盘分区后，接下来您将看到 **Welcome**（欢迎）对话框：现在请转到第 10.8 节，*Welcome*（欢迎）。

## 10.7 通过网络安装

如果您正在执行网络安装，将出现 **Configure TCP/IP**（配置 TCP/IP）对话框；有关此对话框的说明，请前往第 10.13 节 *Configuring a Network Connection*（配置网络连接），然后返回此处。

### 10.7.1 NFS 设置

NFS 设置对话框（图 10–7，NFS 设置对话框）仅适用于从 NFS 服务器进行安装的情况（即您通过网络或 PCMCIA 启动盘启动，并在安装方法对话框中选择了 NFS 映像）。

**图 10–7 NFS 设置对话框**

![](img/eda1471ab4ce718c791c97a85559a478_215_0.png)

输入您的 NFS 服务器的主机名或 IP 地址，以及包含 Red Hat Linux 安装文件或 CD 的导出目录的名称。例如，如果您正在从域名 `redhat.com` 中名为 `east.coast` 的主机进行安装，请在 `NFS Server`（NFS 服务器）字段中输入 `east.coast.redhat.com`。

如果 NFS 服务器将 Red Hat Linux CD 挂载在 /mnt/cdrom 上，请在 Red Hat 目录字段中输入 /mnt/cdrom。如果 NFS 服务器导出的 Red Hat Linux 安装树的镜像而不是 CD，请输入包含 RedHat 目录的目录。例如，如果您的 NFS 服务器包含目录 /mirrors/redhat/i386/RedHat，则输入 /mirrors/redhat/i386。

#### 请注意

如果您正在执行 NFS 安装并正在从 Red Hat Linux CD-ROM 复制文件，请务必检查文件权限，以确保它们为您的安装正确设置。如果没有，您复制的文件将不可执行，您必须在安装之前更改权限。

接下来您将看到 **Welcome**（欢迎）对话框：现在请转到第 10.8 节，*Welcome*（欢迎）。

### 10.7.2 FTP 设置

FTP 设置屏幕（图 10-8，FTP 设置对话框）仅适用于从 FTP 服务器进行安装的情况（即您在安装方法对话框中选择了 FTP）。此对话框允许您识别正在从中安装的 FTP 服务器。

**图 10-8 FTP 设置对话框**

![](img/eda1471ab4ce718c791c97a85559a478_216_0.png)

输入您正在从中安装的 FTP 站点的主机名或 IP 地址，以及该站点中包含适用于您的架构的 RedHat 安装文件的目录的名称。例如，如果 FTP 站点包含目录 `/pub/mirrors/redhat/i386/RedHat`，请输入 `/pub/mirrors/redhat/i386`。

如果所有设置都正确指定，将显示一个消息框，指示正在获取 `base/hdlist`。

接下来您将看到 **Welcome**（欢迎）对话框：现在请转到第 10.8 节，*Welcome*（欢迎）。

### 10.7.3 HTTP 设置

**HTTP Setup**（HTTP 设置）屏幕（图 10-9，*HTTP Setup Dialog*（HTTP 设置对话框））仅适用于从 HTTP 服务器进行安装的情况（即您在 **Installation Method**（安装方法）对话框中选择了 **HTTP**）。此对话框提示您输入有关正在从中安装的 HTTP 服务器的信息。

**图 10-9 HTTP 设置对话框**

![](img/eda1471ab4ce718c791c97a85559a478_217_0.png)

输入您正在从中安装的 HTTP 站点的主机名或 IP 地址，以及该站点中包含适用于您的架构的 RedHat 安装文件的目录的名称。例如，如果 HTTP 站点包含目录 /pub/mirrors/redhat/i386/RedHat，请输入 /pub/mirrors/redhat/i386。如果所有设置都正确指定，将显示一个消息框，指示正在获取 base/hdlist。

接下来您将看到 **Welcome**（欢迎）对话框：现在请转到第 10.8 节，*Welcome*（欢迎）。

## 10.8 欢迎

一旦您选择了语言和键盘，并指定了安装方法，就会显示欢迎对话框（图 10–10）。按确定继续。

**图 10–10 欢迎对话框**

![](img/eda1471ab4ce718c791c97a85559a478_218_0.png)

## 10.9 升级或安装

**Installation Type**（安装类型）对话框（图 10–11，*Installation Type Dialog*（安装类型对话框））为您提供以下五种选择，描述如下。

**图 10–11 安装类型对话框**

![](img/eda1471ab4ce718c791c97a85559a478_219_0.png)

- **Install GNOME Workstation**（安装 GNOME 工作站） – 安装在一个主要用作工作站的系统上。加载 GNOME 图形界面，并配置系统在启动时自动启动 GNOME。安装程序会删除所有现有 Linux 分区中的数据，决定如何为新版本划分磁盘分区，并选择要加载哪些软件包。
  
  > **警告**
  >
  > 如果您正在与 Windows NT 共享磁盘，请不要选择此方法；否则，您将无法启动 Windows NT。LILO 将覆盖 NT 的引导加载器，您将无法启动 NT。您必须执行自定义级安装，并配置 LILO 使其不安装在主引导记录（MBR）上。
  >
  > 要在当前装有 NT 的系统中创建双启动环境，您必须将 LILO 安装在根分区的第一个扇区，而不是 MBR。请务必创建一张启动盘。在这种情况下，您要么使用启动盘，要么配置 NT 系统加载器从根分区的第一个扇区启动 LILO。务必查阅 http://www.linux-doc.org/HOWTO/mini/Linux+NT-Loader.html 以获取有关设置 LILO 和 NT 的更多信息。

- **Install KDE Workstation**（安装 KDE 工作站） – 安装在一个主要用作工作站的系统上。加载 KDE 图形界面，并配置系统在启动时自动启动 KDE。安装程序会删除所有现有 Linux 分区中的数据，决定如何为新版本划分磁盘分区，并选择要加载哪些软件包。
  
  如果您正在与 Windows NT 共享磁盘，请不要选择此方法；否则，您将无法启动 Windows NT。LILO 将覆盖 NT 的引导加载器，您将无法启动 NT。您必须执行自定义级安装，并配置 LILO 使其不安装在主引导记录（MBR）上。
  
  要在当前装有 NT 的系统中创建双启动环境，您必须将 LILO 安装在根分区的第一个扇区，而不是 MBR。请务必创建一张启动盘。在这种情况下，您要么使用启动盘，要么配置 NT 系统加载器从根分区的第一个扇区启动 LILO。务必查阅 http://www.linux-doc.org/HOWTO/mini/Linux+NT-Loader.html 以获取有关设置 LILO 和 NT 的更多信息。

- **Install Server System**（安装服务器系统） – 安装在一个主要用作服务器的系统上。未配置 X 窗口系统，且系统启动时不启动任何图形界面。安装程序删除*所有*现有*任何类型*分区中的*所有*数据，决定如何为新版本划分磁盘分区，并选择要加载哪些软件包。

- **Install Custom System**（安装自定义系统） – 执行自定义安装。您决定所有关于磁盘分区和初始化的事项，要安装哪些软件包，以及如何配置 X 窗口系统和用户界面。

