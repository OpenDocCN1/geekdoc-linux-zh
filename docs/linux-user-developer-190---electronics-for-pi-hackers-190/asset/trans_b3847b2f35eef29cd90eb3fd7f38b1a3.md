

# Linux 必备析

## 使用 GNU Make 构建程序：不常用法

GNU Make 是一个非常强大的程序，它通常可以用于构建之外的其他用途。在之前的系列中，我们已经学习了使用 Make 自动化构建的基础知识，以及处理并行项目的更高级概念和技术。在本教程中，是时候用一种不同的方法来看 Make 了。我们将展示如何以与之前完全不同的方式使用它。

我们将提供两个案例研究，首先是一个用于将文件从一个目录复制到另一个目录的 Makefile。然后，我们将扩展 Make 的并行处理能力。

每个案例研究都利用了 Make 的完整功能；每个案例将充分利用一个特定特性。目标是帮助你将 Make 视为一个强大的自动化套件，可以用于你的日常 Linux 管理中，而不仅仅是一个软件构建工具。由于许多 Linux 发行版默认带有 Make，因此它为不常用法提供了一个便携的替代方案。我们希望在本文之后，你能想到 Make 的一些不常用法。

# 作为同步工具的 Make

假设我们正在构建一个网站。网站位于外部服务器 webserver.example.net 上，但我们想更新网站文件。如果我们本地仓库中有三个文件 index.html, style.css 和 script.js，我们可能会使用类似下面的命令将它们复制到服务器：

## 资源

```make
# Makefile
DHFLAGS=-parallel

export DEKG_BUILD_OPTIONS = hardening=all
DPKG_EXPORT_BUILDS = 1
include /usr/share/dpkg/builddeps.mk

all: $(DHFLAGS)

override_install:
	install=fail-missing

override_auto_config:
	CONFIGURE=1 ../autogen.sh \
	auto_config=$(shell \
	disable-silent-rules \
-libdebexdir=/usr/lib/byte-applets \
-localstatedir=/var \
-disable-any=1 \
-with-cpufreq=libcpufreq

override_dh:
	strip --dpkg-system="make-apt-build-pkg (<= 1.28.0-1)"

get-source:
	ction -noconf --force-download --rename=download:current.version --destdir==
```

上面的 Make 也可以用于打包 Debian 文件 - 参见相反页的小册

```bash
scp index.html style.css script.js \
luad@webserver.example.net:/home/load/public_html
```

这对于小型网站是有效的，但很快我们就会有一个包含多个目录多个文件的大型项目，复制到服务器可能需要很长时间。写一个脚本来复制已经足够了，但如果我们对其中一个文件进行了更改，就不需要复制整个内容；我们只想复制更改的文件。

这个问题的答案是构建一个同步工具，它告诉我们自上次以来哪些文件发生了变化，并仅将这些文件复制到服务器。Make 的整个操作都是围绕文件的修改时间进行的，因此将其作为构建同步工具的工具是有意义的。

> 目标是帮助你将 Make 视为一个可以用于日常 Linux 管理的自动化套件

为了进行测试，我们将使用一个 shell 脚本来模拟文件复制到服务器的过程。你可以在 server.copy.sh 找到这个脚本。脚本会要求密码，如果密码正确，它会将给文件复制到服务器。密码是 swidth，不过你可以在这里找到：

```bash
$ index.html style.css
$ /server.copy index.html
Password: swidth
index.html copied to server:
script.js copied to server: 
```

我们使用一个（唯一的）辅助文件 .last_push，它的最后一个功能是记录我们上次推送到本地仓库的时间。在我们将更改推送到服务器之前，我们运行 `touch last_push` 命令。

当任何一个文件自上次推送以来发生变化变化时，我们将文件复制到服务器。这表明我们要推送到服务器的所有文件都应该是 last_push 的依赖项。

```make
FILES = *.html *.css *.js
last_push = $(FILES)
```

last_push 的配方应该包含 `touch last_push` 命令以便更新时间戳。我们还应该让它负责将所有文件推送到服务器。此此的关键是使用自动变量 `$`，它被填充为所有比该规则更新的当前依赖项列表；在这种情况下，恰恰是自上次推送到服务器以来已修改的文件列表。

# 图 1

```make
FILES = *.html *.css *.js
LAST_PUSH = .last_push
SCP = ./server_copy.sh
PHONY: push
push: $(LAST_PUSH)
	$(SCP) $(FILES)
	touch $(LAST_PUSH)
```

```make
.last_push : $(FILES)
	./server.copy $$
	touch .last_push
```

使用变量来保持可维护性的完整 make 是如图 1 所示。你可以使用 `make sync` 运行它。

```bash
$ make push
./server.copy index.html script.js
Password: swidth
index.html copied to server:
style.css copied to server:
touch .last_push
```

现在，如果我们有多个文件，其中一个被复制的：

```bash
$ make push
./server.copy index.html
Password: swidth
index.html copied to server:
touch .last_push
```

最后，我们需要验证要找到的文件的值，以便找到我们想要跨复制的所有文件。我们可以通过程序化的方式实现这一点，使用一个 shell 函数调用该工具。该函数将搜索目录及其子目录中扩展名为 html、css 或 js 的文件。

```make
FILES = $(find . -name *.html -o -name *.css -o -name *.js -o -name *.jpg)
```

在这里，我们使用 `$(shell ......))` 函数，我们现在可以添加具有相同扩展名的文件我们的同步工具仍然能够复制它们。

- deb 规则文件
使用 Make 的一个重要原因是在 Debian 发行版中。每个带有 Makefile 的 Debian 发行版都是独特的。

# 并行处理

Make 最强大的功能之一是并行处理能力。默认情况下，Make 按顺序执行规则，但除非我们使用，我们可以使用操作系统的任务调度器自动这样做，以确保哪些工作并发，哪些需要顺序执行。

要启用此，我们在运行 make 时使用 -j，如果我们指定作业数 - make -j 将限制同时执行的任务数。如果我们运行 -j 而不指定数字，线程数将以无限制模式运行。

使用命令行开关使用 -j 1，这在系统高负载时让 Make 限制其并发运行的线程数。负载水平通过在我们运行 uptime make 命令时体验平均负载来衡量。

```bash
$ uptime
10:37:13 59 min, 3 users
average: 0.31, 0.34, 0.53
```

# 图 2

```bash
LAST_PUSH=:last_push
for f in "*";*.css; do
  if [ "$f" != "$LAST_PUSH" ]; then
    LAST_PUSH="$f"
  fi
done
scp $LAST_PUSH linux@linux.org:/home
touch LAST_PUSH
```

虽然我们可以使用 shell 脚本构建同步工具，但它比图 2 中的规则更不灵活且更难配置

