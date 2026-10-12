
```
sudo aa-complain /path/to/profile
```

要将配置文件置于`enforce`模式：

```
sudo aa-enforce /path/to/profile
```

#### 创建`AppArmor`配置文件

`AppArmor`配置文件存储在`/etc/apparmor.d/`。要创建新的配置文件：

1. 生成基本配置文件：

```
sudo aa-genprof /path/to/application
```

2. 运行应用程序并执行典型任务

3. 根据应用程序的行为更新配置文件：

```
sudo aa-logprof
```

4. 保存并强制执行新的配置文件

### 结论

保护`Debian`系统涉及实施多层保护，从基本安全原则到`SELinux`和`AppArmor`等高级访问控制系统。通过遵循本章概述的实践，你可以显著增强`Debian`系统的安全性。

请记住，安全是一个持续的过程。定期审查和更新你的安全措施，了解新的漏洞和威胁，并始终遵循最小权限原则。通过谨慎和适当的配置，你可以维护一个安全和稳健的`Debian`系统。

# 第6章：服务与守护进程

### 介绍`Systemd`

`Systemd`是`Linux`操作系统的现代`init`系统和服务管理器。它已成为许多主要`Linux`发行版的默认`init`系统，取代了如`SysV init`等旧系统。`Systemd`旨在提供更好的进程管理、服务启动并行化以及依赖关系跟踪。

### `Systemd`的关键特性

1. **快速启动时间：** `Systemd`可以并行启动服务，减少整体启动时间。

2. **按需服务激活：** 服务可以仅在需要时启动，从而节省系统资源。

3. **依赖管理：** `Systemd`可以自动处理复杂的服务依赖关系。

4. **一致的管理界面：** 一个统一的命令行工具（`systemctl`）用于管理单元、目标和系统状态。

5. **Journal：** 一个集中式日志系统，收集并管理来自各种来源的日志数据。

6. **资源控制：** `Systemd`可以为服务管理`CPU`、内存和其他资源分配。

### `Systemd`单元

`Systemd`围绕“单元”组织其配置和管理。单元是一个配置文件，描述了服务、挂载点、设备或其他系统组件。最常见的单元类型包括：

- **服务单元：** 定义和管理系统服务。

- **目标单元：** 将其他单元分组以实现特定的系统状态（类似于`SysV init`中的运行级别）。

- **挂载单元：** 控制文件系统的挂载。

- **设备单元：** 管理`Linux`设备树中的设备。

- **套接字单元：** 管理用于服务激活的网络或`IPC`套接字。

- **定时器单元：** 调度任务（类似于`cron`任务）。

#### `Systemd`目录结构

`Systemd`单元文件通常存储在以下目录中：

- `/lib/systemd/system/`：由已安装包提供的单元文件。

- `/etc/systemd/system/`：由系统管理员创建的单元文件，其优先级高于 `/lib/systemd/system/` 中的文件。

- `/run/systemd/system/`：运行时单元文件。

#### 基本`Systemd`命令

以下是使用 `systemctl` 工具的一些基本`systemd`命令：

- `systemctl list-units`：列出所有活动的单元。

- `systemctl list-unit-files`：列出所有已安装的单元文件及其状态。

- `systemctl status [unit]`：显示特定单元的状态。

- `systemctl is-active [unit]`：检查单元是否处于活动状态。

- `systemctl is-enabled [unit]`：检查单元是否已启用以在启动时启动。

### 管理服务：启动、停止、启用和禁用

`Systemd`通过 `systemctl` 命令提供了管理服务的统一界面。本节将介绍控制服务的基本操作。

#### 启动服务

要立即启动服务，请使用以下命令：

#### 停止服务

要停止一个正在运行的服务，请使用以下命令：

```bash
sudo systemctl stop [service_name]
```

例如，要停止 `Apache` Web 服务器：

```bash
sudo systemctl stop apache2
```

