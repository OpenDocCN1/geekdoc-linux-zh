
Nov 19 15:40 Rocky Linux gnome-shell[2389]: meta_viewport_info_get_extents: assertion 'viewport_info != NULL'

failed

Nov 19 15:40 Rocky Linux gnome-shell[2389]: meta_viewport_info_get_extents: assertion 'viewport_info != NULL'

failed

Nov 19 19 15:40 Rocky Linux gnome-shell[2389]: meta_viewport_info_get_extents: assertion 'viewport_info != NULL'

failed

Nov 19 15:40 Rocky Linux gnome-shell[2381]: Dependency failed for GNOME Xsettings services[2283]: g_stroll: assertion 'string != NULL' failed

Nov 19 15:43 Rocky Linux gnome-shell[2283]: Dependency failed for GNOME Xsettings services[2283]: DBus.Error.HasNameNoOwner

Nov 19 15:43 Rocky Linux gnome-shell[2283]: org.gnome.settingsDaemon.Settings: Job org.gnome.settingsDaemon.on.Xsettings.service failed with 'dependency'

Nov 19 15:43 Rocky Linux gnome-shell[2381]: gnome-session-x11-services-target: Job gnome-session-x11-service failed with 'dependency'

Nov 19 15:47 Rocky Linux gnome-shell[2380]: libGL warning: egl failed to create dri screen

Nov 19 15:47 Rocky Linux gnome-shell[2380]: libGL warning: egl failed to create dri screen

Nov 19 15:47 Rocky Linux gnome-shell[2380]: failed to get drm for output

Nov 19 15:51 Rocky Linux gnome-dbus-environment[2429]: GLib-GObject: unset_reference: assertion 'G_IS_OBJECT'

Nov 19 15:51 Rocky Linux systemd[2914]: failed to add device /sys/devices/pci0:0000:00:14.0/disk/sda: kernel: failed to open (/dev/sda1). No medium found

Nov 19 15:44 Rocky Linux gnome-software[2381]: failed to get features: no apps to show

```
图 2.16: 失败的消息，第三个示例
```

命令 `grep "failed" /tmp/system_logs.txt` 在特定的日志文件（在本例中为 `/tmp/system_logs.txt`）中搜索关键字 `"failed"`。这种方法处理存储在自定义位置的日志或分析以前会话的日志时非常有用。

## 跨日志文件的文本处理

如果我们处理的是分成部分的非二进制日志文件，合并和过滤的方法与之前相同。

### 合并并过滤

```
cat logs_part1.txt logs_part2.txt | echo "criticalerror1" "criticalErrorT2" > logs_part1.txt
```

```
[cesarmerver@RockyLinux ~#]$ echo "criticalerror644" "criticalerror4xgp" > logs_part2.txt
```

```
[cesarmerver@RockyLinux ~#]$ cat logs_part1.txt logs_part2.txt | grep "critical"
criticalerror1 criticalErrorT2
criticalerror644 criticalerror4xgp
```
