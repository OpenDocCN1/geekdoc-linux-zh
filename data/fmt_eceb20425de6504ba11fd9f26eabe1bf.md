
| `wxLANGUAGE_ENGLISH_AUSTRALIA` | en_AU |
| `wxLANGUAGE_ENGLISH_BELIZE` | en_BZ |
| `wxLANGUAGE_ENGLISH_BOTSWANA` | en_BW |
| `wxLANGUAGE_ENGLISH_CANADA` | en_CA |
| `wxLANGUAGE_ENGLISH_CARIBBEAN` | en_CB（见下） |
| `wxLANGUAGE_ENGLISH_DENMARK` | en_DK |
| `wxLANGUAGE_ENGLISH_EIRE` | en_IE（见下） |
| `wxLANGUAGE_ENGLISH_JAMAICA` | en_JM |
| `wxLANGUAGE_ENGLISH_NEW_ZEALAND` | en_NZ |
| `wxLANGUAGE_ENGLISH_PHILPINES` | en_PH |
| `wxLANGUAGE_ENGLISH_SOUTH_AFICA` | en_ZA |
| `wxLANGUAGE_ENGLISH_TRINIDAD` | en_TT |
| `wxLANGUAGE_ENGLISH_ZIMBABWE` | en_ZW |

`CB` (`wxLANGUAGE_ENGLISH_CARIBBEAN`) 国家代码并非来自 ISO 3166，而 `IE` (`wxLANGUAGE_ENGLISH_EIRE`) 被 ISO 3166 定义为爱尔兰，而不是爱尔兰。因此，在选择合适的语言代码时需要小心。为了确定具体使用了哪个国家代码，wxWidgets 源码 `src/common/intl.cpp` 初始化了一个包含此信息的表；我建议在 `intl.cpp` 中搜索 `wxLANGUAGE_` 枚举以确定正确的值，如下：

```bash
$ grep wxLANGUAGE_ENGLISH_EIRE intl.cpp
LNG(wxLANGUAGE_ENGLISH_EIRE, \
"en_IE", LANG_ENGLISH , SUBLANG_ENGLISH_EIRE \\
  "English (Eire)")
```

为了添加爱尔兰英语语言支持，我们会在开发树的 `en_IE` 中添加条目，如下：

# wx Widgets 425

```
/locale
/en
messages.po
/en_IE
messages.po
/es
messages.po
/ru
messages.po
/fr
messages.po
/de
messages.po
```

并将对 `wxLocale::Init()` 的调用修改如下所示：

```cpp
bool MyApp::OnInit()
{
myLocale.Init(wxLANGUAGE_EN_EIRE);
}
```

通常情况下，最好使用 `wxLANGUAGE_DEFAULT`，并确保应用程序必须支持的区域和语言环境的 MO 文件已正确分发。

# 在运行时加载消息文件

现在，剩下的工作就是确保加载应用程序所需的（文件（或多个消息文件）。如前所述，wxWidgets 会加载一个名为 `wxstd` 的内部文件，该文件包含了在 wxWidgets 源代码中定义的错误和标签。但它对你应用程序的 MO 文件一无所知。要加载你自己的 MO 文件，必须像下面的示例所示调用 `wxLocale` 方法 `AddCatalog()`：

```cpp
bool MyApp::OnInit()
{
myLocale.Init(wxLANGUAGE_DEFAULT);

if (myLocale.AddCatalog("messages") == FALSE) {
printf("Unable to load catalog\n");
}
```

# 426

# 第 8 章 wxWidgets

```cpp
exit(1);
```

```cpp
}
```

```cpp
Toplevel *frame = new Toplevel("Toplevel",
wxPoint(50,50), wxSize(450,340));
frame->Show(TRUE);
SetTopWindow(frame);
return TRUE;
```

```cpp
}
```

`AddCatalog()` 会附加 `.mo` 扩展名，并根据区域语言（如前所示，通过 `wxLocale::Init()` 设置）查找指定的指定目录。假设你是一个非常有条理的人，决定准备多个消息文件：一个用于菜单项（menu.mo），一个用于错误消息（errors.mo），还有一个用于控件标签（labels.mo）。那么，你将通过分别调用 `AddCatalog()` 来加载它们，如下所示：

```cpp
bool MyApp::OnInit()
{
myLocale.Init(wxLANGUAGE_DEFAULT);

if (myLocale.AddCatalog("menu") == FALSE)
    printf("Unable to load catalog\n");
    exit(1);
}
```

```cpp
if (myLocale.AddCatalog("errors") == FALSE)
    printf("Unable to load catalog\n");
    exit(1);
}
```

```cpp
if (myLocale.AddCatalog("labels") == FALSE)
    printf("Unable to load catalog\n");
    exit(1);
}
```

```cpp
Toplevel *frame = new Toplevel("Toplevel",
wxPoint(50,50), wxSize(450,340));
frame->Show(TRUE);
SetTopWindow(frame);
return TRUE;
```

}
