
`id`: `title`, `type`: `string`, `mode`: `'w'`,

单独的键值对代表以下内容：

| 键名 | 值描述 |
| :--- | :--- |
| id | 这是属性的名称。每个属性名称必须是唯一的。 |
| type | 属性的类型。 |
| mode | 属性的模式，决定了是否可写（`'w'` 表示可写）。 |

```python
else:
    self.acl_users._adduser(name, pwd, confirm, roles, domains, REQUEST)
    RESPONSE.redirect('index.html')
```

`addNewWebsiteUser()` 方法使用了 `user.py` 模块中的内置私有方法 `_addUser` 来创建一个新用户（更多信息请参阅第 8 章）。该方法的参数如表 15-3 所示。

### 表 15-3：创建新用户的数据

| 参数 | 说明 |
| --- | --- |
| self | 产品的实例 |
| name | 用户名 |
| pwd | 用户密码 |
| confirm | 确认密码 |
| roles | 用户的角色，格式为列表 |
| domains | 用户可以登录的互联网域名（格式为列表） |
| REQUEST | `REQUEST` 对象（由 Zope 提供） |
| RESPONSE | `RESPONSE` 对象（由 Zope 提供） |

`addNewWebsiteUser()` 方法的代码实现逻辑是：首先检查 `name` 是否已经存在于 `self` 所指向的文件夹的用户文件夹 (`ad_users`) 中。它通过使用 `getUser(name)` 方法来实现，如果该名称存在，则返回一个用户对象，否则返回 `None`。由于在 Python 中，所有用户对象的值都被视为真值，而 `None` 被视为假值，我们可以直接用 `if` 语句检查 `getUser(name)` 的结果来判断用户是否存在。

如果用户存在，我们将使用 `MessageDialog` 生成一个包含消息和 OK 按钮的 HTML 页面。点击 OK 将打开 `action` 参数指定的 URL。`title` 参数指定了应该出现在 HTML 页面 `<HEAD>` 元素中的内容，并用作页面的标题。

如果用户不存在，则会调用产品实例中用户文件夹的 `_addUser` 方法（这是一个内置私有方法），你可以通过它从 Python 直接在 Zope 中添加新用户。我们将所有关于要创建的用户的信息（用户名、密码等）传递给该方法。一旦完成，我们将重定向到 Web 实例的首页（`index.html`）。

`addNewWebsiteUser()` 方法现在结束。如果你已经创建了产品的实例，任何已经登录网站的用户都可以使用该方法来创建新用户。

> 仅凭此方法不足以允许访问者创建新用户。必须创建 DTML 方法来构建网站界面，并且如上述所示，还要创建用于验证用户的安全模型。

## 15.4.2.11 editWebsiteUser 方法

`editWebsiteUser` 方法（显示在列表 15-5 中）非常短，因为我们最初不需要检查要修改的用户是否已经存在于用户文件夹 `acl_users` 中。`editWebsiteUser()` 方法在 DTML 方法 `WebsiteUsers_List` 中被调用，该方法会生成用户文件夹中存在的用户列表。

### 列表 15-5：用于 Website 产品的 `editWebsiteUser()` 方法

```python
# 允许具有“Manage users”权限的用户访问此方法
security.declareProtected('Manage users', 'editWebsiteUser')

def editWebsiteUser(self, name, pwd, confirm, domains, roles, REQUEST, RESPONSE):
    # "更改现有的 WebsiteUser"
    self.acl_users.changeUser(name,pwd,confirm,domains)
    return MessageDialog(
        title='User changed',
        message='The user has been changed.',
        action='index.html'
    )
```

当用户在产品中查看用户列表时，用户名后面会出现“Edit（编辑）”和“Delete（删除）”链接。如果你点击 Edit，会出现一个表单允许你编辑该用户的详情。如果你点击编辑表单上的“Change User（更改用户）”按钮，就会调用此方法并更改数据。

`editWebsiteUser` 方法接收的参数与 `addNewWebsiteUser()` 相同。

用户文件夹有一个用于更改用户的 `changeUser()` 方法；该方法按如下方式与用户文件夹 `acl_users` 配合：

```python
self.acl_users.changeUser(name,pwd,confirm,roles,domains)
```

## 15.4.2.12 deleteWebsiteUser 方法

现在我们需要另一个方法来允许已认证的用户删除用户。如你所知，已认证的用户可以访问 `acl_users` 中的用户列表，通过点击链接，可以编辑或删除该用户。删除用户的链接会调用 `deleteWebsiteUser()` 方法（显示在列表 15.14 中），并将要删除的用户名作为字符串传递过去。当你点击 Delete 时，用户将立即被删除。

### 列表 15-6：用于 Website 产品的 `deleteWebsiteUser()` 方法

```python
# 允许具有“Manage users”权限的用户访问此方法
security.declareProtected('Manage users', 'deleteWebsiteUser')
```

```python
def deleteWebsiteUser(self, name):
    """Deletes a Website""
    self.acl_users.delUsers(name)
    return MessageDialog(
        title ='User deleted',
        message='The user has been deleted.',
        action='index.html'
    )
```

由于删除用户的方法 `delUsers()`（定义在 `User.py` 中）期望将用户名列表作为其参数，我们必须通过方括号将单个名称封装在列表中进行传递。尽管 `_delUsers()` 可以一次性删除多个用户，但我们在产品中没有使用这一功能。

```python
self.acl_users.delUsers(names)
```

## 15.4.2.13 初始化类

我们现在已经编写了整个 Website 类定义。为了让 Zope 正确识别我们的安全断言，我们必须在类定义之后添加一行调用 `Globals` 模块的 `InitializeClass` 函数，并将我们的类作为其参数传递进去：

```python
Globals.InitializeClass(Website)
```

## 15.4.3 定义构造表单

为了让用户创建 Website 类的实例，我们必须提供一个表单，允许他们为新实例指定必要的值，例如其 ID 和标题。为此，我们在 Website 产品中定义一个包含表单模板的 DTML 文件。然后，我们需要将此文件变成可以从 Zope 访问的 DTML 对象。

### 15.4.3.1 addWebsiteForm.dtml

与产品一起使用的 DTML 文件通常存储在产品主目录的 `dtml` 子目录下。以下是存储在 Website 产品 `dtml` 目录下的 `addWebsiteForm.dtml` 文件内容：

```html
<html-var standard_html_header>
<form action="manage_website" method=post>
<h2>Add a new Website</h2>
<p>The Website 是一个类似文件夹的对象，包含多个 DTML 方法以及一个包含已创建用户的 User Folder。</p>
<table>
<tr>
<th>Id:</th</th>
<td><input type="text" name=id size=20></td>
</tr>
<html><em>Title:</em></html>
<td><input type=text name=title size=20></td>
<tr>
<td></td>
<td><input type="submit value=Add></td>
</tr>
</table>
</form>
```
