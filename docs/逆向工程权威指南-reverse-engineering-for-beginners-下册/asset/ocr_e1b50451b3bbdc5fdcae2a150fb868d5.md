```
.text:00541379 mov ecx, esi
.text:0054137B mov ebx, eax ; allocated buffer
pointer -> to EBX
.text:0054137D mov edx, ecx
.text:0054137F xor eax, eax
.text:00541381 mov edi, ebx
.text:00541383 push ebp ; File
.text:00541384 shr ecx, 2
.text:00541387 rep stosd
.text:00541389 mov ecx, edx
.text:0054138B push 1 ; Count
.text:0054138D and ecx, 3
.text:005413900 stosb ; memset(buffer, 00,
aligned_size)
```

# 调用C函数read()读取文件:

```
.text:00541392 mov eax, [esp+38h+Str]
.text:00541396 push eax ;
ElementSize
.text:00541397 push ebx ; DstBuf
.text:00541398 call _fread ; read
file
.text:0054139D push ebp ; File
.text:0054139E call _fclose
```

# 调用crypt()函数，并且向这个函数传递缓冲区、缓冲区尺寸和密码字符串:

```
.text:005413A3 mov ecx, [esp+44h+password]
.text:005413A7 push ecx ; password
.text:005413A8 push esi ; aligned
size
.text:005413A9 push ebx ; buffer
.text:005413AA call crypt ; do crypt
```

创建输出文件。虽然研发人员确实检测了能否成功打开文件，但是他们忘记了检测能否创建文件:

```
.text:005413AF mov edx, [esp+50h+Filename]
.text:005413B3 add esp, 40h
.text:005413B6 push offset aW ; "wb"
.text:005413BB push edx ;
Filename
```