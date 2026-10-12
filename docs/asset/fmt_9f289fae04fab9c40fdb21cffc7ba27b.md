
`FASIT Storage Manager`软件并不包含所有操作系统的代理进程。例如，没有在 Linux 下运行的代理。如果有一个主机通过光纤连接到 `FASIT` 并运行 `Storage Manager` 代理，则 Linux 系统可以运行 `Storage Manager` 客户端并通过带内控制管理 `FASIT` 系统。在这种情况下，Linux 系统上的 `Storage Manager` 客户端将与非 Linux 系统上的代理通信。然而，如果连接到 `FASIT` 存储系统的所有主机都是 Linux 主机，或者没有可作为管理代理候选的可用代理软件连接主机，则必须使用带外控制。

对于此讨论，我们假设环境是纯 Linux 的，并将使用带外控制管理 `FASIT`。

### A.1.3 Linux 是否有 RDAC 驱动？

在编写本文时，冗余磁盘阵列控制器 (`RDAC`) 适用于 Linux。这意味着使用 `FASIT` 存储的 Linux 主机，其卷传输由 `FASIT` 自身管理。多路复用使用主总线适配器 (`HBA`) 的相应驱动程序以及名为 `FASIT MSI` 的额外软件，该软件用于管理与适配器的路径。`FASIT MSI` 在附录 B，“Java FASIT 管理套件”第 75 页中有描述。

From here, navigate to Disk Storage Systems², then `FASIT Storage Server` and then select your `FASIT` model; use the pull-down menu to select Downloads, then select `FASIT Storage Managers` as appropriate for your version.

Read and accept the terms and conditions, and you now see a selection of both software and documentation. Please obtain and read the documentation entitled “`IBM TotalFASIT Storage Manager` Version X.Y installation and Support Guide for Linux” (where X corresponds to your version number); use your browser’s “back” button and select LINUX operating system; this action takes you to the download page for the code and the `README` file. Please look at the `README` file before installing, as it contains the latest information for the code.

The package is rather large (over 30 MB) and requires another 70 MB to install, including the Java Environment, storing the rim files, and the installed code. Also, note that the `Storage Manager` GUI requires the X window system running on the management workstation.

When you have to root to install the client. Site administrators may make their decisions regarding access control to the `Storage Manager`. The `FASIT` itself can be protected by password from changes to the Storage configuration inaccessible of access to the `Storage Manager` client.

First, uninstall any previous version of `Storage Manager` before installing the new version. To check for installations, query the packages that are installed and select only those containing the letters "SM” with the following command:

```
rpm --query --all grep SM
```

Use the output to remove any previous version of the `Storage Manager` software by name. For example:

```
rpm --uninstall Runtime-XX.YY.ZZ-1
```

When you have obtained the latest version of `Storage Manager`, extract the contents of the zipped file:

```
tar xzv *.tgz
```

The required rpm files for installation are extracted into `./Linux/SMXclientcode` where X-Storage Manager version.

```
rpm --install --verify SMClient-<version>.rpm
rpm --install --verify SMClient-LINUX-<version>.rpm
rpm --install --verify SMUtil-<version>.rpm
```

The `Storage Manager` components should be installed in `/opt/IBM/FASIT`, with the client and command install, `SMClient`, in `/opt/IBM/FASIT/client` directory.

### A.2.2 Launching Storage Manager and connecting to the FASIT

To launch `Storage Manager`, open a terminal window and type `SmClient`⁴. Alternatively, you can launch `Storage Manager` from the graphical interface menus: Check the Gnome or KDE icon -> Programs -> Utilities -> `IBM FASIT Storage Manager`.

- ² Navigation details may change from time to time, these instructions were correct as of April 2003

- ³ We use the long names for clarity. Experienced users will know of versions of the options. Please see the documentation (man `rpm`) for more information

- ⁴ You may need to add the directory to your path. Otherwise, use the full path to `SMClient`

Appendix A. `Storage Manager` and Linux 6

The screen shown in Figure appears, asking if you wish to Automatically Discover the storage. This method will not find direct-attached storage controllers. Close this screen with the Enterprise Management Window (Figure 5-6).

![](img/69bfe4e2d59e61df50eecde9154775d5_77_0.png)

Figure 5-5 Automatic Discovery screen

![](img/69bfe4e2d59e61df50eecde9154775d5_77_1.png)

Figure 5-6 Storage Manager Enterprise Management window
