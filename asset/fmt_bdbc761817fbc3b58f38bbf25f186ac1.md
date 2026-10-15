
```bash
echo "done."

echo -n "Copying $ORIG_DIR to $MOUNTPONT ... "

$CP -r $ORIG_DIR $MOUNTPONT

echo "done."

echo -n "Changing ownership to $USER:$GROUP for $MOUNTPONT ... "

$CHOWN -R $USER:$GROUP $MOUNTPONT

echo "done."
```

要在系统上使用该脚本，请执行以下操作：

1. 在 `/usr/local/scripts` 目录中创建 `make_ramfs.sh`。如果没有该目录，请创建 `/usr/local/scripts` 目录。
2. 编辑 `/etc/rc.d/rc.local` 文件并在其中追加以下行：
   `/usr/local/scripts/make_ramfs.sh`
3. 使用 `mkdir ram` 命令创建一个名为 `ram` 的目录。如果你想将加载到 RAM 中的文件保存在 `/www/commonfiles` 以外的任何位置，请修改脚本中 `ORIG_DIR` 变量的值。例如，如果你的文件位于 `/www/mydomain/htdocs/common` 目录中，请将此变量设置为指向该目录。
4. 如果你使用除 `httpd` 以外的用户名或组来运行 Web 服务器，则相应地修改 `USER` 和 `GROUP` 变量的值。例如，如果你以 `nobody`（用户和组）运行 Apache，则设置 `USER=nobody` 和 `GROUP=nobody`。
5. 如果你正在使用 Apache Web 服务器，请在 `httpd.conf` 文件中创建一个别名，如下所示：

```text
Alias /commonfiles/ "/ram/commonfiles/"
```
