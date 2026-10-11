
1. 切换到 `root` 用户以安装 `Mesa` 图形库：

   ```
   $ su
   密码：
   ```

2. 从 CD 安装 `Mesa` 图形库（CD 驱动器的路径可能不同）：

   ```
   # rpm -Uvh /mnt/cdrom/Binaries/Extras/Mesa-3-0-2_i386.rpm
   ```

3. 回到你的普通账户：

   ```
   $ exit
   ```

4. 将 `WINE` 软件包拷贝到你的硬盘：

   ```
   $ cp /mnt/cdrom/Source/Office/Wine-990613.tar.gz /home/nwells/part5
   ```

5. 解压 `WINE` 存档：

   ```
   $ tar xvfz Wine-990613.tar.gz
   ```

6. 进入解压后创建的 `WINE` 目录：

   ```
   $ cd wine-990613
   ```

7. 配置 `WINE`：

   ```
   $ ./configure
   ```

8. 使用此命令编译 `WINE`（通常直接使用 `make` 即可，但 `WINE` 推荐使用这种格式）：

   ```
   $ make depend && make
   ```

   这一步可能需要 30 分钟完成。在编译过程中，你应该能看到文本偶尔在屏幕上滚动。完成后，可执行文件 `wine` 即可使用。

9. 将 `WINE` 文件安装到你 `Linux` 系统上的默认位置（执行此步骤可能需要变为 `root`）：

   ```
   $ make install
   ```

10. 将 `WINE` 提供的配置文件拷贝到你的家目录并重命名为 `.winerc`：

    ```
    $ cp /home/nwells/part5/wine-990613/wine.ini /home/nwells/.winerc
    ```

    此 `.winerc` 配置文件可能需要编辑，以对应你在 `Linux` 中挂载 `Windows` 分区的位置。（你不必在系统中安装 `Windows`）

`WINE` 是一个大型、复杂的程序，并不是所有 `Windows` 程序都能在 `WINE` 中启动，更不用说正确运行了。然而，越来越多的应用程序运行得尚可，`WINE` 开发者继续工作改进 `WINE`，使其能够运行更多应用程序。尽管软件包很复杂，但 `WINE` 与任何其他 `Linux` 应用程序一样易于编译和运行。一旦编译完成，在 `Linux` 中运行 `Windows` 程序就像使用如下命令一样简单：

```
$ wine sol.exe
```

要了解更多 `WINE`，请访问 `http://www.winehq.org`。

## 使用 WINE 运行新的 Windows 应用

尽管 `Wabi` 在当时是一项伟大的商业尝试，但 `WINE` 项目继续为 32 位应用程序开发 `Windows` 兼容代码。

`WINE` 不被认为是“成品”，但它已经可以运行一些基础的 32 位 `Windows` 应用程序（如 `Gnome` 桌面图中 23.1 所示的纸牌游戏）。

图 23.1 `WINE` 运行基础的 32 位 `Windows` 应用程序，例如纸牌游戏，同时仍在开发其他办公应用程序。

`WINE` 软件包位于 CD 上的 `/Source/Office`。它需要 `Mesa` 图形库，该库位于 `/Binary/Extras`（二进制 `rpm` 格式包）。

要编译源码并在你的系统上尝试 `WINE`，请按照以下步骤操作：

1. 切换到 `root` 用户以安装 `Mesa` 图形库：

   ```
   $ su
   密码：
   ```

2. 从 CD 安装 `Mesa` 图形库（CD 驱动器的路径可能不同）：

   ```
   # rpm -Uvh /mnt/cdrom/Binaries/Extras/Mesa-3-0-2_i386.rpm
   ```

3. 回到你的普通账户：

   ```
   $ exit
   ```

4. 将 `WINE` 软件包拷贝到你的硬盘：

   ```
   $ cp /mnt/cdrom/Source/Office/Wine-990613.tar.gz /home/nwells/part5
   ```

5. 解压 `WINE` 存档：

   ```
   $ tar xvfz Wine-990613.tar.gz
   ```

6. 进入解压后创建的 `WINE` 目录：

   ```
   $ cd wine-990613
   ```

7. 配置 `WINE`：

   ```
   $ ./configure
   ```

8. 使用此命令编译 `WINE`（通常直接使用 `make` 即可，但 `WINE` 推荐使用这种格式）：

   ```
   $ make depend && make
   ```

   这一步可能需要 30 分钟完成。在编译过程中，你应该能看到文本偶尔在屏幕上滚动。完成后，可执行文件 `wine` 即可使用。

9. 将 `WINE` 文件安装到你 `Linux` 系统上的默认位置（执行此步骤可能需要变为 `root`）：

   ```
   $ make install
   ```

10. 将 `WINE` 提供的配置文件拷贝到你的家目录并重命名为 `.winerc`：

    ```
    $ cp /home/nwells/part5/wine-990613/wine.ini /home/nwells/.winerc
    ```

    此 `.winerc` 配置文件可能需要编辑，以对应你在 `Linux` 中挂载 `Windows` 分区的位置。（你不必在系统中安装 `Windows`）

`WINE` 是一个大型、复杂的程序，并不是所有 `Windows` 程序都能在 `WINE` 中启动，更不用说正确运行了。然而，越来越多的应用程序运行得尚可，`WINE` 开发者继续工作改进 `WINE`，使其能够运行更多应用程序。尽管软件包很复杂，但 `WINE` 与任何其他 `Linux` 应用程序一样易于编译和运行。一旦编译完成，在 `Linux` 中运行 `Windows` 程序就像使用如下命令一样简单：

```
$ wine sol.exe
```

要了解更多 `WINE`，请访问 `http://www.winehq.org`。

## 街机上的 LINUX

你可能需要以 `root` 身份登录才能使用 `install` 命令。随着游戏的所有组件安装到你的系统上，会出现许多满屏文本的界面。此软件包是为 `Red Hat 6` 设计的。如果你使用的是其他发行版，则应该从源码包编译游戏。文件安装完成后，启动游戏：

```
$ kespueduel
```
