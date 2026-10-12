
## 7.4.6. OpenSCAP 在线修复

在线修复会在扫描时执行修复元素。评估和修复作为单个命令的一部分执行。

要启用在线修复，请使用 `--remediate` 命令行选项。例如，若要使用 scap-security-guide 包执行在线修复，请运行：

```bash
~]$ oscap xccdf eval --remediate --profile xccdf_org.ssgproject.content_profile_rht-ccp --results scan-xccdf-results.xml /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

此命令的输出由两部分组成。第一部分显示修复前的扫描结果，第二部分显示应用修复后的扫描结果。第二部分可能仅包含**已修复**和**错误**结果。**已修复**结果表示修复后执行的扫描通过了测试。**错误**结果表示即使应用了修复，评估仍未通过。

### 7.4.6.1. OpenSCAP 在线修复详情

- 3. **OpenSCAP** 搜索合适的修复元素，解析它，准备环境，并执行修复脚本。
- 4. 修复脚本的任何输出都会被 **OpenSCAP** 捕获并存储在 `rule-result` 元素中。修复脚本的返回值也会被存储。
- 5. 每当 **OpenSCAP** 执行修复脚本时，它会立即再次评估 OVAL 定义（以验证修复脚本是否正确应用）。在此第二次运行中，如果 OVAL 评估返回成功，规则的结果为**已修复**，否则为**错误**。
- 6. 修复的详细结果存储在输出 XCDF 文件中。它包含两个 `TestResult` 元素。第一个 `TestResult` 元素代表修复前的扫描。第二个 `TestResult` 基于第一个元素派生，并包含修复结果。

关于修复，**OpenSCAP** 有三种操作模式：在线、离线和审查。

### 7.4.6.2. OpenSCAP 离线修复

离线修复允许您推迟执行修复。在第一步中，系统仅被评估，结果存储在 XCDF 文件的 `TestResult` 元素中。

在第二步中，`oscap` 执行修复脚本并验证结果。将结果存储到输入文件中是安全的，数据不会丢失。在离线修复过程中，**OpenSCAP** 创建一个基于输入元素的新 `TestResult` 元素，并继承所有数据。新创建的 `TestResult` 仅在对其中 `rule-result` 元素中失败的部分有所不同。对于这些失败的部分，将执行修复。

若要使用 scap-security-guide 包执行离线修复，请运行：

```bash
~]$ oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_rht-ccp --results scan-xccdf-results.xml /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
~]$ oscap xccdf remediate --results scan-xccdf-results.xml scan-xccdf-results.xml
```

### 7.4.6.3. OpenSCAP 修复审查

审查模式允许用户将修复指令存储到文件中以供进一步审查。在此期间不会执行修复内容。

若要生成 shell 脚本形式的修复指令，请运行：

```bash
~]$ oscap xccdf generate fix --template urn:xccdf:fix:script:sh --profile xccdf_org.ssgproject.content_profile_rht-ccp --output my-remediation-script.sh /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

## 7.4.7. 为 DISA STIG 查看器导出 XCCDF 结果

DISA STIG 查看器允许用户从 DISA 规则 ID 的角度查看结果。该实用程序期望使用 DISA（国防信息系统局）STIG（安全技术实施指南）标识符（例如 `SV-86555r1_rule`）作为规则 ID。在大多数公开可用的 SCAP 内容中，惯例是将 DISA STIG ID 作为引用或标识符附加到 XCCDF 规则上。因此，由 OpenSCAP 和 SCAP Security Guide 生成的 XCCDF 结果在 DISA STIG 查看器中打开时不可读。

OpenSCAP 允许您将 XCCDF 结果输出为与 DISA STIG 查看器兼容的格式。转换过程会获取附加的 STIG 规则 ID 引用，并替换 XCCDF 规则 ID。

> **示例 7.12. 扫描系统以符合 DISA STIG 并生成 STIG 查看器结果**
>
> 要扫描本地系统以符合 DISA STIG 并生成可在 DISA STIG 查看器中打开的 XCCDF 结果：

