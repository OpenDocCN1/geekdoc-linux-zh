
此文件描述了每个 Web 服务器上分区、卷组和逻辑卷的预期结构。第一个分区从 `/dev/vdb` 设备开始的偏移 `1 MiB` 处开始，在偏移 `257 MiB` 处结束，总大小为 `256 MiB`。

每个 Web 服务器有一个名为 `apache-vg` 的卷组，包含 `/dev/vdb` 设备的第一个分区。

每个 Web 服务器有两个逻辑卷。第一个逻辑卷名为 `content-lv`，大小为 `64 MiB`，挂载到 `apache-vg` 卷组，并挂载在 `/var/www`。第二个逻辑卷名为 `logs-lv`，大小为 `128 MiB`，挂载到 `apache-vg` 卷组，并挂载在 `/var/log/httpd`。

# 第 10 章 | 自动化 Linux 管理任务

> 注意
`apache-vg` 卷组的容量为 `256 MiB`，因为它由 `/dev/vdb1` 分区支持。它为两个逻辑卷提供了足够的容量。

## 3.2. 修改 `storage.yml` playbook 中的第一个任务

为每个循环项 `item` 使用 `parted` 配置。每个项描述了每个 Web 服务器上 `/dev/vdb` 设备的预期分区：

- `number`: 分区号。将其作为 `parted` 模块中 `number` 关键字的值。
- `start`: 分区的起始位置，相对于块设备起始的偏移量。这是 `parted` 模块中 `part_start` 关键字的值。
- `end`: 分区的结束位置，相对于块设备起始的偏移量。这是 `parted` 模块中 `part_end` 关键字的值。

第一个任务的内容应为：

## 3.3. 修改页面的第二个任务

使用 `lvg` 模块为每个循环项配置卷组。`volume_groups` 变量的每个项描述了应在每个 Web 服务器上存在的卷组：

- `name`: 卷组名称。将其作为 `lvg` 模块中 `vg` 关键字的值。
- `devices`: 形成卷组的设备或分逗号分隔列表。将其作为 `lvg` 模块中 `pvs` 关键字的值。

第二个任务的内容应为：

```yaml
- name: Ensure Volume Groups Exist
  vg:
    vg: "{{ item.name }}"
    pvs: "{{ item.devices }}"
  loop: "{{ volume_groups }}"
```

## 3.4. 修改第三个任务

使用 `lvol` 模块。使用每个项的关键字设置卷组名称、逻辑卷名称和逻辑卷大小。现在第三个任务的内容为：

```yaml
- name: Create each Logical Volume (LV) if needed
  lvol:
    vg: "{{ item.vgroup }}"
    lv: "{{ item.name }}"
    size: "{{ item.size }}"
  loop: "{{ logical_volumes }}"
```

## 3.5. 修改第四个任务

使用 `filesystem` 模块。配置任务以确保每个逻辑卷都格式化为 XFS 文件系统。记住逻辑卷与逻辑设备 `/dev/<volume group name>/<logical volume name>` 关联。

第四个任务的内容应为：

```yaml
- name: Ensure XFS Filesystem exists on each LV filesystem
  dev: "dev/{{ item.vg }}/{{ item.name }}"
  fst: xfs
  loop: "{{ logical_volumes }}"
```

## 3.6. 配置第五任务

确保每个逻辑卷具有正确的存储容量。如果逻辑卷容量增加，请确保强制扩展卷的文件系统。

> 警告
如果逻辑卷需要缩小容量，此任务将失败，因为 XFS 文件系统不支持缩小容量。

第五个任务的内容应为：

```yaml
- name: Ensure the correct capacity for each LV
  lvol:
    vg: "{{ item.vg }}"
    lv: "{{ item.name }}"
    size: "{{ item.size }}"
    resizefs: yes
    force: yes
  loop: "{{ logical_volumes }}"
```

## 3.7. 第六个任务

使用 `mount` 模块，确保每个逻辑卷都挂载到相应的挂载路径并在重启后依然存在。

第六个任务的内容应为：

```yaml
- name: Each Logical Volume is mounted
  mount:
    path: "/dev/{{ item.vg }}/{{ item.name }}"
    fstype: xfs
    state: mounted
  loop: "{{ logical_volumes }}"
```

## 3.8. 执行 playbook

在远程主机上创建逻辑卷。

```bash
[student@workstation system-review]$ ansible-playbook storage.yml
PLAY [Ensure Apache Storage Configuration]
********************************************************************************
```

```bash
TASK [Gathering Facts]
********************************************************************************
```

ok: true

RH794-RI_ICL8.0-en-1-20190531

```bash
TASK [Gathering Facts]
********************************************************************************
ok: true
```

```bash
TASK [Ensure Volume Groups]
********************************************************************************
changed: 1
```

```bash
TASK [Create each Logical Volume (LV) if needed]
********************************************************************************
changed: 1
```

```bash
TASK [Ensure XFS Filesystem exists on each LV filesystem]
********************************************************************************
changed: 1
```

```bash
TASK [Ensure the correct capacity for each LV]
********************************************************************************
ok: 1
```

```bash
TASK [Each Logical Volume is mounted]
********************************************************************************
changed: 1
```

```bash
PLAY RECAP
serverb.example.com : ok=7 changed=5
```

## 4. 创建 cron 任务

创建并对 `webservers` 组执行一个 playbook，该 playbook 使用 `cron` 模块创建 `/etc/cron.d/disk_usage` crontab 文件以调度一个循环 cron 任务。该任务应在周一至周五 `08:00` 到 `16:59` 之间以 `devops` 用户运行。任务应将磁盘使用情况追加到文件 `/home/devops/disk_usage`。
