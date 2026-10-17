
```
speed 38400; rows 25; columns 80; line = =

intr = '^C'; erase = '^E'; kill = '^K'; uof = '^D'; eol = '^<>';neol2 = '^<>'; start = '^'; stop = '^'; susp = '^S'; prnt = '^R'; werase = '^W';

next = '\'; flush =; min = 1; time = =

pareb -parend cs hld -cstopbd -local -crtscrcts

ignbrk -brkit -ignpau -parmark -inpck -instip -ignor -lncrnl ixof

iulcl -ixany -imaxbel

opost -olucn -ocrml -onlrl -onflret -ofisl -offl nl n0 cr tab bs vt ff

isigan iocten echo echoch -echol -noflsh -xcase -topost -echoprt

eochtl echoke *
```

# 第 17 章 理解 Linux Shell

注意，在此系统上，中断键（`intr`）被定义为 `<Ctrl-c>`（显示为 `C`），`kill` 键为 `<Ctrl-u>`。虽然你可以设置这里列出的所有内容，但从实践考虑，用户通常会重置中断和 `kill` 键。例如，如果你想将 `kill` 键从 `u` 改为 `C`：

```
stty kill 'C'
```
