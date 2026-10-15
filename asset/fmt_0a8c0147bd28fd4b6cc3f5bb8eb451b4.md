
Option Explicit

## 第 39 章 使用 StarBasic 进行编程

```vbbasic
Dim oActiveWindow As Object
Dim oActiveDocument As Object
Sub ManualComplete
'该宏仅在文档之外无法运行，因此检查此处
If ActiveModule.Name <> "StarWriter" Then
MsgBox("此程序仅在文本文档可用。",16,"Error")
Exit Sub
End If
'保存两个 StarOffice 对象的引用，因为我们稍后需要它们
oActiveWindow = ActiveWindow
ActiveDocument = ActiveDocument
'调用将单词放入我们列表框的子程序
MC_LoadData()
'将我们的对话框显示在屏幕上
MC_Dialog.Show()
'后续所有命令将在关闭对话框后执行
'从内存中移除对话框
MC_Dialog.Unload()
End Sub
```

```vbbasic
Sub MC_LoadData
'我们将此文档的单词存储在文档属性（文件，属性）的注释字段中。
Dim IntCharNumber As Integer
Dim StrData As String, StrWord As String, StrChar As String
Dim BoolAddedWord As Boolean
'移除列表框中包含单词的所有项
MC_Dialog.WordsList.Clear
'我们必须检查列表框是否至少添加了一个单词，因为我们想要突出第一个条目
BoolAddedWord = False
'将注释保存为字符串
StrData = oActiveDocument.DocumentInfo.Description
'我们需要一个变量来逐字符地收集实际单词
StrWord = "*"
'列表框的单词或短语都在一个字符串中，用星号分隔：
StrData = "*Word1*Word2*Phrase No.1*Word3*"
'我们逐字符遍历这个字符串。如果实际字符是 *，则将上一个单词添加到列表否则将字符添加到我们正在收集的单词中
For IntCharNumber = 1 To Len(StrData)
'我们遍历字符串；StrData 和 StrChar 存储实际字符
StrChar = Mid(StrData,IntCharNumber,1)
'如果遇到遇到分隔符，实际单词的收集就结束。将此单词添加到列表并继续
If StrChar = SeparatorChar Then
'我们的列表中不需要空单词
If BoolAddedWord = False
'添加实际单词
MC_Dialog.WordsList.AddItem(StrWord)
'记住，我们至少添加了一个单词
```

### 在 StarBasic 中构建整个应用程序

```vbbasic
BoolAddedWord = True
'为下一个单词做准备。因此删除旧单词。
StrWord = ""
Else
'我们接收到一个字符，将其添加到实际单词中
StrWord = StrWord + StrChar
Endif
'如果至少添加了一个单词，我们突出列表框中的第一个项
If BoolAddedWord Then
MC_Dialog.ListBox.ListIndex = 0
MC_Dialog.ListBox.Selected(0) = true
Endif
End Sub
```

```vbbasic
Sub MC_AddWord
'SelectionText 返回高亮的文本或光标所在处的整个单词。将此添加到列表
MC_Dialog.ListBox.AddItem(oActiveWindow.SelectionText())
'调用子程序来存储新单词（以及其他单词）
MC_SaveData()
'关闭对话框，无事可做
MC_Dialog.Hide()
End Sub
```

```vbbasic
Sub MC_SaveData
'让我们将列表框中的单词存储到此文档的注释字段中
Dim I As Integer
Dim StrData As String
'StrData 是用于存储所有用 ** 分隔单词的变量最后我们将对其赋值给文档注释字段
StrData = ""
'遍历列表框中的所有项并将所有单词接到字符串
For I = 0 To MC_Dialog.ListBox.ListCount - 1
'将下一个单词连接到字符串后并加上 *
StrData = StrData + MC_Dialog.ListBox.List(i) & StrChar
Next i
'将单词列表保存到文档。
oActiveDocument.Document.Description = StrData
End Sub
```

```vbbasic
Sub MC_InsertWord
'将列表中的实际项插入当前光标位置。
oActiveWindow.Insert(MC_Dialog.ListBox.Text)
'关闭对话框，用户可以继续处理他们的文本。
MC_Dialog.Hide()
End Sub
```
