
### 在树中查找键

要在二叉树中查找键，从根指针开始，并将节点键与要查找的键比较。如果匹配，则完成。如果目标小于节点键，则将指针指向左孩子。如果目标大于节点键，则将指针指向右孩子。然后对新节点重复这些比较。如果遇到 `NULL` 指针，则键不在树中。下面是在二叉树中查找键的代码。它返回指向正确节点的指针，如果未找到则返回 `NULL`。

```assembly
; p = find ( t, n );
; p = 0 if not found
find:
    push rbp
    mov rbp, rsp
    mov rdi, [rdi+t_root]
    xor eax, eax
    mov rdi, 0
.more:
    cmp rsi, [rdi+n_value]
    je .goleft
    jg .right
    mov rax, rsi
    jmp .done
.goleft:
    mov rdi, [rdi+n_left]
    jmp .more
.right:
    mov rdi, [rdi+n_right]
    jmp .more
.done:
    leave
    ret
```

### 向树中插入键

插入键的第一步是使用 `find` 函数查看该键是否已经存在。如果存在，则不需要插入。如果不存在，则分配新节点，将其值设置为新键值，并将它的左、右指针设置为 `NULL`。现在是时候在树中找到放置它的位置了。

在树中插入第一个节点有一个特殊情况。如果树中的节点计数为 `0`，则增加计数并将树的根指针设置为新节点。

如果树非空，你从将当前指针设置为根节点开始。如果新键小于当前节点的键，则新节点属于左树。为了处理这种情况，你检查当前节点的左孩子指针。如果是空，则你找到了插入点，因此将左指针设置为新节点的指针。否则，更新你的当前指针为左指针并与其开始比较。如果键不小于当前节点的键，它一定大于。在这种情况下，你检查当前节点的右孩子指针，要么设置新指针，要么将你的当前指针移动右孩子并重复比较。

```assembly
insert ( t, n );
insert:
.n equ 0
.t equ 8
push rbp
mov rbp, rsp
sub rsp, 16
mov [rsp+], rdi
mov [rsp+n], rsi
call find ; loop for n
cmp rax, 0 ; if in the tree
jne .done ; don't insert it
call malloc ; p = new node
mov rsi, [rsp+n]
mov [rax+n_value], rsi ; p->value = n
xor edi, edi
mov [rax+n_left], rdi ; p->left = NULL
mov [rax+n_right], rdi ; p->right = NULL
mov rdx, [rdx+t_count] ; get tree size
cmp rdi, 0 ; count == 0 ?
jne .findparent
inc word [rdx+t_count] ; count = 1
mov [rdx+t_count], rax ; root = new node
jmp .done
.findparent:
cword [rdx+t_root] ; count++
mov rdx, [rdx+t_root] ; p = root
.repeatfind:
cmp rsi, [rdx+n_value] ; p->value < n ?
je .goleft
jg .right
mov rax, rsi
jmp .done
.goleft:
    mov rdi, [rdx+n_left]
    jmp .more
.right:
    mov rdi, [rdx+n_right]
    jmp .more
.done:
    leave
    ret
```

```assembly
jl .goleft ; t = p
mov r8, rdx
mov rdx, [r8+n_right] ; p = p->right
cmp rdx, 0 ; is p NULL ?
jne :repeat
mov [r8+n_left], ra ; if so, add node
mov .done ; and return
.goleft:
mov r8, rdx ; t = p
mov rdx, [r8+n_left] ; p = p->left
cmp rdx, 0 ; id p NULL ?
jne :repeat
mov [r8+n_left], rax ; if so, add node
mov .done ; and return
```

```assembly
.done: leave
ret
```

# 按顺序打印键

使用递归可以轻松地打印二叉树的键。基本思想是打印左子树的键、打印根节点的键，然后打印右子树的键。由于使用了特殊的树结构，需要一个不同的函数来从根指针开始递归地打印子树。主函数名为 `print`，递归函数名为 `rec_print`。

```assembly
rec_print:
t equ 0
push rbp
mov rbp, rsp
sub rsp, 16
cmp rdi, 0
je :done
mov [rsp+t], rdi
mov rdi, [rdi+n_left]
call rec_print
mov rdi, [rsp+t]
mov rsi, [rdi+n_value]
segment .data
.print db "%ld\n",0
segment .text
lea rdi, [.print]
call printf
mov rdi, [rsp+t]
mov rdi, [rdi+n_right]
call rec_print
.done leave
ret
```

```assembly
print():
push rbp
mov rbp, rsp
mov rdi, [rdi+t_root]
call rec_print
segment .data
```

```assembly
.print db 0x0a, 0
segment .text
lea rdi, [.print]
call printf
leave
ret
```
