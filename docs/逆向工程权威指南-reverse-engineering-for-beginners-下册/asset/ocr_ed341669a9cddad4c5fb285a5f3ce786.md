```
call localtime_r
mov eax, [esp+24h] ; tm_year
lea edx, [esp+76Ch] ; edx=eax+1900
mov eax, offset format ; "Year: %d\n"
mov [esp+4], eax
mov [esp], eax
call printf
mov edx, [esp+20h] ; tm_mon
mov eax, offset aMonthD ; "Month: %d\n"
mov [esp+4], edx
mov [esp], eax
call printf
mov edx, [esp+1Ch] ; tm_day
mov eax, offset aDayD ; "Day: %d\n"
mov [esp+4], edx
mov [esp], eax
call printf
mov edx, [esp+18h] ; tm_hour
mov eax, offset aHourD ; "Hour: %d\n"
mov [esp+4], edx
mov [esp], eax
call printf
mov edx, [esp+14h] ; tm_min
mov eax, offset aMinutesD ; "Minutes: %d\n"
mov [esp+4], edx
mov [esp], eax
call printf
mov edx, [esp+10h] ; "Seconds: %d\n"
mov eax, offset aSecondsD ; tm_sec
mov [esp+4], edx
mov [esp], eax
call printf
leave
retn
endp
```

可能是IDA未能在局部范围内将这些局部变量逐一识别出来，因此标记的别名。但是读到这里的读者都是有经验的逆向工程分析人员了，不需要辅助信息仍然可以分析数据的作用。

需要注意的是“lea edx, [eax+76Ch]”指令。它给AX寄存器的值加上0x7C (1900)，而不会修改任何状态位。对于LEA指令的更多信息，请参阅附录A.6.2。

GDB

我们使用GDB调试这个程序，可以得到如下所示的代码。[4]

指令清单21.7 GDB