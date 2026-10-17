
- `/usr/share/ansible/roles/rhel-system-roles.storage.md`。

## 13.11. 使用 STORAGE RHEL SYSTEM ROLE 创建 SWAP 分区的示例 playbook

本节提供了一个 Ansible playbook。该 playbook 应用了存储角色，在块设备上创建交换分区（如果已存在则修改交换分区），使用默认参数。

示例 13.10. 在 `/dev/sdb` 上创建 XFS 的 playbook。

```yaml
---
- name: Create a disk device with swap
- hosts: all
  vars:
    storage_volumes:
    - name: barefs
      type: disk
      disks:
        - /dev/sdb
      size: 15GiB
      fs_type: swap
      mount_point: /opt/barefs
  roles:
  - rhel-system-roles.storage
```

> NOTE

卷名称（示例中的 `barefs`）目前是任意的。存储角色通过 `disks` 下列出的磁盘设备来识别该卷。

额外资源

- `/usr/share/ansible/roles/rhel-system-roles.storage.md`。

## 13.12. 使用 STORAGE ROLE 配置 RAID 卷

使用存储 System Role，可以使用 Red Hat Ansible Platform 在 RHEL 上配置 RAID 卷。在本节中你将学习如何使用可用参数设置 Ansible playbook 以配置满足需求的 RAID 卷。

前提条件

- 在运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> NOTE

你不需要在部署存储解决方案的系统上安装 Red Hat Automation Platform。

- 在运行 playbook 的系统上安装了 `rhel-system-roles` 包。

- 你有一个详细说明要使用存储 System Role 部署 RAID 卷的系统清单文件。

步骤

- 1. 创建包含以下内容的 `playbook.yml` 文件：

```yaml
---
- hosts: all
vars:
  storage_safe_mode: false
  storage_volumes:
    - name: data
      type: raid
      disks: [ssd, sde, sdf, sdg]
      raid_level: raid
      raid_chunk_size: 32 KiB
      mount_point: /mnt/data
  state: present
roles:
  - name: rhel-system-roles.storage
```

> WARNING

设备名称在某些情况下可能会发生变化，例如向系统添加新磁盘时。因此，为了防止数据丢失，我们不建议在 playbook 中使用特定的磁盘名称。

- 2. 可选。验证 playbook 语法。

```bash
#### ansible-playbook --syntax-check playbook.yml
```

3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file /path/to/file/playbook.yml
```

其他资源

- 管理 RAID。

- `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.13. 使用存储系统角色配置带 RAID 的 LVM 池

使用存储系统角色（storage System Role），你可以通过 Red Hat Ansible Automation Platform 在 RHEL 上配置带有 RAID 的 LVM 池。在本节中，你将学习如何使用可用参数设置 Ansible playbook，以配置带有 RAID 的 LVM 池。

### 前提条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意：

> 你不需要在想要部署存储解决方案的系统上安装 Red Hat Ansible Automation Platform。

- 你在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。

- 你有一个清单文件，详细列出了你想要使用存储系统角色配置带 RAID 的 LVM 池的系统。

### 步骤

- 1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
- hosts: all
vars:
  storage_safe_mode: false
  storage_pools:
  - name: my_pool
    type: lvm
    disks: [sdh, sdi]
    raid_level: raid1
  volumes:
  - name: my_pool
    size: "1 GIB"
    mount_point: "/mnt/app/shared"
    fs_type: xfs
    state: present
  - name: rhel-system-roles.storage
```

> 注意：

> 要创建带 RAID 的 LVM 池，必须使用 `raid_level` 参数指定 RAID 类型。

- 2. 可选。验证 playbook 语法。

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file /path/to/file/playbook.yml
```

其他资源

- 管理 RAID。

- `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件

## 13.14. 使用存储角色创建 LUKS 加密卷

你可以通过运行 Ansible playbook 来创建并配置使用 LUKS 加密的卷。

### 前提条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意：

> 你不需要在要在想要创建卷的系统上安装 Red Hat Ansible Automation Platform。

- 你在 Ansible 控制器上安装了 `rhel-system-roles` 软件包。

- 你有一个清单文件，详细列出了你想要使用系统存储角色部署 LUKS 加密卷的系统。

### 步骤

- 1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
hosts: all
vars:
  storage_volumes:
  - name: barefs
    type: disk
    disks:
    - sdb
    fs_type: xfs
    fs_label: label_name
    mount_point: /mnt/data
    encryption: true
    encryption_password: your-password
    roles:
  - rhel-system-roles.storage
```

- 2. 可选：验证 playbook 语法：

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file/path/to/file/playbook.yml
```

其他资源

- 使用 LUKS 加密块设备

- `/usr/share/ansible/roles/rhel-system-roles/storage/README.md` 文件

## 13.15. 更多资源

- `/usr/share/doc/rhel-system-roles/storage/`

- `/usr/share/ansible/roles/rhel-system-roles.storage/`

## 第 14 章 使用 RHEL 系统角色配置时间同步

使用 `timesync` RHEL 系统角色，你可以通过 Red Hat Ansible Automation Platform 在多个目标机器上管理时间同步。

## 14.1. TIMESYNC 系统角色
