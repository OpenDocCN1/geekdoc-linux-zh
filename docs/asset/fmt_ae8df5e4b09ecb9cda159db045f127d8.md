
一种向用户展示信息的新方法在 Ubuntu Jaty 版本中引入。这是生成被动弹出窗口（也称为“气泡”）的方法，通知用户事件。

虽然某些信息需要用户的响应（例如电量低），但系统产生的大部分信息纯属告知，不需要用户交互。通知（通过 `notify-send` 进程或 `org.freedesktop.Notifications` DBus 接口提供）在这种情况下不为用户提供“操作”（用户无法点击）。从语义上讲，气泡要么是确认（例如亮度增加），要么是通知（例如新歌曲播放）。

可以通过手动命令通知通知系统

```bash
$ notify-send
```

也可以通过 DBus 接口进行编程使用。有四种手动使用 `notify-send` 工具的方法（由 `libnotify-bin` 包提供）：

- `$ notify-send 'Hello Rodrigo' -i notification-message-info`

- `$ notify-send 'WiFi connection lost' -i notification-network-wireless-disconnected`

- `$ notify-send 'PUMD' 'This is some notification'`

- `$ notify-send 'Summary-only'`

通过编程发送通知（这在本章稍后的“将所有概念结合”部分），请使用：

```python
def __init__(self):
    (...)
    # 保存通知系统的可用性状态
    self._notification_available = pynotify.init('disk-applet')
```

## 第4 章：应用开发

```python
if not self._get_dev_prop(device, 'device-is-drive') \
    and not self._notification_available:
    return

if self._get_dev_prop(device, 'drive-connection-interface') == 'usb':
    notification_icon = 'notification-device-usb'
elif self._get_dev_prop(device, 'drive-connection-interface') == 'firewire':
    notification_icon = 'notification-device-firewire'
else:
    notification_icon = 'notification-device'

body_msg = '%s %s %s' % (
    self._get_dev_prop(device, 'drive-vendor'),
    self._get_dev_prop(device, 'drive-model'),
    self._get_dev_prop(device, 'drive-revision')
)

p = pynotify.Notification('New Device Added', body_msg.strip(),
    notification_icon)
n.show()
```

通知图标位于：

`/usr/share/icons/Human/scalable/status/`

以及：

`/usr/share/notify-osd/hicolor/scalable/status/`

注意，Human 是 Ubuntu 的默认图标主题。可以通过运行以下命令来查看：

```bash
gconftool-2 -g /desktop/gnome/interface/icon-theme
```

通过获取最新的 notify-osd 源码，可以下载更多的通知示例：

```bash
$ bzr get http://bazaar.launchpad.net/+ubuntu-desktop/notify-osd/ubuntu-notifyd
```

可以通过以下方法关闭设备的通知系统：

```bash
sudo mv /usr/share/dbus-1/services/org.freedesktop.Notifications.service \
    /usr/share/dbus-1/services/org.freedesktop.Notifications.service.disabled
```

在你的应用程序中恰当使用通知框架，可以为用户创造更丰富的桌面体验。

## 整合所有概念

以下是一个小程序的的完整代码，该小程序会在可移动介质连接到设备时对其显示通知。它使用了本章中提到的所有关键技术，包括 D-Bus、通知和 DeviceKit，并演示了 `gobject`、`gtk` 和 `gconf` 的用法。

它是为 Netbook Remix 的 karmic 版本编写的，在 Jaunty 上无法运行。这是因为代码使用了 Device Kit，而 karmic 用它取代了 HAL 作为默认硬件抽象层。

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

# Copyright (C) 2008 Rodrigo Cesar Lopes Belem
# Author: Rodrigo Cesar Lopes Belem <rodrigo.belem@gmail.com>
#
# 此程序是自由软件；你可以根据自由软件基金会发布的
# GNU 通用许可许可证条款对其进行分发和修改；
# 也可以是该许可证的第 2 版，或
# （根据你的选择）任何后续版本。

# 分发此程序的目的是希望它能够有用，
# 但不提供任何保证；甚至不提供关于商品性
# 或针对特定用途的适用性的隐性保证。详情请参阅
# GNU 通用许可许可证。

# 你在收到此程序时应该收到一份通用许可许可证
# 副本；如果没有，请写信给自由软件
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307

import os
import sys
import gtk
import math
import gettext
import pyinotify
from gettext import gettext as _

import glob
import gob

locale_dirs = [
    'locale',
    os.path.join(os.path.sep, 'usr', 'locale'),
    os.path.join(os.path.sep, 'usr', 'local', 'share', 'locale'),
]
DIR = None
for l in locale_dirs:
    if glob.glob(os.path.join(l,'**','*','disk-applet.mo')):
        DIR = l
        break

