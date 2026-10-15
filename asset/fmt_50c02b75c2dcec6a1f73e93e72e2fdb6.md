
`start_a = amount_light`

`catch_a_ghost()`

```
- except KeyboardInterrupt: pass
```

你可能想将你的幽灵相机部署在一个你无法监控的地方。这需要程序在插上电源时自动启动。打开终端并输入`sudo crontab -e`打开编辑器，你可以在其中列出特定时间运行的程序。滚动到列表底部，输入`@reboot`命令，后跟你的幽灵相机文件名。

```
@reboot python /home/pi/ghost_camera.py
```
