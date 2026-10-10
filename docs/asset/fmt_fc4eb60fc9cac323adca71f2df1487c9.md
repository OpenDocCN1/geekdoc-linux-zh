
`makensis` 命令将向控制台输出内容，描述解析安装脚本时正在发生的情况。如果 `makensis` 遇到语法或逻辑错误，它将报告这些错误，并根据严重程度中止。扫描 `makensis` 的输出以确定是否发生了任何错误是非常重要的。如果一切顺利，将创建由 `$OutFile` 变量指定的安装程序二进制文件。

## 测试安装程序

测试安装程序可以运行所有可能的用例例（安装类型、用户选择），并确保安装程序按预期工作。这是通过使用 Windows 资源管理器确定文件是否在它们应该所在的位置，并使用 `regent` 检查你的安装程序修改的注册表项来实现。当然，能够启动并成功执行该程序也应该是安装程序测试的一部分。如果安装程序运行异常，你可以返回脚本并添加调试语句在安装程序执行期间显示变量，从而对安装程序进行调试。`MessageBox` 函数本质上封装了 Win32 `MessageBox` 函数（详情请参阅上述的 NSIS 文档），并可用于此目的。

## 分发安装程序

剩下的就是将安装程序二进制文件上传到网络，或将其复制到发行介质上。安装程序是自包含的，它将保持你的应用程序以及安装程序负责的任何文件的压缩版本，因此没有必要对安装程序进行进一步压缩。

# 项目 15：为原生安装程序提供支持

## 添加卸载程序

在 NSIS 中添加应用程序卸载的支持非常简单，基本上可以通过向 NSIS 脚本添加一个新节（其中包含在卸载时执行的命令），并通过在之前创建的安装节中添加命令，将信息存储在 Windows 注册表中，以便卸载程序可以使用这些信息定位文件和其他资源。（记住，用户允许在运行时选择安装位置，因此我们无法将此信息编码到安装程序脚本中——在卸载之前我们可以依赖的存储这些信息的固定位置是 Windows 注册表。）以下是添加到上方 `MyAppApp` 节中的代码，它负责在安装时存储注册表信息并创建。以下代码大部分是样板代码；将 `MyApp` 更改为你的应用程序名称是简单卸载程序唯一需要的更改：

```nsis
; 将安装路径写入注册表

WriteRegStr HKLM SOFTWARE\MyApp\"Install_Dir" \
"$INSTDIR"

; 写入 Windows 卸载键

WriteRegStr HKLM\"Software\Microsoft\Windows\CurrentVersion\Uninstall\nMyApp"DisplayName" \ "MyApp"

WriteRegStr HKLM\"Software\Microsoft\Windows\CurrentVersion\Uninstall\nMyApp"UninstallString" \ "\$INSTDIR\\uninstall.exe"

WriteRegDWORD HKLM\"Software\Microsoft\Windows\CurrentVersion\Uninstall\nMyApp"NoModify" 1

WriteRegDWORD HKLM\"Software\Microsoft\Windows\CurrentVersion\Uninstall\nMyApp"NoRepair" 1

WriteUninstall "uninstall.exe"
```

卸载节所示，主要由 `Delete` 和 `RMDIR` 命令组成，用于删除安装程序创建的任何文件或目录以及移除注册表项：

```nsis
Section "Uninstall"
  ; 删除注册表项
DeleteRegKey HKLM
"Software\MyApp\Windows\CurrentVersion\Uninstall\
MyApp"
DeleteRegKey HKLM SOFTWARE\MyApp
  ; 删除文件和安装程序
Delete $INSTALLDIR\*.*
Delete $INSTALLDIR\uninstall.exe
  ; 删除快捷方式（如果有）
Delete "\$SMPGRAMS\MyApp\*.*"
  ; 删除已使用的目录
RMDir "\$SMPGRAMS\MyApp"
RMDir "$INSTDIR"
SectionEnd
```

