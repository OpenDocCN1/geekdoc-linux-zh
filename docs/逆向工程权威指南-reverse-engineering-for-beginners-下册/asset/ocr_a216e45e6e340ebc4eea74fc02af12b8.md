```
push    ebp
mov     ebp, esp
sub     esp, 18h
cmp     [ebp+arg_0], 4
ja      short loc_0048444
mov     eax, [ebp+arg_0]
shl     eax, 2
mov     eax, ds:off_004855C[eax]
jmp     eax
```

```
loc_00483FE: : DATA XREF; .rodata.off_004855C "zero"
mov     [esp+18h+var_18], offset aZero
call    _puts
jmp     short locret_0048450
```

```
loc_004840C: : DATA XREF; .rodata.00048560 "one"
mov     [esp+18h+var_18], offset aOne
call    _puts
jmp     short locret_0048450
```

```
loc_004841A: : DATA XREF; .rodata.00048564 "two"
mov     [esp+18h+var_18], offset aTwo
call    _puts
jmp     short locret_0048450
```

```
loc_0048428: : DATA XREF; .rodata.00048568 "three"
mov     [esp+18h+var_18], offset aThree
call    _puts
jmp     short locret_0048450
```

```
loc_0048436: : DATA XREF; .rodata.0004856C "four"
mov     [esp+18h+var_18], offset aFour
call    _puts
jmp     short locret_0048450
```

```
loc_0048444: : CODE XREF; f+4
mov     [esp+18h+var_18], offset aSomethingUnko "something unknown"
call    _puts
```

```
locret_0048450: : CODE XREF; f+26
      ; f+34...
leave
retn
endp
```

```
off_004855C dd offset loc_000483FE ; DATA XREF; f+12
      dd offset loc_0004840C
      dd offset loc_0004841A
      dd offset loc_00048428
      dd offset loc_00048436
```