gettext.bindtextdomain('disk-applet', DIR)
gettext.textdomain('disk-applet')
gettext.install('disk-applet', DIR, unicode=1)

import locale
try:
    locale.setlocale(locale.LC_ALL,'')
except locale.Error:
    print 'Unable to properly set locale %s%s%(locale.getdefaultlocale())'

import dbus
from dbus.mainloop.glib import DBusMainLoop

DBusMainLoop(set_as_default=True)

class DiscTray(gtk.StatusIcon):

    def __init__(self):
        gtk.StatusIcon.__init__(self)
        self.set_from_stock(gtk.GTK_STOCK_HARDDISK)
        self.set_tooltip('Status icon tooltip')
        self.devices = {}

    # 保存通知系统可用性
    self.notification_available = pnotify.init('disk-applet')

    bus.add_signal_receiver(self.on_device_added,
        'DeviceAdded',
        'org.freedesktop.DeviceKit.Disks',
        'org.freedesktop.DeviceKit.Disks',
        '/org/freedesktop/DeviceKit/Disks')

    bus.add_signal_receiver(self.on_device_removed,
        'DeviceRemoved',
        'org.freedesktop.DeviceKit.Disks',
        'org.freedesktop.DeviceKit.Disks',
        '/org/freedesktop/DeviceKit/Disks')

    bus.add_signal_receiver(self.on_device_changed,
        'DeviceChanged',
        'org.freedesktop.DeviceKit.Disks',
        'org.freedesktop.DeviceKit.Disks',
        '/org/freedesktop/DeviceKit/Disks')

    except dbus.DBusException:
        exit(1)

    self.connect('activate', self.on_activate_event)
    self.connect('popup-menu', self.on_popup_menu_event)

    # 添加一个信号来检测 CD 是否插入了驱动器
    gobject.signal_new('device-is-optical-disc', gtk.StatusIcon,
        gobject.RUN_LAST, gob.TYPE_NONE,
        (gobject.TYPE_STRING, gob.TYPE_BOOLEAN))

    # 添加一个信号来检测设备是否挂载，以便之后可以
    # 执行操作
    gobject.signal_new('device-mounted', gtk.StatusIcon,
        gobject.RUN_LAST, gob.TYPE_NONE,
        (gobject.TYPE_STRING, gob.TYPE_BOOLEAN))

    gobject.signal_new('device-unmounted', gtk.StatusIcon,
        gobject.RUN_LAST, gob.TYPE_NONE,
        (gobject.TYPE_STRING,))

    self.connect('device-is-disc', self._on_disc_insert_event)
    self.connect('device-mounted', self._on_mounted_event)
    self.connect('device-unmounted', self._on_unmounted_event)

    self._populate_device_list()

    def get_human_readable_size(self, bytes):
        bytes = float(bytes)
        count = int(math.log(bytes)) / math.log(1000)
        if count == 1:
            bin_prefix = 'KB'
        elif count == 2:
            bin_prefix = 'MB'
        elif count == 3:
            bin_prefix = 'GB'
        elif count == 4:
            bin_prefix = 'TB'

        return '%0.1f%s' % (bytes/1000**count, bin_prefix)

    def get_dev_interface(self, object_path, interface):
        bus = dbus.SystemBus()
        proxy_obj = bus.get_object('org.freedesktop.DeviceKit.Disks',
            object_path)
        iface_obj = dbus.Interface(proxy_obj, interface)
        return iface_obj

    def get_dev_prop(self, device, property):
        props_iface_obj = self.get_dev_interface(device,
            'org.freedesktop.DBus.Properties')
        try:
            res = props_iface_obj.Get('org.freedesktop.DeviceKit.Device',
                property)
        except dbus.DBusException:
            res = ''
        return res

    def _populate_device_list(self):
        bus = dbus.SystemBus()
        disks_obj = bus.get_object('org.freedesktop.DeviceKit.Disks',
            '/org/freedesktop/DeviceKit/Disks')

        devices = disks_obj.EnumerateDevices()

        if devices:
            devices.sort()
            for device in devices:
                self._add_device_to_list(device)

    def _add_device_to_list(self, device):
        if self._dev_get_prop(device, 'device-partition') == 'uint32' \
           or self._dev_get_prop(device, 'DriveMediaEjectable') == 'True':
            self._devices[device] = dict(self._get_all_dev_prop(device))

    def _get_all_dev_prop(self, device):
        # Implementation detail implied by usage in snippet
        pass

    # SIGNALS CALLBACKS

    def on_device_added(self, device):
        self._add_device_to_list(device)
```
