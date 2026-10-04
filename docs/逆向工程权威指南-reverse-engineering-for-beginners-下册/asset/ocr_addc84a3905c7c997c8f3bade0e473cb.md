.text:6440500B jz short bypass
.text:6440500D push offset aDataCompressio ; "data
compression switched off\n"
.text:64405012 mov ecx, edi

; demangled name ATL::CString::operator+=(char const *)
.text:64405014 call ds:mfc90_945
.text:6440501A mov [ebp+var_10], ebx
.text:6440501D bypass:

更有意思的是，决定程序是否显示窗口的关键因素是决定var_10:

.text:6440503C cmp [ebp+var_10], ebx
.text:6440503F jnz exit ; bypass drawing

; add strings "For maximum data security device" / the setting(s) as as soon as possible!",

.text:64405045 push offset aForMaximumData ; "\nFor
maximum data security ✓
\v delete\nthe$s..."
.text:6440504A call ds:mfc90_945 ;
ATL::CString::operator+=(char const *)
.text:64405050 xor edi, edi;
.text:64405052 push edi ; fWinIni
.text:64405053 lea eax, [ebp+pvParam]
.text:64405056 push eax ; pvParam
.text:64405057 push edi ; uiParam
.text:64405058 push 30H ; uiAction
.text:6440505A call ds:SystemParametersInfoA
.text:64405060 mov eax, [ebp+var_34]
.text:64405063 cmp eax, 1600
.text:64405068 jie short loc_64405072
.text:6440506A cdq
.text:6440506B sub eax, edx
.text:6440506F sar eax, 1
.text:64405072 mov [ebp+var_34], eax
.text:64405072 push edi ; hWnd
.text:64405072 loc_64405072:

start drawing:

.text:64405072 push hWnd
.text:64405073 mov [ebp+cy], 0A0h
.text:6440507A call ds:GetDC

那么，我们通过实践来验证刚才这些推测。

首先找到这个JNZ指令: