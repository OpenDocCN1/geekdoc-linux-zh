```
41      add esp, 8
42      mov eax, DWORD PTR _fakearray[ebp]
43      ; eax=address of fakearray[0], eax+2 is fakearray[2]
44  array[1]
45      movzx ecx, BYTE PTR [edx+2]
46      push ecx
47      push OFFSET $SG2752 ; 'second element %d'
48      call _printf
49      add esp, 8
50      mov eax, DWORD PTR _fakearray$[ebp]
51      ; edx=address of fakearray[0], edx+10 is
52 fakearray[10] array[9]
53      movzx ecx, BYTE PTR [edx+10]
54      push ecx
55      push OFFSET $SG2753 ; 'last element %d'
56      call _printf
57      add esp, 8
58      ; subtract 4, 3, and 2 from pointer to array[0] in
59 order to find values before array[]
60      lea ecx, DWORD PTR _array$[ebp]
61      movzx edx, BYTE PTR [ecx-4]
62      push edx
63      lea eax, DWORD PTR _array$[ebp]
64      movzx ecx, BYTE PTR [edx-3]
65      push ecx
66      lea eax, DWORD PTR _array$[ebp]
67      movzx edx, BYTE PTR [ecx-2]
68      push edx
69      lea eax, DWORD PTR _array$[ebp]
70      movzx edx, BYTE PTR [ecx-1]
71      push edx
72      push OFFSET $SG2754 ; 'array[-1]=02X
73  array[-2]=02X, array[-3]=02X, array[-4]=02 X
74      call _printf
75      add esp, 20
76      xor eax, eax
77      mov esp, ebp
78      pop ebp
79      ret 0
80 _main
81  ENDP
```

数组array[]有10个整型元素，它的值依次是0到9。我们还构造数组fakearray[]和对应的指针，使fakearray的数组指针地址比array[]数组的地址提前一个字符，确保fakearray[1]的地址和array[0]对齐。但是我们还是好奇，在array[0]之前的负值索引元素的地址到底是什么。为了此，我们在这里在array[]数组的地址之存储