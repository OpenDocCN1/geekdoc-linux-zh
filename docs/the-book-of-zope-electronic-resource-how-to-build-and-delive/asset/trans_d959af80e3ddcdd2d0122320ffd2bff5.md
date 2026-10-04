

# 列表 15.3：Website 类的类声明

```
class Website(Folder):
    """此产品由 Katrin Kirchner 创建"""
    name='Website'
    id='Website'
    type='Website'
```

一旦你命名了该类，就应该包含一个文档字符串（doc string）来描述它。如列表 15.3 所示，使用三引号字符串的标准做法，这样文档字符串在需要时可以跨多行。

## 15.4.2.4 name, id, icon, meta_type

现在，我们需要添加与类相关的某些信息，包括 name、id 和 meta_type。`name` 和 `id` 项表示产品的名称和标识符。使用 `meta_type` 来指定你的产品和类（一个产品中可能包含多个类）在文件夹的添加菜单中显示方式。Metatypes 对于 Zope 中的每个对象类来说都是唯一的：如果另一个产品的类使用了相同的 metatype，则在加载产品时会发生错误。

## 15.4.2.5 定义安全信息

为了能够正确保护对 Website 方法的访问，我们需要创建一个 `ClassSecurityInfo` 对象。我们可以使用此对象为我们的类及其方法做出适当的安全断言，以防止未经授权的访问。在 Website 类中，我们使用以下代码创建一个存储在属性 "security" 中的 `ClassSecurityInfo` 对象：

```
security = ClassSecurityInfo()
```

我们之前已在模块的代码中从 `AccessControl` 导入了 `ClassSecurityInfo` 类（见第 15.4.2.1 节）。

> 这种断言机制最早出现在 Zope 2.3 中。在此之前，安全断言是通过在你的类上设置名为 `__ac_permissions__` 的属性来实现的。如果你阅读他人开发的产品代码，可能会使用这种访问控制方法。虽然 `__ac_permissions__` 仍然受支持，但它已被废弃，改为使用 `ClassSecurityInfo`。

接下来，我们将使用安全设置进行类范围的安全断言。`ClassSecurityInfo` 的 `declareObject` 方法用于声明用户访问由该类创建的对象时所需的权限。我们使用以下代码要求用户必须具有 `View` 权限才能访问 Website 实例：

```
security.declareObjectProtected('View')
```

我们可以对整个整体对象进行三种安全断言，如下表所示：

| ClassSecurityInfo 方法 | 说明 |
| :--- | :--- |
| declareObjectPublic | 这是默认的安全设置，无论用户的权限如何都允许访问该对象。此断言仅适用于对象本身，子对象和方法默认仍处于激活状态（详情请见第 1.5.4.1 节）。 |
| declareObjectPrivate | 限制从浏览器以及通过 HTML 或 Python 脚本等 Web 端代码对对象的访问。对于仅在产品内部使用且不应从 Web 访问的类，使用此设置。 |
| declareObjectProtected(permissionName) | 限制只有指定权限的用户可以访问对象。使用此设置允许 Zope 管理员通过安全管理标签页控制对对象的访问。 |

## 15.4.2 声明属性

接下来定义产品的属性，这些属性被用于类的每个实例。在这种情况下，我们只需要 `title` 属性，它可以被用于标记实例。

> 注意：将 `title` 定义为属性允许用户通过 Zope 管理界面对其进行修改。如果你点击实例中的属性标签页，将看到为每个实例定义的属性。

`properties` 变量是一个元组，如下文所示。元组的每个元素都是描述单个属性的字典。

```
properties =
  id: title, type: string, mode: 'w',
```

单独的键值对代表以下内容：

| 键名 | 值描述 |
| :--- | :--- |
| id | 这是属性的名称。每个属性名称必须是唯一的。 |
| type | 属性的类型。 |
| mode | 属性的模式，决定了是否可写（'w' 表示可写）。 |

