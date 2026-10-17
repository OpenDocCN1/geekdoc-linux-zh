
`CLASPATH=$CLASPATH:$ANT_HOME/lib/ant.jar:$ANT_HOME/lib/xml-apis.jar:$ANT_HOME/lib/xercesImpl.jar`

`export ANT_HOME, JAVA_HOME, PATH, CLASPATH`

调用你的用户配置文件来设置环境，运行 Ant 命令获取帮助信息：

```bash
.bashrc_profile

ant -help
```

### 7.2.1 使用 Ant 的基础

Ant 脚本构建文件是用 XML 编写的。每个构建文件（`build.xml`）包含一个 `project` 元素。`project` 元素包含 `target` 元素，每个 `target` 包含一组 `task` 元素。

`task` 元素执行的功能如移动文件；编译项目；创建 JAR 包；或创建 EAR 包。

属性（`property`）有一个名称和值。它通过 `${property,name}` 引用，或者可以在整个构建文件中使用。属性值可以在构建文件内部设置，也可以从属性文件中外部获取。属性文件的优势是你可以为同一个构建文件设置不同的属性。你只需要更改属性文件来更改环境，而不需要修改构建文件。所有的操作系统路径都应该包含在此文件中。

路径（`path`）是一组目录或文件的集合。Java 编译使用路径引用来确定使用的类路径。

#### 表 7-1 ITSO 示例中的内置任务

| 内置任务 | 描述 |
| --- | --- |
| ant | 在提供的构建文件上运行 Ant |
| move | 将文件/目录移动到新的文件/目录。如果目标文件已存在，默认将进行覆盖 |
| echo |向当前 System.out 输出消息 |
| delete | 删除由一个或多个文件集指定的文件或目录 |
| javac | 编译 Java 源码树，将递归扫描源目录和目标目录以查找要编译的 Java 源文件 |
| mkdir | 创建目录 |
| tstamp | 设置包含日期和时间信息的属性。 |
| cvs | 处理从 CVS 存储库检索的包/模块 |
| jar | 将一组文件打包成 Java 归档文件 |
| war | 创建 Web 应用程序归档，包括应存在于 WEB-INF/lib、WEB-INF/classes 的文件 |
| ear | 创建一个类似于 JAR 任务的企业级应用归档文件。此文件包含整个企业级应用。 |
| exec | 在指定的操作系统通过 Ant 执行系统命令 |

### 运行 Ant

安装 Ant 后，我们可以通过在命令行提示符处输入 `ant` 来执行构建文件（`*build.xml*`）：

```
$ ant [options] [target1] [target2] [target3] ...
```

如果构建文件未命名为 `*build.xml*`，则需要使用 `-buildfile` 选项来指定构建文件的名称：

```
$ ant -buildfile [xml file] [target]
```

否则，您只需要运行：

```
$ ant
```

Ant 调用帮助函数（`help`）以查看额外的命令行选项：

```
$ ant -help
```

### 7.3 使用 Ant 构建 JEE 应用程序

本节总体概述了如何在 ITSO Bank 示例中使用构建工具 Ant 构建 J2EE 应用程序。这些内容将主要满足那些使用不同团队或模块交付源码构建大规模 J2EE 应用程序的开发者和部署人员的需求。对于这个社区来说，拥有一个强大且简单的构建工具来重现整个应用程序是有意义的。Ant 的创建是为了支持开发工作，但它也可以作为构建和部署工具用于更大的项目。

ITSO Bank 示例是一个 J2EE 企业级应用。该应用程序包含一个 Web 项目和一个 EJB 项目，并以模块名称的形式存储在 CVS（并发版本系统）中（表 7-2）。我们使用 CVS 系统获取所有源代码和配置文件，以便在 Linux 环境下启动 ITSO Banking 的构建文件。

#### 表 7-2 JEE 项目到 CVS 模块的映射

| 项目名称 | CVS 模块名称 |
| --- | --- |
| 企业级应用项目 | ITSOBankEAR |
| Web 项目 | ITSOBankWeb |
| EJB 项目 | ITSOBankEJB |

