
# 第 5 章：Web 服务器性能

## 表 5-1：CONFIGURE 脚本的选项

| 选项 | 含义 |
| --- | --- |
| `--bindir=DIR` | 在 `DIR` [`PREFIX/bin`] 中用户可执行文件 |
| `--sbindir=DIR` | 在 `DIR` [`PREFIX/sbin`] 中系统管理员可执行文件 |
| `--libexecdir=DIR` | 在 `DIR` [`PREFIX/libexec`] 中程序可执行文件 |
| `--datadir=DIR` | 在 `DIR` [`PREFIX/share`] 中只读的架构无关数据 |
| `--sysconfdir=DIR` | 在 `DIR` [`PREFIX/etc`] 中只读的单机数据 |
| `--sharedstatedir=DIR` | 在 `DIR` [`PREFIX/com`] 中可修改的架构无关数据 |
| `--localstatedir=DIR` | 在 `DIR` [`PREFIX/var`] 中可修改的单机数据 |
| `--libdir=DIR` | 在 `DIR` [`PREFIX/lib`] 中的对象代码库 |
| `--includedir=DIR` | 在 `DIR` [`PREFIX/include`] 中的 C 头文件 |
| `--oldincludedir=DIR` | 在 `DIR` [`/usr/include`] 中非 GCC 的 C 头文件 |
| `--indir=DIR` | 在 `DIR` [`PREFIX/info`] 中的信息文档 |
| `--mandir=DIR` | 在 `DIR` [`PREFIX/man`] 中的 man 文档 |
| `--srcdir=DIR` | 在 `DIR` [`configure` 目录或 ...] 中查找源码 |
| `--program-prefix=PREFIX` | 在安装的程序名前加上 `PREFIX` |
| `--program-suffix=SUFFIX` | 在安装的程序名后加上 `SUFFIX` |
| `--program-transform-name=PROGRAM` | 在安装的程序上运行 `sed` `PROGRAM` |
| `--build=BUILD` | 为在 `BUILD` [`BUILD-HOST`] 构建进行配置 |
| `--host=HOST` | 为 `HOST` 配置 |
| `--target=TARGET` | 为 `TARGET` [`TARGET-HOST`] 配置 |
| `--disable-FEATURE` | 不包含 `FEATURE` (同于 `--feature=no`) |
| `--enable-FEATURE[ARG]` | 包含 `FEATURE` [`ARG=yes`] |

### 表 5-1：CONFIGURE 脚本的选项（续）

| 选项 | 含义 |
| --- | --- |
| `--with-PACKAGE[ARG]` | 使用 `PACKAGE` [`ARG=yes`] |
| `--with-PACKAGE` | 不使用 `PACKAGE` (同于 `--with-PACKAGE=no`) |
| `--x-includes=DIR` | X 文件位于 `DIR` |
| `--x-libraries=DIR` | 库文件位于 `DIR` |
| `--with-optim=FLAG` | 过时 (使用 `OPTIM` 环境) |
| `--with-port=PORT` | 监听的端口 (默认是 80) |
| `--enable-debug` | 开启调试和编译警告 |
| `--enable-maintainer-mode` | 开启调试和编译警告 |
| `--enable-layout=LAYOUT` | 使用布局 |
| `--enable-modules=MODULE-LIST` | 启用模块列表 |
| `--enable-mods-shared=MODULE-LIST` | 启用共享对象列表 |
| `--disable-access` | 基于主机的访问 |
| `--disable-auth` | 基于用户的访问 |
| `--enable-auth-anon` | 匿名用户访问 |
| `--enable-auth-dbm` | 基于 DBM 的访问 |
| `--enable-auth-db` | 基于 DB 的访问 |
| `--enable-auth-digest` | RFC2617 认证 |
| `--enable-file-cache` | 文件缓存 |
| `--enable-dav-fs` | 文件系统的 DAV 程序 |
| `--enable-dav` | Web 协议处理 |
| `--enable-echo` | ECHO 服务器 |
| `--enable-charset-lite` | 字符集转换 |
| `--enable-cache` | 动态文件缓存 |
| `--enable-disk-cache` | 磁盘缓存 |
| `--enable-ext-filter` | 外部过滤器 |
| `--enable-case-filter` | 大写转换 |
| `--enable-generic-hook-export` | hook 导出器 |
| `--enable-generic-hook-import` | hook 导入器 |

### 表 5-1：CONFIGURE 脚本的选项（续）

| 选项 | 含义 |
| --- | --- |
| `--enable-optional-fn-import` | hook 导入器 |
| `--enable-optional-fn-export` | hook 导出器 |
| `--disable-include` | 服务器端包含 |
| `--disable-http` | HTTP 协议处理 |
| `--disable-mime` | 文件扩展到 MIME 的映射 |
| `--disable-log-config` | 日志配置 |
| `--enable-vhost-alias` | 批量托管 |
| `--disable-negotiation` | 内容协商 |
| `--disable-dir` | 目录请求处理 |
| `--disable-imap` | Internalaps |
| `--disable-actions` | 请求触发动作 |
| `--enable-speling` | 纠正常见拼写错误 |
| `--disable-userdir` | 用户请求映射 |
| `--disable-alias` | 请求翻译 |
| `--enable-rewrite` | 正则 URL 翻译 |
| `--disable-so` | DSO 能力 |
| `--enable-so` | DSO 能力 |
| `--disable-env` | 环境变量的清除/设置 |
| `--enable-mime-magic` | 自动确定 MIME 类型 |
| `--enable-cern-meta` | CERN 类型文件 |
| `--enable-expires` | Expires 头控制 |
| `--enable-headers` | HTTP 头控制 |
| `--enable-usertrack` | 用户会话跟踪 |
| `--enable-unique-id` | 请求 ID |
| `--disable-setenvf` | 基于头的环境变量 |
| `--enable-tls` | TLS/SSL 支持 |
| `--with-ssl` | 使用特定的库安装 |
| `--with-mpm-MPM` | 为 Apache 选择进程模型：`MPM=(os threaded prefork perchild)` |

### 表 5-1：CONFIGURE 脚本的选项（续）

| 选项 | 含义 |
| --- | --- |
| `--disable-status` | 进程/线程监控 |
| `--disable-autoIndex` | 目录列表 |
| `--disable-asis` | 原始文件类型 |
| `--enable-info` | 服务器信息 |
| `--enable-suexec` | 为派生进程设置 UID 和 GID |
| `--disable-cgid` | CGI 脚本 |
| `--enable-cgi` | CGI 脚本 |
| `--disable-cgi` | CGI 脚本 |
| `--enable-cgid` | CGI 脚本 |
| `--enable-shared[--PKGS]` | 编译共享库 [`default=no`] |
| `--enable-static[--PKGS]` | 编译静态库 [`default=yes`] |
| `--enable-fast-install[--PKGS]` | 为快速安装优化 [`default=yes`] |
| `--with-gnu-id` | 假设 C 编译器使用 GNU ID [`default=no`] |
| `--disable-libtool-lock` | 避免锁定（可能会破坏并行构建） |
| `--with-program-name` | 可选可执行文件名 |
| `--with-suexec-caller` | 允许调用 SuExec 的用户 |
| `--with-suexec-userdir` | 用户子目录 |
| `--with-suexec-docroot` | SuExec 根目录 |
| `--with-suexec-uidmin` | 最小允许的 UID |
