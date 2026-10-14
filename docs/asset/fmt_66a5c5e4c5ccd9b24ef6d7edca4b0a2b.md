
在此示例中，证书映射的名称为 `Example CA`，它映射到发行者的区分名称 `ou=Example CA, o=Example, c=US`。

> 注意：请注意映射属性的其余行是如何以证书映射名称（`Example CA`）开头的。Web 服务器正是通过此知道这些属性适用于该映射。

`CmapLdapAttr` 属性告诉服务器在整个目录中搜索 `certSubjectDN` 与客户端证书列出的主体完整 DN 匹配的条目。如果搜索没有任何条目，服务器将使用 `DNComps` 和 `FilterComps` 映射重试搜索。

`DNComps` 属性表示搜索的基区分名称（baseDN）应该根据从客户端证书中提取的组织（organization）和国家（country）属性来创建。

`FilterComps` 属性表示 Web 服务器应该搜索与从客户端证书中提取的电子邮件（e-mail）和用户 ID（user ID）属性匹配的条目。

`VerifyCert` 属性告诉服务器是否将客户端证书与用户目录条目中的证书进行比较。值 `on` 确保除非呈现证书与存储在目录中的证书完全匹配，否则服务器不会对客户端进行身份验证。

### 5.7.3 上文

每个服务器实例都有自己的证书映射配置文件；因此，服务器实例与此文件之间是一一对应的关系。

### 5.7.4 修改

管理控制台和命令行界面未提供管理证书映射文件的方法。因此，必须在特定的管理节点直接向 `certmap.conf` 文件添加条目。执行此操作后，必须将更改推回配置并根据情况推送到额外的管理节点。

## 5.8 default.acl 文件

你可以控制对整个 Web 服务器或服务器部分（例如目录、文件和文件类型）的访问。当 Web 服务器评估传入的请求时，它根据允许访问控制条目（ACEs）的分级规则来决定访问权限。Web 服务器使用匹配的条目来确定客户端请求是被允许还是拒绝。

ACE 集合被称为访问控制列表（ACL）。Web 服务器从上到下处理 ACL 列表。如果在任何时候 ACE 的评估值为 `false`，ACL 的处理将停止，用户被拒绝访问资源。

ACL 文件包含定义谁可以访问存储在 Web 服务器上的资源的规则。默认情况下，Web 服务器使用一个包含默认访问列表 `default.acl`。你可以通过编辑此文件或为一个或多个实例创建额外的 ACL 文件来更改访问控制规则。如果你创建了额外的 ACL 文件，可以使用 `server.xml` 中的 `<acl-file>` 元素将其与不同的虚拟服务器关联。

示例 5.9 展示了如何使用 `<acl-file>` 元素为特定服务器指定 ACL 文件：

示例 5.9 ACL 文件的虚拟服务器定义

```
<virtual-server>
<name>www.example.com</name>
<http-listener-name-http-listener-1</listener-name>
<host>www.example.com</host>
<object-file>www.example.com-obj.conf</object-file>
<mime-file>mime.types</mime-file>
<acl-file>example.acl</acl-file>
</virtual-server>
```

## 5.8 DEFAULT.ACL 文件

```
<document-root>/export/home/example.com/public_html</document-root>
<access-log>
<file>/export/home/example.com/logs/access</file>
</access-log>
</virtual-server>
```

为每个虚拟服务器关联不同的 ACL 文件，可以让你在虚拟服务器级别提供不同访问控制的活性。

### 5.8.1 文件结构

ACL 文件是一个包含一个或多个 ACL 的文本文件。示例 5.10 展示了默认管理节点的访问控制列表文件。

示例 5.10 `default.acl` 文件

```
# Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# Use is subject to terms.
version 3.0;
acl "default" {
  allow (read, info) user = "everyone";
  allow (list, write) user = "admin";
  deny (all) user = "guest";
}
acl "/public_html/private/*" {
  allow (read, info) user = "authorized_user";
  allow (list, write) user = "admin";
  deny (all) user = "guest";
}
```

