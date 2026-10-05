

```
locale (share/locale)
services (share/services)
servicetypes (share/servicetypes)
mime (share/mime/)
wallpaper (share/wallpaper)
templates (share/templates)
exe (share/bin)
lib (share/lib)
all (share/)
data_<application_name> (share/apps/<application_name>)
```

这有点让人困惑，因为并不是所有的目录名称都映射到配置文件中的相同名称。示例 7-9 显示了如何在 `kdeglobals` 文件中使用控制模块（Control Module）和自定义限制（Custom Restriction）部分。

## 示例 7-9 更多的 KDE 限制选项

```
[KDE Control Module Restrictions]
kde-background.desktop=false
de-colors.desktop=false
de-fonts.desktop=false
de-kwinddecoration.desktop=false
de-proxy.desktop=false
de-style.desktop=false
```

```
[KDE Custom Restrictions]
restrict_file_browsing=true
```

## Kiosk 限制

对于公共终端来说，禁用运行命令和访问命令行 shell 可能是更优的选择，但使用不使用 KDE 框架的 Mozilla 很容易打开 shell。当你禁用注销选项时，还必须禁用通过按 Ctrl+Alt+Delete 关闭 X 服务器的功能（这些设置可以在 `/etc/initab` 中配置），否则限制可以被轻而易地绕过。为了让整个设置变得无懈一击，还需要考虑很多副作用，因为许多 Linux 应用程序和子系统并没有使用 KDE Kiosk 框架。

## 7.1.2 GNOME 锁定

GNOME 桌面使用数据库，该数据库由可扩展标记语言（XML）文件表示，用于构建和自定义其所有设置。该数据库由三个源构建：设置（settings）、默认（default）和强制（mandatory）。用户所做的更改通常会进入设置源。

默认源（default source）包含默认选项，用于用户未配置的每项设置。最后，强制源（mandatory source）会覆盖用户的个人偏好，并允许对相关设置进行更改。设置源通常存储在 `$HOME/.gconf`。默认源在基于 Red Hat 的系统中位于 `/etc/gconf/gconf.xml.defaults`，在基于 SUSE 的系统中位于 `/etc/opt/gnome/gconf/gconf.xml.defaults`。而强制源在基于 Red Hat 的系统中位于 `/etc/gconf/gconf.xml.mandatory`，在基于 SUSE 的系统中位于 `/etc/opt/gnome/gconf/gconf.xml.mandatory`。

关于 GNOME 如何存储设置的更多信息，请参见第 317 页的“桌面个性化”。

## gconftool-2

GNOME 桌面带有一个名为 `gconftool-2` 的工具。你可以从命令行使用它编辑 GConf 数据库，并编辑任何配置源。由于默认源适用于所有用户，通常只能由 root 用户编辑。此外，这些更改直接编辑 GConf 数据库，因此不会影响正在运行的 GConf 会话。

如果你想删除运行对话的快捷键（通常是 Alt-F2），请运行以下命令：

```
gconftool-2 --direct --config-source
xml:readwrite:/etc/gconf/gconf.xml.mandatory --type bool --set
/apps/panel/global/run
```

如果你想为新用户设置默认工作区数量，但允许他们以后更改此设置，请运行以下命令：

```
gconftool-2 --direct --config-source
xml:readwrite:/etc/gconf/gconf.xml.defaults --type int --set
/apps/metacity/general/num_workspaces 2
```

## 图形化工具

也存在锁定 GNOME 桌面的图形界面工具。与使用 `gconftool-2` ，可以使用 `gconf-editor` 直接编辑默认源和强制源。要这样做，请以 root 身份启动 `gconf-editor`，并选择 **File → Defaults Window** 或 **File → Mandatory Window**。与命令行一样，更改对已运行的 GConf 会话无效。

## Pessus

另一个工具是 Pessus。Pessus 是一个图形工具，用于配置 GNOME 内置的锁定设置，否则这些设置只能通过 GConf 配置。Pessus 包含在 GNOME 2.14 版本中。这些设置包括限制添加面板插件以及是否可以编辑桌面图标。关于 Pessus 的更多信息请访问：

http://www.gnome.org/~vuntz/pessus/
http://live.gnome.org/pessus

## Sabayon

Sabayon 是一种图形化系统管理工具，用于管理 GNOME 桌面配置设置。Sabayon 提供了一种新的策略编辑方法。它并不是提供一个内置 GUI 来编辑每项设置，而是启动一个运行整个 GNOME 桌面环境的嵌套 X 会话（关于 X 会话的更多信息可以见第 118 页 5.2.4，“图形和文本环境”）。嵌套环境中进行的任何更改都会记录，并在会话结束时将这些设置应用到默认或强制 GConf 存储中。Sabayon 还能检测到添加图标以及是否可以编辑桌面图标。关于 Pessus 的更多信息请访问：

http://www.gnome.org/~vuntz/pessus/
http://live.gnome.org/pessus

