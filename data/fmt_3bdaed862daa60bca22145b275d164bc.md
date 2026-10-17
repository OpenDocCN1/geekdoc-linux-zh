
```html
<!DOCTYPE HTML>
<html lang="en">
<head> <meta charset="UTF-8">
<title>Selection List Example</title> </head>
<body>
<form method="POST" action="selection.py">
<select name="CityList">
<option value="New York">New York</option>
<option value="London">London</option>
<option value="Paris">Paris</option>
<option value="Beijing">Beijing</option>
</select>
<input type="submit" value="Submit" >
</form>
</body>
</html>
```

![](img/d06b1f1cf83677f0c7827141_224_1.png)

- 2. 接下来，通过使 CGI 处理功能可用，开始编写一个新的 Python 脚本，并创建一个 `FieldStorage` 数据对象

```python
import cgi
data = cgi.FieldStorage()
```

- 3. 现在，将选中的选项值分配给一个变量

`city = data.getvalue( 'CityList' )`

- 4. 然后，添加语句以输出包含已提交选项值的完整 HTML 网页

```python
print( `Content-type:text/html\r\n\r\n` )
print( `<!DOCTYPE HTML>` )
print( `<html lang="en">` )
print( `<head> <meta charset="UTF-8">` )
print( `<title>Python Response</title> </head>` )
print( `<body>` )
print( `<h1>City:`, city, `</h1>` )
print( `<a href="selection.html">Back</a>` )
print( `</body>` )
print( `</html>` )
```

- 5. 最后，将两个文件保存在 Web 服务器的 `/htdocs` 目录中，在浏览器中加载 HTML 文档，然后按下提交按钮——以查看响应中的选中值

![](img/d06b1f1cf83677f0c7827141_225_0.png)

![](img/d06b1f1cf83677f0c7827141_226_0.png)

![](img/d06b1f1cf83677f0c7827141_226_1.png)

![](img/d06b1f1cf83677f0c7827141_226_2.png)

通常，除非你打开下拉列表并选择另一个选项，否则默认将选择第一个列表选项进行提交。

![](img/d06b1f1cf83677f0c7827141_226_3.png)

你可以在 `<option>` 标签中包含 `selected` 属性，以便在每个列表中自动选中一个选项——从而提供一个默认选项。

### 上传文件

HTML 表单可以提供一个文件选择功能，该功能调用操作系统的“选择文件”对话框，允许用户浏览其本地文件系统并选择一个文件。为了启用此功能，HTML `<form>` 标签必须包含一个 `enctype` 属性，指定编码类型为“`multipart/form-data`”。

所选上传文件的完整路径地址是存储在 `FieldStorage` 对象列表中的一个值，可以使用其关联的键名来访问。实用的是，可以通过“`os`”模块的 `path.basename()` 方法从路径地址中剥离出文件名。

可以通过读取 `FieldStorage` 对象的 `file` 属性，将上传文件的副本写入 Web 服务器。

![](img/d06b1f1cf83677f0c7827141_227_0.png)

- 1. 创建一个新的 HTML 文档，其中包含一个带有文件选择功能和提交按钮的表单

```html
<!DOCTYPE HTML>
<html lang="en">
<head> <meta charset="UTF-8">
<title>File Upload Example</title> </head>
<body>
<form method="POST" action="upload.py" enctype="multipart/form-data" >
<input type="file" name="filename" style="width:400px">
<input type="submit" value="Submit">
</form>
</body>
</html>
```

![](img/d06b1f1cf83677f0c7827141_227_1.png)

```
upload.py
```

- 2. 接下来，通过使 CGI 处理和操作系统功能可用，开始编写一个新的 Python 脚本，然后创建一个 `FieldStorage` 数据对象

```python
import cgi, os
data = cgi.FieldStorage()
```

- 3. 现在，将上传文件的完整路径分配给一个变量，将其剥离出的文件名分配给另一个变量

```python
upload = data[ 'filename' ]
filename = os.path.basename( upload.filename )
```

- 4. 然后，在 Web 服务器上写入上传文件的副本

```python
with open( filename, 'wb') as copy:
    copy.write( upload.file.read() )
```

- 5. 然后，添加语句以输出包含上传文件名的完整 HTML 网页

```python
print(‘Content-type:text/html\r\n\n’)`
print(‘<!DOCTYPE HTML>’)`
print(‘<html lang=\"en\">’)
print(‘<head>’)`
print(‘<meta charset=\"UTF-8\">’)`
print(‘<title>Python Response</title>’)`
print(‘</head>’)`
print(‘<body>’)`
print(‘<h1>File Uploaded:’, filename, ‘</h1>’)`
print(‘<a href=\"upload.html\">Back</a>’)`
print(‘</body>’)`
print(‘</html>’)`
```

- 6. 最后，将两个文件保存在 Web 服务器的 `/htdocs` 目录中，在浏览器中加载 HTML 文档，然后选择一个文件进行上传——以查看文件上传响应

![](img/d06b1f1cf83677f0c7827141_228_0.png)

![](img/d06b1f1cf83677f0c7827141_229_0.png)

(C:) » MyProjects »

![](img/d06b1f1cf83677f0c7827141_229_1.png)

Abyss Web Server » htdocs

![](img/d06b1f1cf83677f0c7827141_229_2.png)

![](img/d06b1f1cf83677f0c7827141_229_3.png)

请注意，这里使用二进制文件模式来复制上传的文件。

### 总结

- Python 可以安装在 Web 服务器主机上，以便在将响应发送到 Web 浏览器客户端之前处理脚本代码。
- 服务器端 Python 脚本可以通过将内容类型描述为 `Content-type:text/html\r\n\n` 来生成 HTML 文档。
- `cgitmodule` 提供一个 `FieldStorage()` 构造函数，用于创建一个对象，以键值对的形式存储提交的数据。
- `FieldStorage` 对象中存储的任何值都可以通过向该对象的 `getvalue()` 方法指定其键名来检索。
- 浏览器可以使用 `GET` 方法向脚本发送数据，该方法在 URL 地址后添加一个 `?` 标记后附加键值对。
- 如果每个键值对之间用 `&` 字符分隔，则可以使用 `GET` 方法提交多个键值对数据。
- `GET` 方法请求字符串长度不能超过 1024 个字符，并且将在浏览器地址栏中可见。
- 浏览器可以使用 `POST` 方法向脚本发送数据，该方法将键值对作为单独的消息提交。
- 从 HTML 表单提交的数据可以存储为键值对形式的 Field Storage 对象，对应于每个表单字段。
- 服务器端 Python 脚本可以为用户留空的提交 HTML 表单字段提供默认值。
- HTML 表单中未勾选的复选框字段不会提交给 Web 服务器。
