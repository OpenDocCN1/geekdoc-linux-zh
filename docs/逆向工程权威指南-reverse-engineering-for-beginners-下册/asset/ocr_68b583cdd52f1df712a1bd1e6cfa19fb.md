.text:00541348 ;
.text:00541348 loc_541348:

# 通过fseek()/ftell()函数获取文件大小:

```
.text:00541348 push ebx
.text:00541349 push esi
.text:0054134A push edi
.text:0054134B push 2              ; Origin
.text:0054134D push 0              ; Offset
.text:0054134F push ebp              ; File

; move current file position to the end
.text:00541350 call fseek
.text:00541355 push ebp              ; File
.text:00541356 call ftell         ; get current file
position
.text:0054135B push 0              ; Origin
.text:0054135D push 0              ; Offset
.text:0054135F push ebp              ; File
.text:00541360 mov [esp+2Ch+Str], eax
```

; move current file position to the start
.text:00541364 call _fseek

上述指令将文件大小64字节边界对齐。程序采用的加密算法只能处理64字节消息块，它的算法相当直白：把文件除以64，舍弃余数，然后把整除结果乘以64。下述指令的“与”运算起到整除64并清除剩余的操作，然后用加法运算把指令送到上述整除的商加到64。重组指令将文件大小64字节边界对齐。

```
.text:00541369 esi, [esp+2Ch+Str]
; reset all lowest 6 bits
.text:0054136D and esi, 0FFFFFC0h
; align size to 64-byte border
.text:00541370 add esi, 40h
```

接下来按照上述结果分配缓冲区:

```
.text:00541373 push esi              ; Size
.text:00541374 call _malloc
```

调用用memset()，即清除缓冲区数据：[1]