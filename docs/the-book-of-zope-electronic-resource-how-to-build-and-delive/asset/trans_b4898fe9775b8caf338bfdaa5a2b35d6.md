

![](img/43a28cce5475b2f487bf455365567fb6_376_0.png)

# 网站产品的源代码

# C.1 网站产品 __init__.py 的源代码

```python
__version__='Version 0.1'
__doc__='Website'

import Website

def initialize(context):
    """注册 Website 类"""

    context.registerClass(
        Website.Website,
        constructors = (
            Website.manage_addWebsiteForm,
            Website.manage_addWebsite
        ),
        permission = 'Add Website',
        icon = 'www/icon.gif'
    )
```

# C.2 网站产品 Website.py 的源代码

```python
################################################################
## 导入必要的模块、类和方法 ##
################################################################

import Globals
from Globals import MessageDialog, DTMLFile
from AccessControl import ClassSecurityInfo
from AccessControl.Permission import Permission
from AccessControl.User import UserFolder
from OFS.Folder import Folder
import StringIO

################################################################
## 在 Zope 中创建 DTML 方法的辅助方法 ##
################################################################

def getDTML(name):
    return DTMLFile(name, globals())

def addDocsTo(folder, theDocs):
    """ 在 Zope 中添加多个 DTML 方法 """
    errs = StringIO.StringIO()
    for key in theDocs.keys():
        id = key
        dtml,title = theDocs[key]
        try:
            thedml = open(dtml.raw).read()
        except:
            raise RuntimeError("Can't find " + dtml.raw)
        try:
            folder.manager_addDocument(id, title=title, file=dtml)
        except:
            traceback.print_exc(file=errs)
        errs.seek(0)
    return errs.read(0)

################################################################
## 包含 .dtml 文件的字典，这些文件需要被
## 转换为 DTML 方法
################################################################

Website_pages={
    'standard_html_header':
    (GetDTML('/public/standard_html_header'),"网站标准头部"),
    'standard_html_footer':
    (GetDTML('public/standard_html_footer'), '网站标准页脚'),
    'index_html':
    (GetDTML('public/index_html'), '网站首页'),
    'login_html':
    (GetDTML('public/login_html'), '密码检查'),
    'new_WebsiteUser':
    (GetDTML('public/new_WebsiteUser'), '创建一个新的 WebsiteUser'),
    'WebsiteUsers_list':
    (GetDTML('public/WebsiteUsers_list'), 'WebsiteUsers 列表'),
    'edit_WebsiteUser':
    (GetDTML('public/edit_WebsiteUser'), '编辑 WebsiteUser'),
    'products_html':
    (GetDTML('public/products_html'), '关于我们的产品'),
    'about_us_html':
    (GetDTML('public/about_us_html'), '关于公司'),
}
```

```python
############################################################
## Website 产品的类定义
############################################################
```

```python
class Website(Folder):
    """此产品由 Katrin Kirchner 创建"""
    name='Website'
    id='Website'
    meta_type='Website'
```

```python
############################################################
## 为我们的类创建一个 ClassSecurityInfo 对象
## 这样我们就可以对类中定义的属性
## 进行安全断言
############################################################
```

```python
security = ClassSecurityInfo()
```

```python
############################################################
## 为类的实例设置默认安全设置
## 用户必须拥有“查看(View)”权限才能对
## Website 实例进行任何访问。
############################################################
```

```python
security.declareObjectProtected('View')
```

```python
## 定义类的默认属性 ##
```

```python
properties=(
    (id title type string mode=W),
)
```

```python
## 在产品实例的标签栏中添加自定义标签的
## 示例（使用 # 注释） ##
```

```python
manage_options=folder.manage_options(
    label='my_label', icon=icon, action=my_action, target='manage_main',
).
```

```python
## 创建新网站用户的方法 ##
```

```python
# 允许拥有“管理用户”权限的用户访问此方法
security.declareProtected('Manage users', addwebsiteuser)
```

```python
def addwebsiteuser(self, name, pwd, confirm, roles, domains, REQUEST, RESPONSE):
    """如果用户名不存在，则创建一个新的 websiteuser"""
    if self.acl_users.get(name):
        return MessageDialog(
            title='用户已存在',
            message='该名称已有一个用户。',
            action='new_websiteuser')
    else:
        self.acl_users.add(name, pwd, confirm, roles, domains, REQUEST)
        return RESPONSE.redirect('index.html')
```

```python
## 修改密码、
## 互联网域名以及现有
## websiteuser 角色的方法 ##
```

```python
# 允许拥有“管理用户”权限的用户访问此方法
security.declareProtected('Manage users', editwebsiteuser)
```

```python
def editwebsiteuser(self, name, pwd, confirm, domains, roles, REQUEST, RESPONSE):
    """修改现有的 websiteuser"""
    self.acl_users.change(name,pwd,confirm,roles,domains)
    return MessageDialog(
        title = '用户已修改',
        message='用户已更改。',
        action = 'index.html'
    )
```

```python
############################################################
## 删除现有 WebsiteUser 的方法 ##
###########################################################
```

```python
# 允许拥有“管理”权限的用户访问此方法
security.declareProtected('Manage users', 'deleteWebsiteUser')

def deleteWebsiteUser(self, name):
    """删除一个 WebsiteUser"""
    self.acl_users.delUsers([name])
    return MessageDialog(
        title = '用户已删除',
        message='用户已被删除。',
        action = 'index.html'
    )
```

```python
############################################################
## 在 Zope 中正确初始化该类
###########################################################
```

```python
Globals.InitializeClass(Website)
```

```python
################################################************
## 显示创建 Website 产品新
## 实例的表单
###########################################################
```

```python
manage_addWebsiteForm=DTMLFile('dtml/addWebsiteForm', globals)
```

```python
################################################************
## 创建 Website 产品实例的方法，
## 包括 DTML 方法和
## 用户文件夹 ##
###########################################################
```

```python
def manage_addWebsite(self, id, title, REQUEST=None):
    """添加一个新的 Website"""
    
    ########################################## 类到
    ## 将 Website 赋值给
    ## 变量Instance
    ########################################## ## 
    ##
    instance=Website()
    instance.id=id
    instance.title=title

    ########################################## ##
    ## 创建用户文件夹
    ########################################## ##
    ##
    user_folder=UserFolder()
    instance._setObject('acl_users', user_folder)

    ########################################## ##
    ## 创建角色 'WebsiteUser'
    ########################################## ##
    ##
    instance_addRole('WebsiteUser')

    ########################################## ##
    ## 为 'WebsiteUser' 角色设置权限
    ##########################################
    ##
    p_list = ['Access contents information',
    'Manage users', 'View']
    for permission in p_list:
        p=Permission(permission,,'instance')
        p.setRole('WebsiteUser', permission in p_list)

    ########################################## ##
    ## 在当前文件夹中创建
    ## 产品实例
    ##########################################
    ##
    self._setObject(id, instance)

    ########################################## ##
    ## 创建 DTML 方法
    ##########################################
    ##
    addDocsToFolder(instance, Website_pages)
```

