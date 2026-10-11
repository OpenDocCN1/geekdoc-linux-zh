
```xml
<xml version="1.0"?>

<!DOCTYPE TYPE SYSTEM "file://picnik/locale/picnik.dtd">

<overlay id="picnik-overlay">
<html xmlns="http://www.mozilla.org/keykeeper/there.is.only_xml"
     xmlns:html="http://www.w3.org/1999/xhtml">
  
  <script type="application/javascript"
    src="chrome://picnik/content/menu.js";
  </script>
  <script type="application/javascript"
    src="chrome://picnik/content/menu.js";
  </script>

  <popup id="contentAreaContextMenu">
    <menuitem id="context-iconic"
      id="picnic-ct-ext"
      inserter="context-image"
      label="&picnik.edit_picture."
      oncommand="picnik.edit(this)"
      image="chrome://picnik/picnik_i16.png" />
    </menuitem>
  </popup>
```

我们是。其中一个主要部分是在 `DTD`（文档类型定义）文件中将 `UI` 字符串化的能力。在 `Chrome` 中，`firefox.xmlOverlay` 使用代码行中的字符串。

本地化 `URL` 是特殊的，因为浏览器会自动将它们映射到扩展程序中的正确位置。`Firefox` 会自动为美国英语用户扩展 `chrome://linuxjournal/locale/linuxjournal.dtd/locale/linuxjournal-US.linuxjournal.dtd`。

`DTD` 用于定义新的 `XML` 实体，这些实体可以被视为。我们的 `DTD` 如下：

```xml
<ENTITY linuxjournal.label "您的本地化菜单项">
<ENTITY linuxjournalContext.label "您的菜单">
<ENTITY linuxjournalContext.accesskey "-">
```

这些实体在 `XML` 中通过将它们替换为 `&...;` 来引用：

```xml
<menuitem id="context-linuxjournal">
  label="&linuxjournalContext.label";
  accesskey="&linuxjournalContext.accesskey;">
```

这种字符串分离起初看起来可能很奇怪，如果你在字符串中写了拼写错误，它会出现在多个处，你只需要修复一次。

## 代码

实际的扩展代码是用 `JavaScript` 编写的，这使得许多资深 Web 开发人员在编写它们时游刃有。

## `ASA` 计算机

### 定制化服务器专家！

`www.ascomputers.com`

`1-800-REAL-PCS`

面向开源社区的硬件系统 - 自 1989 年以来。

(`Linux`, `FreeBSD`, `NetBSD`, `OpenBSD`, `Solaris`, `MSX`)

`AMD` `Opter` 处理器为最先进的应用提供高性能、可扩展的服务器。

“同时运行 32 位和 64 位应用程序。”

您的定制应用程序解决方案！

“告诉我们您的需求……”

![](img/1234e63edf27cb1f15e6071bce50485a_78_0.png)

“我们将构建……”

# `AMD` 选项起价 $847

- 1U 双路 2.6GHz
- `AMD` 选项 40G
- 512MB `DDR3300` 无缓冲
- 支持到 8GB `DDR4`
- 460GB `SATA` 硬盘
- x 10/000 Mbps

列表 2: `contextmenu.js`

```javascript
var picnicClickContextMenu = {
  onload: function() {
    // 将 showContextMenu 函数附加到右键菜单
    var e = document.getElementById('contextAreaMenu');
    e.addEventListener('popmenu', function(event) {
      picnicContextMenu.showContextMenu(event);
    });
  },
  // 在右键菜单弹出前点击
  showContextMenu: function(event) {
    if (event) {
      var editPicture = document.getElementById('picnic-ct-edit');
      if (editPicture) {
        editPicture.hidden = !editPicture.onload;
      }

      if (picnicContextMenu.hasImage()) {
        this.imageUrl = picnicContextMenu.imageUrl;
      } else {
        this.imageUrl = '';
      }
    }
  },
  // 当用户点击“编辑”菜单项时调用
  editFunction: function() {
    var url = picnic.baseURL + "Import" + escape(this.imageUrl);
    g.selected = g.addTab(url);
  }
};
window.addEventListener('load', function () {
    picnicContextMenu.load();
}, false);
```

# `AMD` 选项(TM) 起价 $4120

- 1U 双路型号 840
- 2GB 内存
- 支持到 64GB `FB/IMM`
- 80 GB `SATA` 热插硬盘
- 虚拟双路 10/0000 通道

![](img/1234e63edf27cb1f15e6071bce50485a_80_1.png)

# 双路选项(TM) 容量 $6445

- 2U 双路型号 246
- 4TB 容量 (6TB) 最大
- 10/1000 `Gigabit` `Gigabit`
- `NAS` 或 `SAS` 选项

## 为什么与 `ASA` 合作？

自 1989 年以来

![](img/1234e63edf27cb1f15e6071bce50485a_80_2.png)

2664 Calle del Mundo, Santa Clara, CA 95064

`www.ascomputers.com`

电话: `1-800-REAL-PCS`，传真: 408-654-2910

很容易跨平台。为了加载代码，必须在叠加层文件中引用。在这种，有以下代码：

```html
<script src='overlay.js'></script>
```

编写扩展程序时最重要的记忆之一是，`JavaScript` 的全局命名空间在扩展程序和核心代码之间共享。这意味着要使用技术防止命名冲突，简单的方法是为所有变量和函数添加唯一前缀。首选的方法是创建一个包含所有变量和函数的匿名对象。查看

## 深度

列表 3. `picnik.xml` 文件的扩展版本