CVS 模块名称的结构也描述了 Linux 环境下的目录结构，类似于 J2EE 的命名规范。在 Linux 文件系统中，我们将构建过程创建以下结构（图 7-1）。

+ build
  lib
    sqlitext.jar
    j2ee.jar
  dest
    ITSOBankEAR.ear
  ITSOBankEAR
  ITSOBankEJB
  ITSOBankWeb
    build.xml
    osamus1.properties

**图 7-1** 构建目录的文件系统结构

构建文件命名为 `build.xml`，并使用 `osamus1.properties` 文件提供 Linux 下的环境信息。该属性文件包含了构建 J2EE 应用程序的所有重要类路径。为了在构建过程中修改或添加类路径，必须在该属性文件中进行。构建文件 `build.xml` 内部包含表 7-3 所示的 `target`（`targets`）。

#### 表 7-3 build.xml 的目标名称

| 目标名称 | 描述 |
| --- | --- |
| init | 启动构建的实际 |
| clean | 删除所有生成的文件 |
| getcvs | 从 CVS 存储库导出所需项目，模块为 ITSOBankEAR、ITSOBankWeb 和 ITSOBankEJB |
| web-compile | 将 ITSOBankWeb 项目源码编译为 .class 文件 |
| ej-compile | 将 ITSOBankEJB 项目源码编译为 .class 文件 |
| ej-jar | 创建 EJB 项目的 JAR 文件，依赖于 ej-compile |
| ej-deploy | 为 WebSphere 服务器生成部署代码，调用部署工具 |
| war | 创建项目的 war 文件 |
| ear | 创建整个项目的 ear 归档文件 |

接下来的章节详细描述了构建文件中的目标。

### 设置属性和 ant 元素

理解 Ant 操作最重要的概念是属性（`properties`）的含义。属性类似于变量，因为它们在名称和值之间建立映射，并且在概念上与 `java.util.Properties` 非常相似。Ant 属性取决于它们的使用上下文，在构建文件中通过 `${property.name}` 表示。

`property` 任务允许构建文件定义自己的属性集。我们使用的变体是 `name/value` 属性，以及从构建文件中加载一组属性。

我们在构建文件中使用了 `property` 标签来将配置和设置数据加载到构建文件中...

```
[echo] J2EE Project Banking 示例构建开始于 2002年10月19日 1155

BUILD SUCCESSFUL
```

### Clean target

初始化后的下一个目标是 `clean target`。在我们的示例中，我们清理了目录结构。这对于开始新的构建非常重要，可以确保没有来自之前构建周期的旧依赖项。`<delete>` 任务会删除构建周期中的模块和子目录。这些目录包含了构建周期所需的所有包和模块。完成清理后，我们就可以开始新的构建。

示例 7-7 为新构建周期准备的的环境

```
<target name="clean" depends="init">

  <echo message="Clean all" />

  <delete dir="${ear.project}" />

  <delete dir="${web.project}" />

  <delete dir="${ejb.project}" />

  <delete dir="${dest}" />

</target>
```

### Target getcsv

在本书的开发过程中，我们使用 CVS 服务器作为仓库，在 WebSphere Studio 中编写示例代码。J2EE 项目结构与 CVS 中的模块结构相同。我们必须在 Linux 下更新构建结构，并使用新的代码级别来构建 J2EE 。在此之前，我们必须在 CVS tag 版本中创建一个代码基线。该版本是我们用于构建 ITSO Bank 示例的驱动。在示例中，我们在属性文件中设置属性以配置与 CVS 服务器的连接。

示例 7-8 CVS 属性

```
# CVS Properties

cvs.home=:pserver=osamers1:osamers1@dhcp39039.almaden.ibm.com:/home/cvs/cvsrep

cvs.command=export -r itslo_1

ear=ITSOBankEAR

war=ITSOBankWeb

eb=ITSOBankEJB
```
