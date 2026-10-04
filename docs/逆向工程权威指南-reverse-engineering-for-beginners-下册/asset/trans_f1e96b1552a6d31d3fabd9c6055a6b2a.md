

.text:6440500B jz short bypass
.text:6440500D push offset aDataCompressio ; "数据压缩关闭\n"
.text:64405012 mov ecx, edi

; 解修后的名称 ATL::CString::operator+=(char const *)
.text:64405014 call ds:mfc90_945
.text:6440501A mov [ebp+var_10], ebx
.text:6440501D bypass:

更有意思的是，决定程序是否显示窗口的关键因素是决定 var_10 的：

.text:6440503C cmp [ebp+var_10], ebx
.text:6440503F jnz exit ; 绕过绘制

; 添加字符串 "For maximum data security device" / the setting(s) as soon as possible!,

.text:64405045 push offset aForMaximumData ; "\n为了最大数据安全 ✓\v delete\nthe$s..."
.text:6440504A call ds:mfc90_945 ; ATL::CString::operator+=(char const *)
.text:64405050 xor edi, edi;
.text:64405052 push edi ; fWinIni
.text:64405053 lea eax, [ebp+pvParam]
.text:64405056 push eax ; pvParam
.text:64405057 push edi ; uiParam
.text:64405058 push 30H ; uiAction
.text:6440505A call ds:SystemParametersInfo
.text:64405060 mov eax, [ebp+var_34]
.text:64405063 cmp eax, 1600
.text:64405068 je short loc_6440572
.text:6440506A cdq
.text:6440506B sub eax, edx
.text:6440506F sar eax, 1
.text:64405072 mov [ebp+var_34], eax
.text:64405072 push edi ; hWnd
.text:64405072 loc_6440572:start drawing:

.text:64405072 push edi ; hWnd
.text:64405073 mov [ebp+cy], 0AH
.text:6440507A call ds:GetDC

那么，我们通过实践来验证刚才的推测。首先找到这个 JNZ 指令：

.text:6440503F jnz exit :绕过绘制

把它改成程序之后，程序就不会显示提示窗口了！下一步，我们找到 load_line 函数（函数名字）里偏移量为 0x15 的数据，以及 CDWs::Info 里的变量 this+3D。这两个值是相等的？为了验证这一猜测，我们需要搜索与偏移量 0x15 有关的全部指令。在这样的程序里，某个变量会被同一个调用；在当前文件中，第一处赋值如下：

```
.text:6440C19 6440C19 proc near
.text:6440C19      = arg_0 dword ptr 4
.text:6440C19      push ebx
.text:6440C19      push ebp
.text:6440C1A      push esi
.text:6440C1B      push edi
.text:6440C1C      mov edi, [esp+10h+arg_0]
.text:6440C1D      mov eax, [edi]
.text:6440C21      mov esi, ecx; ESI/ECX 是指向某些未知对象的指针
.text:6440C23      mov [esi], eax
.text:6440C25      mov eax, [edi+4]
.text:6440C2A      mov [esi+4], eax
.text:6440C2D      mov eax, [edi+8]
.text:6440C30      mov [esi+8], eax
.text:6440C33      lea eax, [edi+0Ch]
.text:6440C36      push eax
.text:6440C37      mov ecx, [esp+0Ch]
```

```
& named: ATL::CString::operator=class ATL::CString
.text:6440C3A      call ds:mfc90_817
.text:6440C40      mov eax, [edi+10h]
.text:6440C43      mov [esi+10h], eax
.text:6440C46      mov al, [edi+14h]
.text:6440C49      mov [esi+14h], al
.text:6440C4C      mov al, [edi+15h];从 0x15 偏移量拷贝字节
.text:6440C4F      mov [esi+15h], al ; 到 CDwsGui 对象中的 0x5 偏移
```

上述函数的调用函数是 CDWs::CopyOptions。这些名字都是参照调试信息的。但是在整理程序流程之后，我们会发现在“时间上”第一次调用上述函数的调用函数是 CDWs::Init()

```
.text:6440B0BF loc_6440B0BF:   mov   eax, [ebp-arg_0]
.text:6440B0BF       push   [ebp-arg_4]
.text:6440B0C2       mov   [esi+28h], eax
.text:6440B0C5       lea   eax, [esi+28h]; ;esi 是指向 CDwsGui 对象的指针
.text:6440B0CE       push   eax
.text:6440B0CF       call   CDWs::CopyOptions
```

综合上述分析：由 load_command_line() 函数返回的数组，是 CDWs 类的一部分。这个数组的地址是 this+28。0x15+0x28=0x3D。这就是数据传递的终端。接下来，我们在程序中查找“使用偏移量0x3D 的指令”。我们发现 CDWsGui::Run 函数（根据调试信息）使用了偏移量：

