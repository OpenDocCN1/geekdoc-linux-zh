
# Notes:
# 1.      You can add comments after the pound sign (#) anywhere on a line.
# 2.      Rules are matched in descending order: first rule through the last rule.
# 3.      Rules can be continued to a new line by using the backslash (\\) before
#         the carriage return.
# 4.      Don't use the "*" character or other shell wildcards, because the rules
#         file is interpreted by a Bourne shell script.
#
################################################################################
#
# RULE_KEYWORD AND RULE_VALUE DESCRIPTIONS
#
#
#       rule_keyword  rule_value Type    rule_value Description
# ---------------  ----------  ----    -----------------------
#       any      minus sign (-) always matches
#       arch    text    system's architecture type
#       domainname    text    system's domain name
#       disksize  text range    system's disk size
#               disk device name (text)
#               disk size (MBytes range)
#       hostname  text    system's host name
#       installed text text    system's installed version of Solaris
#               disk device name (text)
#               OS release (text)
#       karch text    system's kernel architecture
#       memsize   range    system's memory size (MBytes range)
#       model text    system's model number
#       network   text    system's IP address
#       totaldisk range    system's total disk size (MBytes range)
#
#
################################################################################
#
# RULE EXAMPLES
#
# The following rule matches only one system:
#
#hostname sample_host     -     host_class     set_root_pw
#
# The following rule matches any system that is on the 924.222.43.0 network
# and has the sun4u kernel architecture:
#     Note: The backslash (\\) is used to continue the rule to a new line.
#
#network 924.222.43.0 && \
#        karch sun4c     -     net924_sun4u     -
#
# The following rule matches any sparc system with a c0t3d0 disk that is
# between 400 to 600 MBytes and has Solaris 2.1 installed on it:
#
#arch sparc && \
#        disksize c0t3d0 400-600 && \
#        installed c0t3d0s0 solaris_2.1 - upgrade  -

```
#
# The following rule matches all x86 systems:
#arch i386   x86-begin   x86-class   -
#
# The following rule matches any system:
#any -   -   any_machine   -
#
# END RULE EXAMPLES
#
#
karch sun4u   -      basic_prof   .
```

表 21.2 描述了规则文件必须遵循的语法。

## 表 21.2

### 规则语法

| 字段 | 描述 |

|---|---|

| ! | 在规则关键字前使用此项以表示否定。 |

| [ ] | 用于表示可选表达式或字段。 |

| ... | 用于表示前面的表达式可能重复。 |

| rule_keyword | 预定义的关键字，用于描述一般的系统属性，例如主机名（hostname）或内存大小（memsize）。它与 rule_value 一起使用，将具有相同属性的系统与配置文件匹配。rule_keywords 的完整列表在表 21.3 中描述。 |

| rule_value | 为相应的 rule_keyword 提供特定的系统属性值。rule_values 的列表请参见表 21.3。 |

| && | 用于在同一规则中连接规则关键字和规则值对（逻辑 AND）。在自定义 JumpStart 安装期间，系统必须与规则中的每一对匹配，规则才匹配。 |

| <begin> | 可选的 Bourne shell 脚本的名称，可在安装开始前执行。如果不存在 begin 脚本，则必须在此字段中输入连字符（-）。所有 begin 脚本必须位于 JumpStart 目录中。有关更多信息，请参阅“Begin and Finish Scripts”部分。 |

| 字段 | 描述 |

|---|---|

| `<profile>` | 类文件的名称，一个文本文件，用于定义如果系统匹配规则，则 Solaris 软件如何在系统上安装。类文件中的信息由类文件关键字及其对应的类文件值组成。所有类文件必须位于 JumpStart 目录中。类文件在“创建类文件”一节中进行了描述。 |

| `<finish>` | 可在安装完成后执行的可选 Bourne shell 脚本的名称。如果不存在 finish 脚本，则必须在此字段中输入减号 (-) 。所有 finish 脚本必须位于 JumpStart 目录中。有关更多信息，请参阅“开始和结束脚本”一节。 |

规则文件必须具有以下内容：

-   至少一条规则

-   名称为“rules”

-   至少一个规则关键字、一个规则值和一个对应的配置文件

-   如果没有条目，则在 begin 和 finish 字段中使用减号 (-)

规则文件应保存在 JumpStart 目录中，应由 root 所有，并且权限应等于 644。

规则文件允许以下内容：

-   行中任何位置 # 符号后的注释。如果一行以 # 开头，则整行都是注释。如果在行中间指定了 #，则 # 之后的所有内容都视为注释。

-   空行。

-   规则可跨多行。您可以让规则换行到新行，或在按下 Enter 之前使用反斜杠 (\ ) 在新行上继续规则。

表 21.3 描述了前面介绍的各种 rule_keywords 和 rule_values。

## 表 21.3

### 规则关键字和规则值描述

| 规则关键字 | 规则值 | 描述 |

|---|---|---|

| any | Minus sign (-) | 匹配始终成功。 |

| arch | processor_type | 下表列出了 processor_type 的有效值： |

| Platform SPARC x86 | processor_type sparc i386 | 匹配系统的处理器类型。uname -p 命令报告系统的处理器类型。 |

| domainname | domain_name | 匹配系统的域名，该域名控制名称服务如何确定信息。如果您已安装系统，则 domainname 命令会报告系统的域名。 |
