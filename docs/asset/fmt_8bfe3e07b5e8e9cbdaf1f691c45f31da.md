
```
        device_obj = self.get_dev_methods(device)

        device_obj.FilesystemUnmount(self.device['IdType'], fs_args,

            mount_path)

    except DBusException:

        return False

    return True

def on_unmount_device(self, menuitem, device):

    try:

        device_obj = self.get_dev_methods(device)

        device_obj.FilesystemUnmount([])

    except DBusException:

        return False

    return True
```

# UI 回调

def _on_activate_event(self, status, icon):

    ui_manager = gtk.UIManager()

    ui_manager.add_ui(ui_manager.merge_id(), '/', 'popup', 'popup',

        GTK_UI_MANAGER_POPUP, False)

    action_list = []

    if self._devices:

        for device_obj_path in self._devices:

            device = self._devices[device_obj_path]

            if device['IdUsage'] == 'filesystem':

                if device['IdLabel']:

                    label = device['IdLabel']

                else:

                    label = '%s Filesystem' \

                    # self.get_human_readable_size(

                        device['DeviceSize'])

                uuid = str(device['IdUuid'])

                ui_manager.add_ui(ui_manager.new_merge_id(), '/popup',

                    uuid, uuid, gtk.UI_MANAGER_MENU, False)

                action_list.append((uuid, gtk.STOCK_HARDDISK, label,

                    # 子菜单在此

                if device['DeviceIsMounted']:

                    # 浏览内容

                    ui_manager.add_ui(ui_manager.new_merge_id(),

                        '/popup/' + uuid, 'open' + uuid,

                        gtk.UI_MANAGER_MENUITEN, False)

                    action_list.append(('open' + uuid, gtk.STOCK_OPEN,

                        'Browse', None, 'Browse the device contents',

                        self.on_about_event))

                # 卸载设备

                ui_manager.add_ui(ui_manager.new_merge_id(),

                    '/popup/' + uuid, 'unmount' + uuid,

                    unmount + uuid,

                    gtk.UI_MANAGER_MENUITEN, False)

                action_list.append(('unmount' + uuid, gtk.STOCK_OPEN,

                    'Unmount', None, 'Unmount the device',

                    self.on_about_event))

            else:

                # 卸载设备

                ui_manager.add_ui(ui_manager.new_merge_id(),

                    '/popup/' + uuid, 'mount' + uuid,

                    mount + uuid,

                    gtk.UI_MANAGER_MENUITEN, False)

                action_list.append(('mount' + uuid, gtk.STOCK_APPLY,

                    'Mount', None, 'Mount the device',

                    self.on_about_event))

            elif device['MediaEjectable']:

                if device['IdLabel']:

                    label = device['IdLabel']

                else:

                    label = '%s %s %s' % (

                        device['DriveModel'],

                        device['Revision'])

                ui_manager.add_ui(ui_manager.merge_id(), '/popup',

                    label, label, gtk.UI_MANAGER_MENU, False)

                action_list.append((label, gtk.STOCK_CDROM, label,

                if device['DeviceIsMounted']):

                    # 浏览内容

                    ui_manager.add_ui(ui_manager.new_merge_id(),

                        '/popup/' + uuid, 'open' + uuid,

                        gtk.UI_MANAGER_MENUITEN, False)

                    action_list.append(('open' + uuid, gtk.STOCK_OPEN,

                        'Browse', None, 'Browse the device contents',

                        self.on_about_event))

                    # 卸载设备

                    ui_manager.add_ui(ui_manager.new_merge_id(),

                        '/popup/' + uuid, 'unmount' + uuid,

                        unmount + uuid,

                        gtk.UI_MANAGER_MENUITEN, False)

                    action_list.append(('unmount' + uuid, gtk.STOCK_OPEN,

                        'Unmount', None, 'Unmount the device',

                        self.on_about_event))

                else:

                    # 卸载设备

                    ui_manager.add_ui(ui_manager.new_merge_id(),

                        '/popup/' + uuid, 'mount' + uuid,

                        mount + uuid,

                        gtk.UI_MANAGER_MENUITEN, False)

                    action_list.append(('mount' + uuid, gtk.STOCK_APPLY,

                        'Mount', None, 'Mount the device',

                        self.on_about_event))

            else:

                # 卸载设备

                ui_manager.add_ui(ui_manager.new_merge_id(), '/popup',

                    'WithoutDisks', 'WithoutDisks',

                    gtk.UI_MANAGER_MENUITEN, False)

                action_list.append(('WithoutDisks', gtk.STOCK_DELETE,

                    'WithoutDisks', None, 'WithoutDisks',

                    self.on_about_event))

        action_group = gtk.ActionGroup('actions1')

        action_group.add_actions(action_list)

        ui_manager.insert_action_group(action_group, 0)

        ui_manager.ensure_update()

        menu = ui_manager.get_widget('/popup')

        menu.show_all()

        menu.popup(None, None, gtk.status_icon_position_menu, 1,

            gtk.get_current_time(time), status_icon)

    def _on_popup_menu_event(self, status_icon, button, activate_time):

        action_group = gtk.ActionGroup('actions2')

        action_group.add_actions()

        ui_string = '''

<ui>

    <popup>

        <menuitem name="Preferences" action="Preferences"/>

        <separator/>

        <menuitem name="About" action="About"/>

    </popup>

</ui>"""

        ui_manager = gtk.UIManager()

        ui_manager.add_ui_from_string(ui_string)

        ui_manager.insert_action_group(action_group, 0)

        menu = ui_manager.get_widget('/popup')

        menu.show_all()

        menu.popup(None, None, gtk.status_icon_position, button, activate_time, status_icon)

    def on_preferences_event(self, *args):

        pass

    def on_help_event(self, *args):

        pass

    def on_about_event(self, *args):

        pass

    def run(self):

        try:

            gtk.main()

        except KeyboardInterrupt:

            print('Exiting...')

            exit(0)

if __name__ == '__main__':

    tray_icon = DiscTray()

    tray_icon.run()
```

## 总结

世界上五分之一的人口很快将拥有移动设备并接入互联网。有了如此多的潜在用户，移动应用的爆发是不可避免的，而且正在发生。本章帮助你理解了引导这一发展的技术。

# 应用打包

有几个原因你可能想学习如何为 Ubuntu 打包。首先，构建和修复 Ubuntu 软件包是贡献 Ubuntu 社区的极佳方式。这也是学习 Ubuntu 以及你安装的应用如何运行的良好方法。如果你需要打包一个尚未进入存档的应用程序，这也很有用。

最后，如果你打算高度自定义 Ubuntu Mobile 自带的默认应用程序集，这显然也是重要的。

# 背景和重要工具

让 Ubuntu 成为备受尊敬的 Linux 发行版之一的原因是它的软件包系统，该系统基于 Debian，这被认为是自由软件世界中安装、升级和删除软件的最优雅的方法之一。

要成为一个优秀的打包者，必须对以下工具有所了解（此列表并非详尽，而是我们使用的一些应用程序的示例）：

## configure

`configure` 通常是为在多个平台上运行而设计的。由于这些平台具有不同的编译器和包含文件，因此需要编写 Makefiles（下一项）和构建脚本，使其能够在各种平台上运行。GNU 项目面对这个问题，设计了一套工具来帮助完成这项任务。`configure` 脚本运行一系列测试来确定关于你机器的重要信息。

## make

`make` 是一个用于从程序的源文件生成可执行文件和其他非源文件的工具。

## 第5章：应用程序打包

它通过一个名为 `Makefile` 的文件获取构建构建程序的知识。`Makefile` 是一个包含 shell 命令的特殊文件，由你创建并命名为 `Makefile`，通过在 Makefile 所在的目录下输入命令 `make` 来执行。当你编写一个程序时，应该为它编写一个 makefile，以便使用 `make` 来构建和安装该程序。

`apt` 是 Advanced Package Tool（高级软件包工具）的缩写。该工具在整书中被广泛使用。以下 `apt` 命令对打包很有用：

- `apt-cache dump` — 显示缓存中的每个包。此命令可以配合 `grep` 管道符使用，例如 `apt-cache dump | grep search`，用于查找名称或依赖项包含 bar 的包。
- `apt-cache show` — 列出包所在的仓库（main/restricted/universe/multiverse）。
- `apt-cache showsrc` — 显示二进制包的信息。
- `apt-cache rdepends` — 显示包的依赖关系（哪些包需要所查询的包）。
- `apt-rdepends` — 递归列出包依赖关系以及前向构建依赖。

`dpkg` 是一个 Debian 打包工具，可用于安装、查询和卸载包。以下命令对打包很有用：

- `dpkg -S` — 显示特定文件所属的包。
- `dpkg -l` — 显示当前安装的包。这类似于 `apt-cache dump`，但针对的是已安装的包。
- `dpkg -c` — 显示二进制包的内容。它有助于确保文件被安装到正确的位置。
- `dpkg -f` — 显示二进制包的控制文件。它有助于确保依赖是正确的。
- `dpkg -L` — 列出由包（包）“所有”的文件。
- `dpkg -s` — 显示包状态详情。

处理源包时一个非常实用的命令：

```
$ dpkg-source -x filename.dsc [output-directory]
```