通过上述更改，我们只需要指定由卸载程序显示哪些页面。只需要两个 `UninstPage` 命令实例（位于脚本中全局作用域内 `Page` 命令旁边）即可：

```nsis
UninstPage reinstConfirm
UninstPage instfiles
```

## 集成到开始菜单和桌面

在 NSIS 安装程序和卸载程序中集成桌面快捷方式和开始菜单项的支持相当容易。如之前所述，在 Windows XP 的开始菜单中放置项目只需在目录中创建指向应用程序二进制文件的快捷方式；在桌面上放置快捷方式也是如此。NSIS 脚本定义了 `SMPPROGRAMS` 变量，它指定了可以放置快捷方式的目录，导致程序显示在开始菜单的“所有程序”区域。这只是更改 Windows 系统上各种特殊目录位置的大量变量之一。下一节包含以下代码，如果用户选择了该选项，将在开始菜单的“所有程序”中创建一个名为 `MyApp` 的下拉菜单，其中包含代表应用程序及其卸载程序的项：

```nsis
Section "Start Menu Shortcuts"
  ; 通过在 $SMPGRAMS 下创建一个名为 MyApp
  ; 的目录创建创建菜单
  CreatedDirectory "SMPGRAMS\MyApp"
  ; 在 $SMPGRAMS 内部创建快捷方式
  ; 用于卸载程序
  CreateShortCut "$SMPGRAMS\MyApp\Uninstall.lnk"
"$INSTDIR\uninstall.exe" "" "$INSTDIR\uninstall.exe" 0
  ; 用于应用程序
  CreateShortCut "$SMPGRAMS\MyApp\MyApp.lnk"
"$INSTDIR\MyApp.exe" "" "$INSTDIR\MyApp.exe" 0
SectionEnd
```

在两种情况下，`CreateShortCut` 的第三个参数 `""` 定义了传递给应用程序的命令行参数（`""` 表示无参数）。指定它的目的是为了第四和第五个参数。第四个参数指定了从哪个二进制文件获取将显示在开始菜单中的图标，第五个参数是该可执行文件内图标资源的索引。。省略这些参数将使用默认值，这对于大多数应用程序都是足够的。

## 应用程序数据

最后，让我们讨论安装程序如何在 Application Data 文件夹中创建并填充数据。记住 `HKEY_CURRENT_USER\Software\Windows\CurrentVersion\Explorer\Shell Folders` 包含一个名为 `AppData` 的键，我的系统将其设置为 `C:\Data and Settings\Application Data`。对于天气管理器，我想在那里创建一个名为 `weatherxml` 的目录，我们在安装时在那里存储包含某些天气源 URL 的 XML 文件，而在运行时我们将存储通过 HTTP 从 NOAA 下载的数据。为了实现这一点，我可以在 NSIS 安装脚本中添加以下新节：

```nsis
Section "XML Feeds File"
  ; 将输出路径设置为 appdata 下的
  ; 目录。
  SetOutPath $APPDATA\weatherxml
  ; 在此处放置文件
  File /r "..\wxsites.xml"
SectionEnd
```

变量 `$APPDATA` 是指向我的 AppData 目录的 NSIS 变量。`SetOutPath` 定义了 `File` 命令指定的le安装的位置。执行安装程序中的此节将创建 `weatherxml` 目录（如果不存在），并将 `wxsites.xml` 复制到其中。

## 天气管理器的完整示例

以下是天气管理器的完整 NSIS 安装脚本：

```nsis
; 安装名称
Name "Weather Manager"
; 要写入的文件
OutputFile "winstall.exe"
; 默认安装目录
InstallDir $PROGRAMFILES\WeatherManager
; 检查目录的注册表键（这样如果
; 再次安装，它会自动覆盖旧版本）
InstallDirRegKey HKLM "Software\WeatherManager" \
"Install1_Dir"
```

; 页面
Page components
Page directory

页面安装文件

卸载页面重确认

卸载页面安装文件