此命令将尝试优雅地停止该服务。如果服务未运行，该命令将不会产生任何影响。

#### 重启服务

要重启一个服务（先停止然后启动），请使用以下命令：

```bash
sudo systemctl restart [service_name]
```

例如，要重启 `Apache` Web 服务器：

```bash
sudo systemctl restart apache2
```

当您进行了配置更改并希望应用这些更改，而无需手动停止和启动服务时，这非常有用。

#### 重新加载服务

某些服务支持在不完全重启的情况下重新加载其配置。可以通过以下操作完成：

```bash
sudo systemctl reload [service_name]
```

例如，要重新加载 `Apache` Web 服务器配置：

```bash
sudo systemctl reload apache2
```

并非所有服务都支持此操作。如果某个服务不支持重新加载，它可能会回退到完全重启。

#### 启用服务

启用服务将其设置为在开机时自动启动：

```bash
sudo systemctl enable [service_name]
```

例如，要启用 `Apache` Web 服务器在开机时启动：

```bash
sudo systemctl enable apache2
```

此命令创建必要的符号链接以便在开机时启动服务，但它不会立即启动该服务。

#### 禁用服务

要防止服务在开机时自动启动，请使用：

```bash
sudo systemctl disable [service_name]
```

例如，要禁用 `Apache` Web 服务器在开机时启动：

```bash
sudo systemctl disable apache2
```

这将移除导致服务在开机时启动的符号链接，但如果该服务当前正在运行，它不会停止该服务。

#### 检查服务状态

要检查服务的当前状态，请使用：

```bash
systemctl status [service_name]
```

例如，要检查 `Apache` Web 服务器的状态：

```bash
systemctl status apache2
```

此命令提供有关该服务的详细信息，包括它是否处于活动状态、是否已启用，以及任何最近的日志条目。

#### 屏蔽和取消屏蔽服务

屏蔽服务会阻止其启动，无论是手动启动还是由其他服务启动：

```bash
sudo systemctl mask [service_name]
```

要取消屏蔽服务：

```bash
sudo systemctl unmask [service_name]
```

屏蔽比禁用更为极端，应谨慎使用。

### 运行后台进程

在 `Linux` 系统中，后台进程（也称为守护进程）是在后台持续运行的程序，为系统或用户提供各种服务。了解如何管理这些进程对于系统管理员和高级用户至关重要。

#### 后台进程类型

- **系统守护进程**：这些是启动时随系统一起启动并在系统关闭前持续运行的后台进程。示例包括 `sshd`（`SSH` 服务器）、`crond`（`cron` 守护进程）以及 `systemd` 本身。

- **用户守护进程**：这些是由单个用户启动的后台进程，通常用于特定任务或应用程序。

- **分离进程**：这些是手动从终端“分离”并发送到后台的常规进程。

#### 在后台启动进程

要从命令行在后台启动进程，您可以在命令末尾使用 `&` 符号：

```bash
command &
```

例如：

```bash
long_running_script.sh &
```

这会启动脚本并立即将控制权返回给终端，该进程将在后台运行。

#### 管理后台进程

1. **列出后台任务：**

   使用 `jobs` 命令列出当前 shell 会话中当前的后台任务：

   ```bash
   jobs
   ```

2. **将后台任务带到前台：**

   使用 `fg` 命令后跟任务编号（如 `jobs` 所示）：

   ```bash
   fg %1
   ```

3. **将前台进程发送到后台：**

   按 `Ctrl+z` 暂停当前前台进程，然后使用 `bg` 命令在后台继续执行：

   ```bash
   bg
   ```

4. **终止后台进程：**

   使用 `kill` 命令后跟进程 ID 或任务编号：

   ```bash
   kill %1
   ```

   或者

   ```bash
   kill 1234
   ```

#### `Nohup` 命令

`nohup` 命令用于运行对挂起信号（hangups）免疫的命令，输出到非 tty（终端）：