```
.text:6440D958       cmp [esi+DH], bl; ;esi 是指向 CDwsGui 对象
.text:6440D95B       lea ecx, [esi+B8h]
.text:6440D961       testz al
.text:6440D964       push eax              ; ConnectionContext 的 arg_10
.text:6440D965       push dword ptr [esi+64h]
```

```
; demanded name: const char* ATL::CString::operatorPCX
.text:6440D968       call ds:mfc90_910; 无参数
.text:6440D96E       push eax
.text:6440D96F       lea ecx, [esi+BCh]
```

```
; demanded name: const char* ATL::CString::operatorPCX
.text:6440D975       call ds:mfc90_910; 无参数
.text:6440D975       push eax
.text:6440D97B       push esi
.text:6440D97D       lea ecx, [esi+8h]
.text:6440D980       call ConnectionContext::Create
```

而后，验证我们的推测：“testz al”替换为“xor eax, eax”，清除环境变量再次运行。此后，令人惊讶的是提示窗口果然不见了，而且 Wireshark 包不再压缩了！这种修改对 ConnectionContext 对象的标识直接操作。可见，压缩标识到了 ConnectionContext::Create 的第五个参数。不过构造函数还调用了其他：

```
.text:64403476 push [ebp+compression]
.text:64403479 push [ebp+arg_C]
.text:6440347C push [ebp+arg_8]
.text:6440347F push [ebp+arg_4]
.text:64403482 push [ebp+arg_0]
.text:64403485 call CNetwork::CNetwork
```

压缩标识被传递到 CNetwork::CNetwork 的第五个参数。根据这个参数，函数在 CNetwork 对象上设置标识、并设置一个压缩有关的变量。这个构造的操作如下：

```
.text:6441DF1 cmp [ebp+compression], esi
.text:6441DF7 jz short set_EAX_to_0
.text:6441DF9 mov al, [ebx+7] ;另一个值可能影响压缩
.text:6441DFC4 cmp al, '3'
.text:6441DPEE jz short set_EAX_to_1
.text:6441E00 cmp al, '4'
.text:6441E02 jnz short set_EAX_to_0
.text:6441E04 set_EAX_to_1:
.text:6441E04 xor eax, eax ; EAX -> 1
.text:6441E07 jmp short loc_6441EB
.text:6441E09 set_EAX_to_0:
.text:6441E09 xor eax, eax ; EAX -> 0
.text:6441E0B mov loc_6441EB:
.text:6441E0B mov [ebx+3Ah], eax ; EAX 是指向 CNetwork 对象
```

综上，我们可以确定 CNetwork 存储压缩标识的相对地址是 this+0x3A。

然后我们以 0x34 为偏移量着手，继续分析 SAPilib.dll。这个偏移再次出现在 CDWSGui::OnClientMessage 里。当然，笔者是通过调试才能确定构造函数的准确名称：

```
.text:6440F76 loc_6440F76: mov ecx, [ebp+728h+var_7794]
.text:6440F76 mov ecx
.text:6440F79 cmp dword ptr [ecx+3A4h], 1
.text:6440F80 jnz compression_flag_is_zero
.text:6440F86 mov byte [ebx+7], 1
.text:6440F8A mov eax, [esi+1h]
.text:6440F8BD mov ecx, eax
.text:6440F8BF mov eax
.text:6440F91 test [ebp+F4h], eax
.text:6440F93 mov ecx, [esi+h]
.text:6440F96 mov eax, [esi]
.text:6440F9F test [ebp+728h+var_7794
.text:6440FA02 push offset
.text:6440FA03 lea eax, [ebp+h]
.text:6440FA07 push dword ptr [ebp+28h]
.text:6440FA08 mov eax, [ebp+24h]
.text:6440FAE call offset
.text:6440FB4 mov [esi+24h], eax
.text:6440FBC mov [esi+24h], 00000
.text:6440FCE cmp [ebp+compression], esi
.text:6440FCD4 mov eax, [edi+10h]
.text:6440FCD6 jz short set_EAX_to_0
.text:6440FCD7 mov al, [edi+14h]
.text:6440FCD9 mov [esi+14h], al
.text:6440FCE mov al, [edi+15h]
.text:6440FD00 mov [esi+15h], al
.text:6440FD04 call
.text:6440FD05 push [ebp+compression]
.text:6440FD06 push [ebp+arg_C]
.text:6440FD0C push [ebp+arg_8]
.text:6440FD0F push [ebp+arg_4]
.text:6440FD12 push [ebp+arg_0]
.text:6440FD15 call CNetwork::CNet
```

