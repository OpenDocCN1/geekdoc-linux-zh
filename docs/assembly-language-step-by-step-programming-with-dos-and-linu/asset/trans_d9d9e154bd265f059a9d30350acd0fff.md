

# 为 Linux 编码

```assembly
push dword 7          ; 取的数字位数，单位为位
push dword [pulls]      ; 生成的随机数个数
push dword display      ; 基础显示字符串的地址
call printf             ; 显示标签
add esp,12               ; 清理 printf 调用留下的栈空间
call shownums           ; 显示随机数的行
```

```assembly
; 创建并显示一个 4 位随机值数组：
mov edi, dword pull4     ; 将随机数生成子程序的地址复制到 edi
call puller             ; 按照 [pulls] 中的要求推送多个数字
push dword 4            ; 取的数字位数，单位为位
push dword [pulls]      ; 生成的随机数个数
push dword display      ; 基础显示字符串的地址
call printf             ; 显示标签
add esp,12               ; 清理 printf 调用留下的栈空间
call shownums           ; 显示随机数的行
```

```assembly
; 将缓冲区清为空值
bufcl r: mov exc, BUFSIZE+5 ; 填充整个缓冲区，外额外加 5 以确保安全
.loop: dec exc             ; BUFSIZE 是从 1 开始的，先减1
mov byte [randchar+exc],0 ; 将空值移缓冲区
cmpx exc,0               ; 完成了吗？
jnz .loop                ; 如果未完成，返回并填充另一个空值
```

```assembly
; 创建一个随机字母数字字符字符串
Pulchr: mov exc, BUFSIZE ; BUFSIZE 告诉我们需要取多少字符
.loop: dec exc             ; BUFSIZE 是从 1 开始的，先减1
mov edi, dword pull16    ; 范围为 0-63
call puller              ; 获取一个 0-63 之间的随机数
mov cl,[chartbl+eax]    ; 使用随机数作为表的偏移量
                         ; 将表中的字符复制到 cl
mov byte [randchar+exc],cl ; 将字符从 cl 复制到字符缓冲区
cmpx exc,0               ; 玩够了吗？
jnz .loop                ; 如果未完成，返回并取另一个空值
```

```assembly
; 显示字符串
mov eax,1                ; 输出换行符
call newline            ; 使用换行子程序
push dword randchar     ; 推送字符缓冲区的地址
call puts               ; 调用 puts 显示它
add esp,4                ; 清理栈空间
mov eax,1                ; 输出换行符
call newline            ; 使用换行子程序
```

```assembly
; 此后的所有内容皆为模版代码；适用于所有常规任务！
pop ebp                  ; 恢复保存的寄存器
pop esi
pop ebx
mov esp,ebp             ; 在返回前销毁栈帧
pop ebp
ret                     ; 返回控制权给 Linux
```

# 汇编语言逐步进阶

```assembly
;; 子程序===================================================================
;
; 随机数生成器子程序 -- 最后更新于 1999/12/1
;
; 此例程提供了 5 个入口点，并根据 rand 返回的值返回 5 个 
; 不同“大小”的伪随机数。首先注意，
; rand 取出的是一个 31 位的值。高 16 位是最“随机”的，
; 所以为了返回范围较小的数字，你获取一个 31 位的值，
; 并向右移零填充你需要的任意位数。一个 8 位
; 随机值范围是 0-255，7 位为 0-127，依此类推。
; 尊重 esp, esi, edi, ebx 和 esp 寄存器。在 eax 中返回随机值。

pull31: mov ecx,0 ; 对于 31 位随机数，我们不移位
jmp pull
pull16: mov ecx,15 ; 对于 16 位随机数，移位 15 位
jmp pull
pull8: mov ecx,23 ; 对于 8 位随机数，移位 23 位
jmp pull
pull7: mov ecx,24 ; 对于 7 位随机数，移位 24 位
jmp pull
pull6: mov ecx,25 ; 对于 6 位随机数，移位 25 位
jmp pull
pull4: mov ecx,27 ; 对于 4 位随机数，移位 27 位
pull: push ecx ; rand 会破坏 ecx;将移位值存在栈上
	call rand ; 调用 rand 获取随机值；返回在 eax
	pop ecx ; 将移位值弹出回 ecx
	shr eax,cl ; 按选定的因子移位随机值
	; 记住我们需要的部分在 cl 中
	ret ; 带着 eax 中的随机数返回

-----------------------------------------------------------------
; 换行符输出 -- 最后更新于 1999/12/1
;
; 此例程允许向标准输出（stdout）输出数量换行符，取决于
; 传递 eax 的值。合法值为 1-10。所有关键寄存器均
; 尊重。在 eax 中传递 0 值将导致不产生换行符。
-----------------------------------------------------------------
newline:
	mov ecx,10 ; 我们需要一个跳过值，即 10 减
	sub ecx,eax ; 调用者需要的换行符数量。
	add ecx,dword nl ; 此跳过值加到调用 printf 之前的
	; 换行符地址上。
	push dwarf ecx
	call printf ; 显示选定数量的换行符
	add esp,4                ; 清理栈
	ret
```

在 Linux 中，rand 函数返回一个 31 位的值。高 16 位是最“随机”的，因为低位受线性同源生成器周期的影响。如果你想限制随机数的范围，可以将 31 位的值向右移动 25 位。问题显而易见：假设你想取随机字符？只有 127 个 ASCII 字符，实际上只有 62 个是字母数字（其余是标点符号、空白字符、控制字符如表情符号）。你需要做的是获取一个小于 62 的随机数。这需要很长时间。显然，你需要不同的方法。这种方法将 rand 返回的 31 位值视为随机位的集合。6 位可以表示 0-63，所以我从原始值中提取高位来指定随机字符。这很简单：我将 31 位的值向右移动，直到高 6 位移出值的右端消失。同样的技巧适用于任何（合理的）位数。你所做的只是选择移动位数。我创建了一个具有多个入口点的子程序，每个入口点从随机值中选择特定的位数：

```assembly
pull31: mov ecx,0  ; 对于 31 位随机数，我们不移位
       jmp pull
pull16: mov ecx,15 ; 对于 16 位随机数，移位 15 位
       jmp pull
pull8: mov ecx,23  ; 对于 8 位随机数，移位 23 位
       jmp pull
pull7: mov ecx,24  ; 对于 7 位随机数，移位 24 位
       jmp pull
pull6: mov ecx,25  ; 对于 6 位随机数，移位 25 位
       jmp pull
pull4: mov ecx,27  ; 对于 4 位随机数，移位 27 位
pull: 
	push ecx       ; rand 会破坏 ecx;将移位值存在栈上
	call rand      ; 调用 rand 获取随机值；返回在 eax
	pop ecx         ; 将移位值弹出回 ecx
	shr eax,cl     ; 按选定的因子移位随机值
```

