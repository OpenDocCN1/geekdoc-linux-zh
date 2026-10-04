; fake luggage
real_code:

我们还可以看看其他的例子（同样，我们假定ESI始终会零）。

# 50.2.4 把指令序列搞乱

```
instruction 1
instruction 2
instruction 3
```

上面的3行正常执行的指令序列可以用下所示的复杂结构替代：

```
begin:\           jmp        ins1_label
ins2_label:      instruction 2
               jmp        ins3_label
ins3_label:      instruction 3
               jmp        exit:
ins1_label:      instruction 1
               jmp        ins2_label
exit:
```

# 50.2.5 使用间接指针

```
dummy_datal   db        100h dup (0)
message1       db        'hello world',0
dummy_data2   db        200h dup (0)
message2       db        'another message',0
```

```
func           proc
               ...
reloc here     mov       eax, offset dummy_datal ; PE or ELF
               add       eax, 100h
               push      eax
               call      dump_string
```