### 5.8.2 语法

输入字符串可以包含以下字符：

- 字母 a 到 z 以及数字 0 到 9
- 点 (`.`) 或下划线 (`_`)

如果你使用任何其他字符，请在其周围加上双引号。单个语句可以单独占一行，并以分号结束。多个语句放在大括号内。项目列表必须用逗号隔开，并用双引号括起来。

### 5.8.3 身份验证方法

ACL 可以可选地指定服务器在处理 ACL 时必须使用的身份验证方法。共有三种方法：

- `basic`
- `digest`
- `ssl`

`basic` 和 `digest` 方法都需要用户在访问资源之前输入用户名和密码。然而，两者的区别在于客户端与 Web 服务器之间传输数据的方式，以及在身份数据库中验证密码的方式。

`basic` 身份验证方法允许用户输入用户名和密码，并将信息以知的 Base64 编码传输到 Web 服务器。出于安全考虑，`basic` 几乎总是与 SSL 连接一起使用，用户名和密码在从客户端发送之前会被加密。

`digest` 身份验证方法防止客户端的用户名和密码以明文发送。浏览器使用 MD5 算法通过密码和 Web 服务器发送的信息创建消息摘要。摘要值在服务器端使用 Digest 身份验证插件进行计算和比较。

`ssl` 方法要求用户拥有客户端证书。Web 服务器必须开启加密，并且用户的证书颁发机构必须在受信任证书颁发机构（CA）列表中。有关使用客户端证书进行身份验证的更多信息，请参见第 5.7 节“`certmap.conf` 文件”。

# 第 5 章 Web 服务器 7.0 配置文件

默认情况下，对于任何未显式指定方法的 ACL，服务器都使用基础方法（`basic`）。如果你使用摘要方法（`digest`），服务器的身份验证数据库必须能够处理摘要认证。身份验证数据库在 `server.xml` 中通过 `<auth-db>` 元素配置。有关配置身份验证数据库的更多信息，请参阅第 8 章。

每一行身份验证内容必须指定属性（用户、组或同时包含用户和组）。以下位于 ACL 类型行之后的身份验证语句指定了基础认证，并将用户与数据库或目录中的单个用户匹配：

```
authenticate (user) { method = "basic";
```

以下示例使用 `ssl` 作为用户和组的认证方法：

```
authenticate (user, group) { method = "ssl";
```

以下示例允许任何以 `sales` 开头的用户：

```
authenticate (user)
allow (all)
  user = sales*
```

如果将最后一行改为 `group = sales`，则 ACL 将失败，因为组属性未经过身份验证。

## 5.8.2.3 授权语句

每个 ACL 条目可以包含一个或多个授权语句。授权语句指定了谁允许或拒绝访问服务器资源。使用以下语法编写授权语句：

```
allow|deny [absolute] (right[,right..]) attribute expression;
```

每条语句都以 `allow` 或 `deny` 开头。由于层级规则，通常的做法是在第一条规则中拒绝所有人的访问，并在后续规则中专门允许用户、组或计算机的访问。也就是说，如果你允许访问名为 `/my_stuff` 的目录，并且你有一个允许少数用户访问的子目录 `/my_stuff/personal`，那么该子目录的访问控制将不起作用，因为任何被允许访问 `/my_stuff` 目录的人也被允许访问 `/my_stuff/personal` 目录。为了防止

## 5.8 DEFAULT.ACL 文件

出现这种情况，请为子目录创建一个规则，首先拒绝任何访问，然后允许需要访问的少数用户访问。

在某些情况下，如果你将默认 ACL 设置为拒绝所有人访问，则你的其他 ACL 规则就不需要 `deny all` 规则。

以下行拒绝了所有人的访问：

```
deny (all) user = "anyone";
```
