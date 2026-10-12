
机器和人类。SCAP（安全内容自动化协议）是一个多用途的规范框架，支持自动化配置、漏洞和补丁检查、技术控制合规活动以及安全度量。

换句话说，SCAP 是一种厂商中立的安全策略表达方式，因此被现代企业广泛使用。SCAP 规范创建了一个生态系统，在该系统中，安全内容的格式是众所周知且标准化的，而扫描器或策略编辑器的实现方式并未被强制规定。这种状态使得组织可以只构建一次其安全策略（SCAP 内容），无论他们使用多少个安全供应商。

最新版本的 SCAP 包含几个底层标准。这些组件根据其在 SCAP 中的功能划分为以下组：

## SCAP 组件

- **语言** – 该组包含定义标准词汇和约定以表达合规策略的 SCAP 语言。
    - *可扩展配置检查清单描述格式*（XCCDF） – 一种设计用于表达、组织和管理安全指南的语言。
    - *开放漏洞和评估语言*（OVAL） – 一种开发用于对扫描系统状态进行逻辑断言的语言。
    - *开放检查清单交互语言*（OCIL） – 一种设计用于提供向用户查询并解释用户对给定问题响应之标准方式的语言。
    - *资产标识*（AI） – 一种开发用于提供数据模型、方法和指南以识别安全资产的语言。
    - *资产报告格式*（ARF） – 一种设计用于表达收集的安全资产信息的传输格式以及资产与安全报告之间关系的语言。
- **枚举** – 该组包括定义命名格式以及来自某些感兴趣的安全领域的项目的官方列表或词典的 SCAP 标准。
    - *常见配置枚举*（CCE） – 应用程序和操作系统中与安全性相关的配置元素的枚举。
    - *常见平台枚举*（CPE） – 用于识别信息技术（IT）系统、平台和软件包的结构化命名方案。
    - *常见漏洞与暴露*（CVE） – 公开已知的软件漏洞和暴露的参考方法。
- **度量** – 该组由用于识别和评估安全风险的框架组成。
    - *常见配置评分系统*（CCSS） – 一种用于评估与安全性相关的配置元素并为其分配分数，以帮助用户确定适当的响应步骤优先级的度量系统。
    - *常见漏洞评分系统*（CVSS） – 一种用于评估软件漏洞并为其分配分数，以帮助用户确定其安全风险优先级的度量系统。
- **完整性** – 一个用于维护 SCAP 内容和扫描结果完整性的 SCAP 规范。
    - *安全自动化数据信任模型*（TMSAD） – 一组解释如何使用现有规范在安全自动化域内的 XML 文件上下文中表示签名、哈希、密钥信息和身份信息的建议。

每个 SCAP 组件都有自己基于 XML 的文档格式及其 XML 命名空间。以 SCAP 表达的一致性策略可以采取单个 OVAL 定义 XML 文件、数据流文件、单个 zip 归档或包含代表策略检查清单的 XCCDF 文件的独立 XML 文件集的形式。

### 7.2.1. XCCDF 文件格式

XCCDF 语言旨在支持信息交换、文档生成、组织和情境定制、自动化合规测试以及合规评分。该语言主要是描述性的，不包含执行安全扫描的任何命令。然而，XCCDF 文档可以引用其他 SCAP 组件，因此可用于制定在所有目标平台间可移植的合规策略，但相关的评估文档（OVAL, OCL）除外。

表示合规策略的常见方式是一组 XML 文件，其中一个文件是 XCCDF 检查清单。这个 XCCDF 文件通常指向评估资源，多个 OVAL、OCL 和脚本检查引擎（SCE）文件。此外，文件集可以包含一个 CPE 字典文件和一个定义该字典对象的 OVAL 文件。

作为一种基于 XML 的语言，XCCDF 定义并使用了大量的 XML 元素和属性。以下列表简要介绍了主要的 XCCDF 元素；有关 XCCDF 的更多详细信息，请查阅 NIST 机构间报告 7275 第 4 版。

