
如果编译失败，请检查错误信息以获取原因，并在重新之前运行

```
$ make clean
```

如果你不喜欢该软件，也可以运行

```
$ make uninstall
```

来移除该软件。

运行 `make install` 的替代方案是一个名为 `CheckInstall` 的程序，它可以为你的安装生成一个 `.rpm` 文件。这种方法允许 RPM 数据库感知并跟踪你正在安装的所有文件。更多信息请参阅下文关于 CheckInstall 的侧边栏。

> 一款实用的软件安装工具——CHECKINSTALL
>
> 当你从源码编译并安装应用程序时，它们不会显示在 RPM 数据库中，因此无法通过 RPM 进行管理。
>
> 你可以使用名为 CheckInstall 的程序为这些应用程序提供 RPM 管理。在简单的情况下，`checkinstall` 是从源码构建时 `make install` 步骤的直接替代品。
>
> 例如，当从源码编译时，传统上你会使用：
>
> ```
> # ./configure
> # make
> # make install
> ```
>
> 使用 CheckInstall，步骤将如下：
>
> ```
> # ./configure
> # make
> # checkinstall
> ```
