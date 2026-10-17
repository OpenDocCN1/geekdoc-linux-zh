
```
$ glxinfo | grep rendering

direct rendering: Yes
```

此示例显示已启用直接渲染。如果不支持，输出将显示为 `No` 而不是 `Yes`。虽然 DRI 可能非常重要，但许多游戏实现了 OpenGL 渲染，这是 NVIDIA 和 ATI 显卡都支持的功能。要为支持的显卡启用渲染，请向你的 `/etc/X11/xorg.conf` 文件添加以下行：

```
Load "render"
```
