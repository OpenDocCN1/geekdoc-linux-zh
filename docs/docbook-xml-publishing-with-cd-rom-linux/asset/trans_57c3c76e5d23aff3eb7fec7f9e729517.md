

# 第8章：使用 Emacs

程序 喜好 设置 emacs@gnu.emacs.net 上午 11:20:25
缓冲区 文件：编辑 搜索 模式 SGML 修改 标记 视图 帮助
那只快速的棕色狐狸跳过了那只懒狗……

![](img/81f56bf497dbf7f7582072400d12cb42_201_0.png)

如果你尚未安装 PSGML，可以从 CD-ROM 获取其二进制文件或源码，或者从 PSGML 网页（http://www.lysator.liu.se/projects/about_psgml.html）获取最新源码。

PSGML 不仅适用于 DocBook；其最新版本应适用于任何有效的 SGML 或 XML DTD。

要安装 PSGML，你必须将文件放在 Emacs 加载路径（load path）中的某个目录下。在我的系统上，我在主目录下有一个 Emacs 目录，在其下有一个 psgml 目录，路径看起来像 /home/zonker/Emacs/psgml/，所有的 PSGML *.el 和 *.cle 文件都位于 psgml/ 目录中。你还需要在主目录下创建一个 emacs 文件，并包含以下行：

```
(autoload 'sgml-mode "psgml" "编辑 SGML 文件的主模式。" t)
(autoload 'xml-mode "psgml" "编辑 XML 文件的主模式。" t)
```

作为一个完整的 .emacs 文件的示例，你可以使用我的文件作为参考（见图 8.13）。

# 如何使用 Emacs 节省时间 — Emacs PSGML 模式

177

![](img/81f56bf497dbf7f7582072400d12cb42_202_0.png)

```lisp
(setq load-path
      (cons "~/Emacs/Extensions"
      (cons "~/psgml" load-path)))

(autoload 'sgml-mode "psgml" "编辑 SGML 文件的主模式。" t)
(autoload 'xml-mode "psgml" "编辑 XML 文件的主模式。" t)

custom-set-variables
  '(delete-selection-mode nil nil (delsel))
  '(scroll-bar-mode (quote right)))

custom-set-faces
  '(vhdl-font-lock-enumvalue-face (((class color) (background light))
    (:foreground "Gold4")))
  '(vhdl-font-lock-attribute-face (((class color) (background light))
    (:foreground "Orchid")))
```

```lisp
(vhdl-font-lock-translate-off-face (((((class color) (background light))
  (:background "LightGray")))

(font-lock-comment-face (((((class color) (background light))
  (:foreground "Firebrick")))

(vhdl-font-lock-directive-face (((((class color) (background light))
  (:foreground "CadetBlue")))

(font-lock-string-face (((((class color) (background light))
  (:foreground "RosyBrown")))

(font-lock-keyword-face (((((class color) (background light))
  (:foreground "Purple")))

(font-lock-warning-face (((((class color) (background light))
  (:bold t :foreground "Red")))

(font-lock-constant-face (((((class color) (background light))
  (:foreground "CadetBlue")))

(font-lock-type-face (((((class color) (background light)) (:foreground "ForestGreen")))

(vhdl-font-lock-function-face (((((class color) (background light))
  (:foreground "Orchid4")))

(vhdl-font-lock-reserved-words-face (((((class color) (background light))
  (:bold t :foreground "Orange")))

(font-lock-selection-face (((((class color) (background light))
  (:background "Gold44")))

(vhdl-font-lock-prompt-face (((((class color) (background light))
  (:bold t :foreground "Red")))

(font-lock-name-face (((((class color) (background light))
  (:foreground "Orchid")))

(font-lock-builtin-face (((((class color) (background light))
  (:foreground "Orange"))"))))
```

只有前几行是关于加载的。其余部分是关于语法高亮的。Lisp 是一种在 1950 年代发明的语言。I.T. 的缩写通常是指 Lisp。Emacs 运行 Lisp 解释器，它可以做很多事情。emacs 文件是显而易见的。

在 Emacs 中编辑 DocBook

如果你还没有安装 PSGML，可以通过 `sgml-mode` 进入 PSGML 模式。你会注意到，这些菜单是专门用于标记标记的。

PSGML 模式为标记 DocBook 提供了某些优势。使用 PSGML 模式菜单，你可以插入元素和属性，只查看文本，验证文档并查看错误。

# SGML 菜单

PSGML 模式下的 SGML 菜单允许你查看文档错误（见图 8.14）。

PSGML 模式下的 SGML 菜单允许根据上下文列出有效标签，验证文档并切换警告日志（见图 8.15）。

![](img/81f56bf497dbf7f7582072400d12cb42_204_0.png)

| 程序 | 喜好 设置 桌面 | emacs3@ey.email.net | 上午 11:34:52 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| emacs-frame@email.net | | | | | |

- 缓冲区 文件：编辑 搜索 模式 SGML 修改 标记 视图 DTD 帮助
- 介绍 (C-h)
- 设置解析掩码 (Yes) (C-c) 允许轻松管理
- 实时元素指示 (Yes)
- 自动重启 DTD (Yes) 本质：
- 标签区域激活时 (Yes) 列出有效标签
- 树归一化 (Yes) C-c 输出
- 文件选项
- 用户选项 提交错误报告
- 忽略透明 (No)
- 插入后保留光标 (No)
- 插入元素注释 (Yes)
- 标签结束菜单 (No)
- 警告未定义元素 (Yes)
- 警告未定义实体 (Yes)
- 忽略未定义元素 (No)
- 编辑时重新编译 DTD (No)
- 默认语言模式 (No)
- 声明 (-)
- 验证命令 (...)
- 标记菜单
- 系统标识符优选 (No)
- 跟踪输入查找 (No)
- 公共映射 (...) (No)
- 目录文件 (...)
- Ecat 文件 (...)
- 通用插入大小 | (No)

```
CHAPTER/DOC(1)==-L1--All
```

图 8.15 SGML 菜单

SGML 菜单和其他 PGML 菜单没有关联热键，但必须通过菜单访问。

# 修改菜单

PSGML 模式下的修改菜单允许用户将元素和字符引用转换为各种元素和属性的更改（见图 8.17）。

# 标记菜单

在编辑 DocBook 时，最常用的菜单可能是标记菜单。要结束当前元素，使用命令 `C-c /`，这应该很容易记住，因为所有的结束标签都使用 `/` 字符。

标记菜单还赋予用户在文档该处插入属性的能力。

