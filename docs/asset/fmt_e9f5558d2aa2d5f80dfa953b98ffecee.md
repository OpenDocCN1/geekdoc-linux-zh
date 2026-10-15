
如果你无法直接从 Linux 镜像访问，请将 tar 文件下载到你的工作站并复制到 Linux。以下是直接从互联网下载 64 位发行版 tar 文件的示例。在控制器或任何其他虚拟机上使用 SSH 会话。

1. 切换目录到 `/usr/local/src/`：

    ```
    # cd /usr/local/src/
    ```

2. 使用 `wget` 命令下载适当的文件。对于 64 位 SLES 9 和 SLES 10，使用：

    ```
    # wget ftp://ftp.software.ibm.com/eserver/zeries/zos/rmf/rmfps_s390_kernel26.tgz
    ```

3. 对于 RHEL 4 和 5，使用 `wget` 命令：

    ```
    # wget ftp://ftp.software.ibm.com/eserver/zeries/zos/rmf/rmfps_s390_kernel26_rhel4.tgz
    ```

4. 使用 `tar` 命令解压文件并复制到 `rmfps/`：

    ```
    # tar xzf rmfps_s390_kernel26.tgz
    # ls
    # cd rmfps/
    # # bin enable_autostart
    .rmfms_config README
    .rmfms_config_autostart
    ```

5. 你应该能够通过以下命令在 `bin/` 目录启动 `rmfms`：

    ```
    # bin/rmfms start /rmfms

    Starting /root/rmfms/ backends...
    DSRV: RMF-DOS-Server-Beta (Sep 2007) started.
    DSRV: Functionality Level=2
    DSRV: Reading exceptions from gpmsys.ini and gpexusr.ini.
    DSRV: Server will now run as a daemon.
    done
    ```

6. 运行后，你可以通过浏览器访问 Linux 镜像端口 `8803` 查看性能数据，如图 14-4 所示。

![](img/57d3457c1c2ef8ee20ea427808ec95_224_0.png)

你也可以使用 Performance Toolkit 查看 Linux 镜像，如第208页第14.4节“在 Performance Toolkit 中查看 Linux 数据”所述。

## 直接从内核监控 Linux 性能数据

要直接从内核监控 Linux 性能数据，必须满足以下两个要求：

1. 必须在用户目录中设置 `APPLMON` 选项。
2. 内核必须已构建监控功能。

第一个要求是在控制器在之前的章节中设置的。

对于第二个要求，SLES 9 和 SLES 10 都内置了此功能。该功能的简要说明位于设备驱动，可以通过以下地址访问：
`http://www-128.ibm.com/developerworks/linux390/2005_documentation.html`

关于此内置功能的说明如下：

1. 内核中内置但未加载三个模块：`appdata_mem`、`appdata_os` 和 `appdata_net_sum`。可以使用 `lmod` 命令和 `grep` 命令验证它们未加载：

    ```
    # lmod | grep appdata
    ```

2. 没有输出，这意味着没有字符串 `appdata` 的模块。使用 `modprobe` 命令加载这些模块：

    ```
    # modprobe appdata_mem
    # modprobe appdata_os
    # modprobe appdata_net_sum
    ```

3. 再次执行 `lmod` 命令，你应该看到：

    ```
    # lmod | grep appdata
    appdata_net_sum      20064 0
    appdata_os          22536 0
    appdata_mem        20576 0
    ```

4. 使用 `echo` 命令为 `/proc` 文件系统中的四个监控变量设置非零值以开启内核监控：

    ```
    # echo 1 / /proc/sys/appdata/timer
    # echo 1 / /proc/sys/appdata/mem
    # echo 1 / /proc/sys/appdata/os
    # echo 1 / /proc/sys/appdata/net_sum
    ```

> 注意：我们不建议一直运行 Linux 数据收集器，因为可能会导致严重的性能问题。相反，仅在特定时间段和有性能问题需要调查时启动收集器。此外，由于捕获了 Linux 监控，Performance Toolkit 的磁盘空间可能会很快填满。

## 14.4 在 Performance Toolkit 中查看 Linux 数据

系统收集一段时间数据后，你应该能够使用 Performance Toolkit 查看 Linux 数据。如第199页第14.2.2节“配置 Web 浏览器支持”所述，`FCONX LINUSR` 文件中应有条目。

查看该数据，深入进入菜单 29，Linux 系统。这可以通过浏览器界面或如图 14-5 所示的 3270 接口完成。

FCX242  CPU 2094  SER 2991E  Linux Displays

Linux 屏幕选择

| S Display | Description |
| --- | --- |
| - `LCPU` | RPF 系统选择菜单 |
| - `CPU` | CPU 活动摘要显示 |
| - `LXMEM` | 内存利用率及活动摘要显示 |
| - `LXNETWRK` | 网络活动摘要显示 |

用光标选择性能屏幕并按 `ENTER`
命令 ===>
图 14-5 Linux 客户子菜单

在子菜单窗口左侧对应于你想查看的报告的行输入 S。你将看到一个新的报告窗口，其中包含 Linux 客户系统的 CPU 概览。

## 14.5 常见性能工具包问题

当浏览性能工具包时，请检查 Performance Toolkit 控制台异常。如果你收到 `FCXPMON446E Incomplete monitor data: DCSS size too small` 或 `FCXPMON446E Incomplete monitor data: SAMPLE size too small`，你必须采取行动；否则，数据可能会错误或缺失（即你的数据可能存疑）。

要增大 `SAMPLE CONFIG` 或 `EVENT CONFIG`，你可能可以在 `PRFSVM PROFILE EXEC` 中使用或添加以下命令：

- `* CP MONITOR SAMPLE CONFIG SIZE xxx`
- `* CP MONITOR EVENT CONFIG size yyy'`

要增大 `DCSS`，这里有一个提示。首先，通过输入以下命令确定当前 `MONCSS` 的位置：

```
qss name mondcss map
```

这将产生类似于下面的输出：

```
FILEFILENAME MINSIZE BEGPAG ENDPAG CL #USERS PARREMS VGGROUP
7271 MONCSS CPDCSS N/A 03300 06FFR SC R 00007 N/A N/A
```

在此示例中，它从 `x3300` 开始，到 `x6FFF` 结束（这是一个页边界）。你还需要执行 `q nss all map` 来确定新的 `MONDCSS` 可以存放在何处且不重叠。

**重要：** 仔细检查以确保新的 `MONDCSS` 不与其他任何 `NSS` 重叠。如果重叠，`PERKIT` 可能无法使用它。

测试 `MONDCSS` 段的一种方法是在启动 `PERKIT` 之前加载 `SEGMENT LOAD MONDCSS`。如果它返回任何错误（例如 `DMDSCS343E`），则可能存在重叠，你将不得不重新定义 `MONDCSS` 的位置。

通常，你只需提高当前 `MONDCSS` 的结束位置即可解决此问题。

首先，通过以下删除旧的 `MONDCSS`：

```
PURGE NSS NAME MONDCSS
```

如果有任何用户当前连接到 `MONDCSS`，你需要注销这些用户。你可以通过执行 `MONITOR` 来确定谁正在连接。

创建一个新的 `MONDCSS`：

```
CP DEFSEG MONDCSS 03300-09FF SC RSSTD
```

保存新的 `MONDCSS`：

```
CP SAVESEG MONDCSS
```
