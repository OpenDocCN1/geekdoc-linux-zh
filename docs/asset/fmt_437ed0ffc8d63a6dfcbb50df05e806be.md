
```python
import Globals

from Globals import MessageDialog, DTMLE

from AccessControl import ClassSecurityInfo

from AccessControl.Permission import Permission

from AccessControl.User import UserFolder

from OFS.Folder import Folder

import StringIO
```

下面是对所导入模块的描述：

- `DTMLE` 类允许我们从文件中存储的 DTML 创建 DTML 方法对象。
- `Permission` 类为名为 `"WebsiteUser"` 的新角色分配必要的权限。
- `MessageDialog` 在 Zope 中向用户生成消息。
- `AccessControl` 是 `lib/python` 目录下的一个文件夹，其中包含几个模块（如 `Permission.py`、`Role.py`、`User.py`）。这些模块反过来包含方法（用于创建和编辑用户文件夹、角色、权限等），用以管理 Zope 中的安全性。
- `FS` 是 `lib/python` 目录下的另一个文件夹。它包含了定义了大多数标准 Zope 对象的模块，例如文件夹、DTML 方法和图像。
- `StringIO` 模块是一个标准的 Python 模块，允许你像处理文件一样处理文本字符串。它稍后将在一个名为 `addDocsToFolder` 的方法中使用，该方法会在 Zope 中创建 DTML 方法。

### 15.4.2.2 工具函数

示例产品还需要以下实用函数：

- `GetDTML(name)`
- `addDocsToFolder(theFolder, theDocs)`

`GetDTML(name)` 方法是方法 `"DTMLFile(name, globals())"` 的简化。它避免了你反复编写 `globals()`。该方法的代码如下：

```python
def getDTML(name):
    return DTMLFile(name, globals())
```

`addDocsToFolder(theFolder, theDocs)` 方法将产品目录中的 `.dtml` 文件作为 DTML 方法添加到由参数指定的 Zope 文件夹中。在我们的示例中，`theFolder` 代表产品的一个新实例。当创建实例时，DTML 方法会被添加到存储在 Website 产品子目录中的相应 `.dtml` 文件中。然后，这些 DTML 方法可以在 Zope 中进行自定义定制，以满足特定网站实例的需求。

`addDocsToFolder` 的代码显示在列表 15.1 中。

#### 列表 15.1：addDocsToFolder() 方法

```python
def addDocsToFolder(theFolder, theDocs):
    """
    # 在 Zope 中添加多个 DTML 方法
    """
    errs_String = String(IO)
    for key in theDocs.keys():
        id = key
        dtml.title = theDocs[key]
        try:
            dtml = open(dtml.raw).read()
        except:
            raise RuntimeError("Can't find " + dtml.raw)
        try:
            theFolder.manage_addDTMLMethod(id, title, file=thedtml)
        except:
            traceback.print_exc(file=errs)
    errs.seek(0)
    return errs.read()
```

该方法需要的参数是一个文件夹对象和一个字典（`thedocs`），该字典列出了要创建的各个 `.dtml` 文档。（参见表 15-2 获取示例产品所需的 `.dtml` 文件的列表和描述。）字典必须在随后定义的产品类之外创建（在 15.4.2.3 节）。

### 15.4.2.3 类定义

类是创建对象（实例）的模板。我们使用类来定义实例的所有属性，这些属性可能包含变量数据（如字符串、列表和字典）或其他对象（如 DTML 对象），或者定义作用于实例的方法。

`Website` 类的主要元素如下：

- 将类定义为文件夹对象，指定 `Folder` 为基类。
- 定义所有实例的属性（通过管理界面中的 Properties 选项卡访问），允许管理员对实例进行某些更改。（在案例中，只有 `title` 属性是通用的。）
- 定义每个产品实例管理界面标签栏中的新选项卡。这些新选项卡可以添加到现有选项卡中，也可以单独出现。
- 分配与产品特定实例方法相关的权限（通过管理界面中的 Security 选项卡访问）。这些扩展了实例相对于其他对象的安全性模型。
- 定义登录到产品实例的身份验证用户可用的方法，包括创建、编辑和删除用户的方法。

### 列表 15.3：Website 类的类声明

```python
class Website(Folder):
    """此产品由 Katrin Kirchner 创建"""
    name = 'Website'
    id = 'Website'
    type = 'Website'
```

一旦你命名了该类，就应该包含一个文档字符串（doc string）来描述它。如列表 15.3 所示，使用三引号字符串的标准做法，这样文档字符串在需要时可以跨多行。

## 15.4.2.4 name、id、icon、meta_type

现在，我们需要添加与类相关的某些信息，包括 `name`、`id` 和 `meta_type`。`name` 和 `id` 项表示产品的名称和标识符。使用 `meta_type` 来指定你的产品和类（一个产品中可能包含多个类）在文件夹的添加菜单中显示方式。Metatypes 对于 Zope 中的每个对象类来说都是唯一的：如果另一个产品的类使用了相同的 metatype，则在加载产品时会发生错误。

## 15.4.2.5 定义安全信息

为了能够正确保护对 `Website` 方法的访问，我们需要创建一个 `ClassSecurityInfo` 对象。我们可以使用此对象为我们的类及其方法做出适当的安全断言，以防止未经授权的访问。在 `Website` 类中，我们使用以下代码创建一个存储在属性 `"security"` 中的 `ClassSecurityInfo` 对象：

```python
security = ClassSecurityInfo()
```

我们之前已在模块的代码中从 `AccessControl` 导入了 `ClassSecurityInfo` 类（见第 15.4.2.1 节）。

> 这种断言机制最早出现在 Zope 2.3 中。在此之前，安全断言是通过在你的类上设置名为 `__ac_permissions__` 的属性来实现的。如果你阅读他人开发的产品代码，可能会使用这种访问控制方法。虽然 `__ac_permissions__` 仍然受支持，但它已被废弃，改为使用 `ClassSecurityInfo`。

接下来，我们将使用安全设置进行类范围的安全断言。`ClassSecurityInfo` 的 `declareObject` 方法用于声明用户访问由该类创建的对象时所需的权限。我们使用以下代码要求用户必须具有 `View` 权限才能访问 `Website` 实例：

```python
security.declareObjectProtected('View')
```

我们可以对整体对象进行三种安全断言，如下表所示：

| `ClassSecurityInfo` 方法 | 说明 |
| :--- | :--- |
| `declareObjectPublic` | 这是默认的安全设置，无论用户的权限如何都允许访问该对象。此断言仅适用于对象本身，子对象和方法默认仍处于激活状态（详情请见第 1.5.4.1 节）。 |
| `declareObjectPrivate` | 限制从浏览器以及通过 HTML 或 Python 脚本等 Web 端代码对对象的访问。对于仅在产品内部使用且不应从 Web 访问的类，使用此设置。 |
| `declareObjectProtected(permissionName)` | 限制只有指定权限的用户可以访问对象。使用此设置允许 Zope 管理员通过安全管理标签页控制对对象的访问。 |

## 15.4.2.6 声明属性

接下来定义产品的属性，这些属性被用于类的每个实例。在这种情况下，我们只需要 `title` 属性，它可以被用于标记实例。

> 注意：将 `title` 定义为属性允许用户通过 Zope 管理界面对其进行修改。如果你点击实例中的属性标签页，将看到为每个实例定义的属性。

`properties` 变量是一个元组，如下文所示。元组的每个元素都是描述单个属性的字典。

```python
properties =
```
