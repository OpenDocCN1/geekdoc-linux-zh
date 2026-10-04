本节的任务就是去除这个提示窗口。

在此之前，我们可以确定的事实是：

+   ① 在 SAP GUI 客户端程序中，环境变量TDW_NOCOMPRESS被设为1。

借用文件管理器FAR程序[2]，我们可以在SAPguib.dll里找到这个字符串。

然后，我们用IDA编辑器打开文件SAPguib.dll，在文件中搜索字符串“TDW_NOCOMPRESS”。或许的是，我们可以找到这个字符串，而且整个文件只有一处指令调用了这个字符串。

该任务的相关指令为：[3]

```
.text:6440D51B      lea      eax, [ebp+218h+var_211C]
.text:6440D51E      push      eax      ; int
.text:6440D51F      push      offset tdw_ncompress ;
."TDW_NOCOMPRESS"
.text:6440D524      mov      byte ptr [edi+15h], 0
.text:6440D528      call     chk_env
.text:6440D52D      pop      ecx
.text:6440D52E      pop      ecx
.text:6440D52F      push      offset byte_6443438F
.text:6440D534      lea      eax, [ebp+218h+var_211C]
```

```
; demangled name const char* int::CString::Compare(char const*) const *
```

```
.text:6440D537      call     ds:mfc90_1603
.text:6440D53D      test     eax      ; eax
.text:6440D53F      jz       short loc_6440D55A
.text:6440D541      lea      eax, [ebp+218h+var_211C
```

```
; demangled name const char* int::CString::operator PCXSTR
```

```
.text:6440D544      call     ds:mfc90_910
.text:6440D54A      push     eax      ; Str
.text:6440D54B      call     ds:atoi
.text:6440D551      test     eax, eax
.text:6440D553      setnz   al
.text:6440D556      pop      ecx
.text:6440D557      mov      [edi+15h], al
```

由此可见，chk_env()函数通过第二个参数获取环境变量字符串，然后MFC字符串函数继续处理这个字符串，接下来按照标准C函数atoi()的字符