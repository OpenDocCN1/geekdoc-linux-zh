# GVSTIMER
select inst_id,ksutmtm from x$ksutm

不过kqftab/kqftab表没有用引用生成这项数值的函数。

# 指令清单81.12 Result of oracle tables

```
kqftab_element.name: [X$KSUTM] ?: [ksutm] 0x1 0x0 0x0 0x4 0x0
0xffffc09b 0x3
kqftab_param.name=[ADDR] ?: 0x01917 0x0 0x0 0x4 0x0
kqftab_param.name=[INDX] ?: 0x20b02 0x0 0x0 0x0 0x4 0x0
kqftab_param.name=[INST_ID] ?: 0x0b2 0x0 0x0 0x0 0x4 0x0
kqftab_param.name=[KSUTM] ?: 0x1302 0x0 0x0 0x0 0x4 0x0 0x1e0le
kqftap_element.fn1=NULL
kqftap_element.fn2=NULL
```

当我们搜索字符串KSUTMTIM时，我们看到了下列函数：

```
kqfd_DRN_ksutm_c proc near      ; DATA XREF:
rodata:0805B4E8

arg_0               = dword ptr       8
arg_8               = dword ptr       10h
arg_C               = dword ptr       14h

push                 ebp
mov                  ebp, esp
push                 [ebp+arg_C]
push                 offset ksugtm
push                 offset 2__STRING_1263_0 ;

"KSUTMTIM"
push                 [ebp+arg_8]
push                 [ebp+arg_0]
call                 kqfd_cfui_drain
add                  esp, 14h
mov                  esp, ebp
pop                  ebp
retn
kqfd_DRN_ksutm_c endp
```

而数据表kqfd_tab_registry_0引用了kqfd_DRN_ksutm_c()函数：

```
dd offset 2__STRING_62_0 ;"X$KSUTM"
dd offset kqfd OPN_ksutm_c
dd offset kqfd_tabl_fetch
```