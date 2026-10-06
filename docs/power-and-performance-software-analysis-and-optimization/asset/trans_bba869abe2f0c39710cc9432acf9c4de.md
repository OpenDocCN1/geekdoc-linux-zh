
通过合并操作。相反，将在默认的 `test-results` 目录中创建一个新结果，其名称以 `merge-` 开头。

## 5.4.3 创建自定义测试

无论是否发布，向默认库中添加自定义测试都非常简单。本质上，测试配置是一个 XML 文件和可执行文件（通常是 shell 脚本）的集合，用于安装和基准测试。

首先，在 `$HOME/.phoronix-test-suite/profiles/local` 为测试配置创建一个新目录。在该目录下，将创建安装测试所需的所有文件（外部资源除外）。此 XML 文件

测试配置的核心是 `test-definition.xml` 文件，它不仅描述了元数据（如名称和描述），还包含了所需的软件 `PhoronixTestSuite.TestProfile.External Dependencies`、运行实际基准测试所需的外部依赖 `PhoronixTestSuite.TestInformation.Executable`，以及关于结果指标的数据。`PhoronixTestSuite.Information.ResultScale` 属性是指标的标签，例如“seconds”或“MB/s”。`PhoronixTestSuite.TestInformation.Property` 配置设置指标是报告为“HIB”还是“LIB”。

由于 `test-definition.xml` 文件的复杂性，作者建议直接从任何现有的测试配置复制，然后根据需要更新或添加字段。列表 5.4 展示了一个简单的测试定义。

```xml
<xml version="1.0"
<!--Phoronix Test Suite v4.4.0ml (Forsand)-->
<PhoronixTestSuite>
  <TestInformation>
    <Title>System X Decompression</Title>
    <Description>This measures the time to decompress a Linux kernel tarball using XZ.</Description>
    <ResultScale>seconds</ResultScale>
    <Proportion>LIB</Proportion>
    <TimesToRun>3</TimesToRun>
  </TestInformation>
  <TestProfile>
    <Version>1.0.2</Version>
    <SupportedPlatforms>Linux, BSD</SupportedPlatforms>
    <SoftwareType>Utility</SoftwareType>
    <TestType>Processor</TestType>
    <Maintainer>Jim Kukanas</Maintainer>
  </TestProfile>
</PhoronixTestSuite>
```

## 列表 5.4

用于 `system-decompress-xz` 测试配置的 `test-definition.xml`。

## 第 5 章设计实验

如果测试配置取决于特定的系统配置，请创建一个 `support-check.sh` 脚本。该脚本会在测试安装之前运行，以确定测试是否适用于该系统。该脚本返回正值表示该测试不适用于当前的系统配置。列表 5.5 展示了一个简单的支持检查脚本。

```sh
#!/bin/sh
which xz
if [ $? -gt 0 ]; then
    echo "The system must provide xz for this test profile."
    echo "Some Linux distributions provided xz through the xz-utils package." > $TEST_CUSTOM_ERROR
fi
```

## 列表 5.5

用于 `system-decompress-xz` 测试配置的 `support-check.sh`。

接下来，如果测试需要任何外部依赖，将在 `downloads.xml` 中创建一个下载清单。此 XML 文件列出了每个所需文件的 URL、文件名、文件大小和 MD5 校验和。在安装时，这些文件将从 URL 获取，根据文件和 MD5 校验和进行验证，然后复制到 `$HOME/phoronix-test-suite/installed-tests/` 目录下。列表 5.6 展示了一个简单的下载清单。

```xml
<?xml version="1.0"?>
<!--Phoronix Test Suite v4.0.4ml (Forsand)-->
<PhoronixTestSuite>
  <Downloads>
    <Package>
      <URL>http://www.kernel.org/pub/linux/kernel/v3.x/linux-3.7.tar.xz</URL>
      <MD5>21223369682bc44bdcfe152109583</MD5>
      <Filesize>69736096</Filesize>
    </Package>
  </Downloads>
</PhoronixTestSuite>
```

## 列表 5.6

用于 `system-decompress-xz` 测试配置的 `downloads.xml`。

接下来，创建一个 `install.sh` 脚本，它将执行测试的实际安装。通常，此脚本负责生成运行实际基准测试的 shell 脚本，并将结果重定向到 Phorix 结果解析器。列表 5.7 展示了一个简单的安装脚本。注意第 6 行创建了可执行的基准测试脚本 `system-decompress-xz`。所有的测试输出都重定向到环境变量 `$LOG_FILE`。这非常重要，因为 `$LOG_FILE` 中的唯一输出将用于解析结果。此外，始终记住要赋予脚本可执行权限，如第 11 行所示。

```bash
#!/bin/bash
XZ='which xz'
echo $? ~ /install-exit-status

cat > system-decompress-xz << EOT
#!/bin/sh
$XZ -dk --stdout linux-3.7.tar.xz > /dev/null 2>&1
EOT

chmod +x system-decompress-xz
```

- 5.7
用于 `system-decompress-xz` 测试配置的 `install.sh`。

此外，如果测试配置中存在 `pre.sh`、`run.sh` 或 `post.sh`，这些脚本将分别在测试之前、期间和之后执行。最后，一步是定义 `results-definition.xml`。此 XML 文件解释了 Phoronix 应如何解析结果。

```xml
<?xml version="1.0"?>
<!--Phoronix Test Suite v4.4.0ml (Forsand)-->
<PhoronixTestSuite>
  <SystemMonitor>
    <Sensor>time</Sensor>
  </SystemMonitor>
</PhoronixTestSuite>
```

- 5.8
用于 `system-decompress-xz` 测试配置的 `results-definition.xml`。

## 5.4 Phoronic Test Suite 97