```bash
$ oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_stig-rhel7-disa --stig-viewer stig-results.xml /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

要在 DISA STIG 查看器中查看 XCCDF 结果，请首先导入您选择的 STIG，并创建一个检查清单。创建好检查清单后，使用“导入 → XCCDF 结果文件”菜单项导入您的结果。

**注意**

请注意，您可以使用其他任何 `oscap` 选项与 `--stig-viewer` 选项一起使用，以导出具有常规规则 ID 的结果。

有关 STIG 查看的更多信息，请参阅 IASE STIG 查看指南网页。

## 7.5. 在 Docker 中使用 OPENSCAP

`oscap-docker` 命令行实用程序允许用户使用 `oscap` 程序扫描其 docker 格式的容器镜像和容器。

以下部分：
- 解释 `oscap-docker` 的安装
- 提供基本的使用示例

要了解有关子命令的更多信息，请在使用 `oscap-docker` 或 `oscap` 命令时使用 `--help` 选项。

**注意**

由于容器文件系统受挂载点影响，扫描镜像的结果可能与从该镜像创建的容器的扫描结果不同。例如，自定义路径中仅提供容器内进程数据的挂载点不会影响扫描结果。但是，容器中针对 `/bin`、`/etc` 或 `/var` 等路径提供的挂载点，若包含新的二进制文件或配置文件，可能会导致扫描结果出现差异。

要启用镜像和容器的扫描，请安装 docker 包。有关安装 Docker 的说明，请参阅《容器入门》指南中“在 Red Hat Enterprise Linux 7 中获取 Docker”章节。

输入以下命令安装 `oscap-docker`：

```bash
# yum install openscap-utils
```

以下示例使用 Red Hat Enterprise Linux 7 镜像。

```bash
# docker pull registry.access.redhat.com/rhel7
```

```bash
# docker images
REPOSITORY                      TAG                 IMAGE ID
registry.access.redhat.com/rhel7   latest              c453594215e4
```

### 7.5.1. 扫描 Docker 格式镜像和容器中的漏洞

`oscap-docker` 命令提供两种扫描镜像和容器漏洞的方法：
- `image-cve` 或 `container-cve` 子命令确定操作系统版本，下载适用于给定系统的 CVE 流，并运行漏洞扫描：

```bash
# oscap-docker image-cve registry.access.redhat.com/rhel7
```

- 另一种更灵活的方法允许您在检查漏洞时指定 OVAL 定义。使用 `image` 或 `container` 子命令配合 `oscap` 的 OVAL 评估参数。例如，若要使用从 Red Hat OVAL 仓库下载的 definitions 文件扫描镜像，请使用以下命令：

```bash
# oscap-docker image registry.access.redhat.com/rhel7 oval eval com.redhat.rhsa-all.xml
```

### 7.5.2. 扫描 Docker 格式镜像和容器的配置合规性

要扫描配置合规性，请使用 SCAP Security Guide (SSG) 提供的 SCAP 内容。确保已安装 scap-security-guide 包：

```bash
# yum install scap-security-guide
```

若要验证 Red Hat Enterprise Linux 7 镜像是否符合国防信息系统局安全技术实施指南（DISA STIG）策略，请输入以下命令：

```bash
# oscap-docker image registry.access.redhat.com/rhel7 xccdf eval --profile xccdf_org.ssgproject.content_profile_stig-rhel7-disa /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

以下命令扫描 ID 为 5ef05eef4a01 的容器的运行环境：

```bash
# oscap-docker container 5ef05eef4a01 xccdf eval --profile xccdf_org.ssgproject.content_profile_stig-rhel7-disa /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

要获取包含结果的 XML 文件，请使用 `--results` 参数；要为评估生成 HTML 报告，请添加 `--report` 参数。有关更多信息，请参阅 `oscap (8)` 手册页。

## 7.6. 在 ATOMIC 扫描命令中使用 OPENSCAP

atomic scan 命令允许用户使用 OpenSCAP 扫描功能来扫描系统中的 docker 格式容器镜像和容器。可以扫描已知的 CVE 漏洞或配置合规性。此外，用户可以将 docker 格式容器镜像修复到指定的策略。

### atomic scan 和 OpenSCAP 扫描器镜像

要安装用于容器管理的 atomic 工具，请输入以下命令：

```bash
# yum install atomic
```

有关 atomic 安装的更多信息，请参阅 Atomic CLI 参考中的先决条件。

安装 atomic 工具后，还需要一个扫描器，它被 atomic scan 命令用作扫描镜像和容器的后端。Red Hat 建议选择 registry.access.redhat.com 镜像注册表中 rhel7/openscap 容器镜像中捆绑的 OpenSCAP 扫描器：

```bash
# atomic install registry.access.redhat.com/rhel7/openscap
```

registry.access.redhat.com/rhel7/openscap 容器镜像被 atomic scan 命令用作默认扫描器。它目前支持针对 Red Hat Enterprise Linux 系统的两种扫描类型。要列出支持的扫描类型，请输入以下命令：