**XCCDF 文档的主要 XML 元素**

- `<xccdf:Benchmark>` – 这是根元素，包裹整个 XCCDF 文档。它还可能包含检查清单元数据，如标题、描述、作者列表、最近修改日期以及检查清单接受状态。
- `<xccdf:Rule>` – 这是一个关键元素，代表检查清单要求并持有其描述。它可能包含定义验证或强制执行对给定规则合规性的操作或修改规则本身的子元素。
- `<xccdf:Value>` – 这个关键元素用于表达基准中其他 XCCDF 元素的属性。
- `<xccdf:Group>` – 此元素用于通过收集 `<xccdf:Rule>`、`<xccdf:Value>` 和 `<xccdf:Group>` 元素，将 XCCDF 文档组织为具有相同上下文或要求域的结构。
- `<xccdf:Profile>` – 此元素用于 XCCDF 基准的命名定制。它允许基准持有多个不同的定制。`<xccdf:Profile>` 利用多个选择器元素，例如 `<xccdf:select>` 或 `<xccdf:refine-rule>`，以确定在生效时哪些元素将被修改和处理。
- `<xccdf:Tailoring>` – 此元素允许在基准外部定义基准配置文件，这对于合规策略的手动定制有时是期望的。
- `<xccdf:TestResult>` – 此元素用于保存目标系统上给定基准的扫描结果。每个 `<xccdf:TestResult>` 应引用用于定义特定扫描的合规策略的配置档案，并且还应包含与扫描相关的目标系统的重要信息。
- `<xccdf:rule-result>` – 这是 `<xccdf:TestResult>` 的子元素，用于保存针对目标系统应用基准中特定规则的结果。
- `<xccdf:fix>` – 这是 `<xccdf:Rule>` 的子元素，用于修复不符合给定规则的目标系统。它可以包含在目标系统上运行的命令或脚本，以使系统符合该规则。
- `<xccdf:check>` – 这是 `<xccdf:Rule>` 的子元素，引用定义如何评估给定规则的外部来源。
- `<xccdf:select>` – 这是一个选择器元素，用于从策略中包含或排除选定的规则或规则组。
- `<xccdf:set-value>` – 这是一个选择器元素，用于覆盖指定的 `<xccdf:Value>` 元素的当前值，而不修改其其他属性。
- `<xccdf:refine-value>` – 这是一个选择器元素，用于在策略定制期间指定特定 `<xccdf:Value>` 元素的约束。
- `<xccdf:refine-rule>` – 此选择器元素允许覆盖选定规则的属性。

**示例 7.1. XCCDF 文档示例**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Benchmark xmlns="http://checklists.nist.gov/xccdf/1.2"
           id="xccdf_com.example.www_benchmark_test">
    <status>incomplete</status>
    <version>0.1</version>
    <Profile id="xccdf_com.example.www_profile_1">
        <title>Profile title is compulsory</title>
        <select idref="xccdf_com.example.www_group_1"
                selected="true"/>
        <select idref="xccdf_com.example.www_rule_1"
                selected="true"/>
        <refine-value idref="xccdf_com.example.www_value_1"
                      selector="telnet service"/>
    </Profile>
    <Group id="xccdf_com.example.www_group_1">
        <Value id="xccdf_com.example.www_value_1">
            <value selector="telnet_service">telnet-server</value>
            <value selector="dhcp_service">dhcpd</value>
            <value selector="ftpd_service">tftpd</value>
        </Value>
        <Rule id="xccdf_com.example.www_rule_1">
            <title>The telnet-server Package Shall Not Be Installed</title>
            <rationale>
                Removing the telnet-server package decreases the risk
                of the telnet service's accidental (or intentional) activation
            </rationale>
            <fix platform="cpe:/o:redhat:enterprise_linux:6"
                 reboot="false"
                 disruption="low"
```
