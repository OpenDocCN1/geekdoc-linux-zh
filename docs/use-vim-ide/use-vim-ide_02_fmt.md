
# 一、源码安装编辑器 Vim

## 1. 源码安装编辑器 Vim

发行套件的软件源中预编译的 Vim 要么不是最新版本，要么功能有阉割，有必要升级成全功能的最新版，当然，源码安装必须滴：

```bash
git clone git@github.com:vim/vim.git
cd vim/
./configure --with-features=huge --enable-pythoninterp --enable-rubyinterp --enable-luainterp --enable-perlinterp --with-python-config-dir=/usr/lib/python2.7/config/ --enable-gui=gtk2 --enable-cscope --prefix=/usr
make
make install
```

其中，`--enable-pythoninterp`、`--enable-rubyinterp`、`--enable-perlinterp`、`--enable-luainterp` 等分别表示支持 Ruby、Python、Perl、Lua 编写的插件，`--enable-gui=gtk2` 表示生成采用 GNOME2 风格的 GVim，`--enable-cscope` 支持 Cscope，`--with-python-config-dir=/usr/lib/python2.7/config/` 指定 Python 路径（先自行安装 Python 的头文件 `python-devel`）。

这几个特性非常重要，影响后面各类插件的使用。注意，你得预先安装相关依赖库的头文件：`python-devel`、`python3-devel`、`ruby-devel`、`lua-devel`、`libX11-devel`、`gtk-devel`、`gtk2-devel`、`gtk3-devel`、`ncurses-devel`。如果缺失，源码构建过程虽不会报错，但最终生成的 Vim 很可能缺失某些功能。

构建完成后，在 Vim 中执行：

```vim
:echo has('python')
```

若输出 `1`，则表示构建出的 Vim 已支持 Python；反之，`0` 则表示不支持。
