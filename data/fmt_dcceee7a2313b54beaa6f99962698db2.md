
如第 15.2.6 节所示，为了让链接器在 `lib_dir` 中查找，我们使用此命令：

```
$ LDFLAGS=-Llib_dir ./configure
```

如果 `lib_dir` 中包含共享库（参见第 15.1.4 节），`configure` 可能不会设置运行时动态链接器路径。在这种情况下，除了 `-l` 之外，使用 `-rpath` 链接器选项：

```
$ LDFLAGS="-Llib_dir -Wl,-rpath=lib_dir" ./configure
```

设置变量时要小心。一个小疏忽就会导致编译器出错并引起 `configure` 失败。例如，如果你忘记了 `-I`，如下所示：

```
$ CPPFLAGS=-Iinclude_dir ./configure
```

这将产生如下所示错误：

```
configure: error: C compiler cannot create executables

See 'config.log' for more details
```

深入分析由失败尝试生成的 `config.log` 会得到如下内容：

```
configure:5037: checking whether the C compiler works
configure:5059: gcc include_dir config.c >&8ngcc: error: include_dir: No such file or directory
configure:5063: $? = 1
configure:5301: result: no
```
