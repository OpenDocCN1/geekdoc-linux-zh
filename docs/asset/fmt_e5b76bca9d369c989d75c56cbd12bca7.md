
# PLAY [Ensure Apache Storage Configuration]
************************************

## TASK [Gathering Facts]
****************************************************

ok: [server.lab.example.com]

## TASK [Correct partitions exist on /dev/vdb]
************************************

ok: [server.lab.example.com] => {item={number: 1, start: 257Mi, end: 511Mi}}
ok: [server.lab.example.com] => {item={number: 2, start: 512Mi, end: 767Mi}}

## TASK [Ensure Volume Groups Exist]
************************************

ok: [server.lab.example.com] => {item={name: apache-vg, devices: ["/dev/vdb1", "/dev/vdb2"]}}

## TASK [Create Logical Volume (LV) if needed]
************************************

skipping: [server.lab.example.com] => {item={name: content-lv, size: 128M, group: apache-vg, mount_path: /var/www}}
skipping: [server.lab.example.com] => {item={name: logs-lv, size: 256M, group: apache-vg, mount_path: /var/log}}

## TASK [Ensure XFS Filesystem exists on each LV]
************************************

changed: [server.lab.example.com] => {item={name: content-lv, group: apache-vg}}
changed: [server.lab.example.com] => {item={name: logs-lv, group: apache-vg}}

## TASK [Ensure the correct capacity for each LV]
************************************

ok: [server.lab.example.com] => {item={name: content-lv, size: 128M, group: apache-vg, mount_path: /var/www}}
ok: [server.lab.example.com] => {item={name: logs-lv, size: 256M, group: apache-vg, mount_path: /var/log}}

## TASK [Each Logical Volume is mounted]
************************************

ok: [server.lab.example.com] => {item={name: content-lv, group: apache-vg, mount_path: /var/www}}
ok: [server.lab.example.com] => {item={name: logs-lv, group: apache-vg, mount_path: /var/log}}

**************************************************
# PLAY RECAP

servera.lab.example.com : ok=6 changed=3 unreachable=0
failed=0
skipped=1 rescued=0 ignored=0

+ 9.3. 使用 Ansible 命令在远程主机上运行 `lsblk` 命令。输出显示了逻辑卷的挂载点。

```bash
[student@workstation-storage]$ ansible all -a lsblk

servera.lab.example.com | CHANGED | rc=>

NAME MAJ MIN RM SIZE TYPE MOUNTPOINT

sr0 11:0 1 1024M disk rom

vda 252:0 0 10G disk

  |-vda1 252:1 0 10G disk part /

db 252:16 0 16G disk

  |-apache-vg-content--lv 253:0 0 64M lvm /var/www
```

RH254-RHEL8.0-en-1-20190531
451

10. 将 `content-lv` 逻辑卷的容量增加到 128 MIB，并将 `logs-lv` 逻辑卷增加到 256 MIB。这需要增加 `apache-vg` 卷组的容量。创建一个容量为 256 MIB 的新分区并添加到 `apache-vg` 卷组。

+ 10.1. 编辑 `storage_vars.yml` 中的 `partitions` 变量，为 `/dev/vdb` 设备添加第二个分区。`partitions` 变量的内容应该是：
```yaml
partitions:
- number: 1
  start: 257Mi
  end: 511Mi
- number: 2
  start: 512Mi
  end: 767Mi
```

+ 10.2. 编辑 `storage_vars.yml` 中的 `volume_groups` 变量，为 `apache-vg` 卷组添加第二个分区。`volume_groups` 变量的内容应该是：
```yaml
volume_groups:
- name: apache-vg
  devices: ["/dev/vdb1", "/dev/vdb2"]
```

+ 10.3. 编辑 `storage_vars.yml` 中的 `logical_volumes` 变量以增加其容量。`logical_volumes` 变量的内容应该是：
```yaml
logical_volumes:
- name: content-lv
  size: 128M
  group: apache-vg
  mount_path: /var/www
- name: logs-lv
  size: 256M
  group: apache-vg
  mount_path: /var/log
```

+ 10.4. 执行 playbook 以验证每个逻辑卷的容量。
```bash
[student@workstation system-storage]$ ansible-playbook storage.yml
```
