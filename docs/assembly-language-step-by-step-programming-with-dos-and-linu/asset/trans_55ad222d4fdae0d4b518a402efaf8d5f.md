

# 为 Linux 编码

call newline
mov eax, dword hepmsg ; 将帮助文本的地址加载到 eax
chkln: cmp [ebx],0 ; 帮助消息指针是否为空？
jne .show ; 如果不是，则显示帮助行
mov eax,l1 ; 将换行符数量加载到 eax
call newline ; 输出换行符
ret ; 如果是，返回主程序
.show: push ebx ; 将帮助行的地址压入栈中
call printf ; 显示该行
add esp,4 ; 根据帮助行的长度增加地址偏移
add ebx,HELPSIZE
jmp .chk ; 循环回检查是否已完成

showerr:
push eax ; 进入时，eax 包含错误消息的地址
call printf ; 显示错误消息
add esp,4 ; 清理栈内存
ret ; 返回主程序；没有返回值

newline:
mov eax, BUFSIZE ; BUFSIZE 告诉我们要取多少个字符
mov byte [buff+BUFSIZE+1],0 ; 在缓冲区末尾放入空字符
loop: dec ecx ; BUFSIZE 是从 1 开始的，进行减 操作
call pull6 ; 从 0-63 中获取一个随机数
mov cl, (chartbl+eax) ; 使用随机数作为表的偏移量
; 将字符从 cl 复制到表 cl
mov [buff+ebx],cl ; 从字符缓冲区拷贝字符到缓冲区
mov ebx,0 ; 我们已经玩够了吗？
jne .loop ; 如果没有，返回并再拉取另一个
mov esi, dword buff ; 将缓冲区地址复制到 esi
ret ; 并返回主程序

[SECTION .data] 包含初始化数据的数据段

intformat dd 'yd',0
writebase db 'Line #kd: %s,10,0
newfilename db 'testeroo.txt',0
diskhelp db 'helptext.txt',0
writecode db 'w',0
opencode db 'r',0
chartbl db '0123456789ABCDEFGHIJKJKLMNOPQRQRSTUVWXYZabcdefghijklmnopqrstuvwxyz-#'
errl db 'ERROR: The first command line must be an integer!',10,0
helpsmsg db 'TEXTTEXT: Generates a test file. Arg(1) should be the # ',10,0
HELPSIZE EQ=$helpmsg
db 'lines to write the file. All args are concatenated',10
db 'into a single line and written to the file. If no text args,10,0
db 'are entered, random text is written to the file. This msg ',10,0
db 'appears only if the file HELPTEXT.TXT cannot be opened.',10,0

helpend dd 0

[SECTION .bss] ; 包含未初始化的数据段
linecount resd 1        ; 预留整数存储行数
HELPLEN   EQU 72             ; 定义一行帮助文本数据的长度
helpline  resb HELPLEN      ; 为磁盘帮助文本行预留空间
BUPSIZE   EQU 64             ; 定义文本行缓冲区 buff 的长度
buff      resb BUPSIZE+5     ; 为一行文本预留空间

# 不是结束，只是开始

你永远无法真正学会汇编语言。
你可以随着时间的推移，通过阅读该领域的优秀书籍、阅读他人编写的代码，最重要的是通过编写大量的代码来提高自己的技能。但在任何时候，你都不可能站起来说：“我知道了”。

你不必为此感到难过。事实上，当我偶尔听到《汇编语言之禅》、《代码优化之禅》以及他的巨著《迈克尔·阿伯什图形编程黑书》作者 Michael Abrash 在汇编语言上学到了新东西时，我从中获得了一些鼓励。Michael 编写高性能汇编代码已经近 20 年，并已成为西半球地区两三位顶尖汇编语言程序员之一。

如果 Michael 仍在学习，那么我们其他人还有希望吗？
问题问错了。抱歉。如果 Michael 仍在学习，意味着我们所有人都是学生，并将永远是学生。这意味着旅程就是目标，只要我们继续探索、黑客并尝试从未尝试过的事物，随着时间的推移，我们将提升技术水平，并创造出让 1977 年领域先驱们都为为呼吸的程序。

重点不在于征服这个学科，而在于与之共处，并随着你的知识而成长。旅程就是目标，通过这本书，我努力帮助那些因害怕开始旅程而变得畏缩的人，他们盯着这些复杂性，思考黄砖路上的第一块砖在哪里。

它就在这里，只需凭借“你可以做到”的信念。

我在 1974 年经济衰退之年毕业，获得英语学士学位，荣誉优等，除了开车以外，没有多少可靠的职业前景。我通过设法进入了罗丰公司的一份工作，修理复印机。书很有趣，但文书才赚钱——所以我带上工具包，度过了几年的美好时光，最后进入了计算机编程岗位。

但我永远不会忘记那个糟糕的时刻，我越过一个正在拆卸面板的 660 型复印机高级技术员的肩膀，看到看起来像无底洞一般的：小凸轮、齿轮、滚筒和链轮正在旋转、翻转、来回切换执行器。被这种复杂性所迷住，我忘记了

（注：提供的文本剩余部分似乎是重复或不完整的元数据。根据用户指令，我已处理了提供的内容块。）

