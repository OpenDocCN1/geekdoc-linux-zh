```
s.insert(11);
s.insert(12);
s.insert(100);
s.insert(1001);
printf("dumping s as set:\n");
dump_map_and_set((struct tree_struct*) (void*)&s, true);
std::set<int>::iterator it2=s.begin();
printf("s.begin():\n");
dump_tree_node((struct tree_node*) (void**)&it2, true,
false, true);
it2=s.end();
printf("s.end():\n");
dump_tree_node((struct tree_node*) (void**)&it2, true,
false, false);
n};
```

# 指令清单51.36 GCC 4.8.1

```
dumping m as map:
ptr=0x0028FE3C, M_key_compare=0x402b70, M_header=0x0028FE40,
M_node_count=17
ptr=0x007A4988 M_left=0x007A4C00 M_parent=0x0028FE40
M_right=0x007A4B80 M_color=1
key=10 value=[ten]
ptr=0x007A4C00 M_left=0x007A4ABE0 M_parent=0x007A49988
M_right=0x007A4C60 M_color=1
key=1 value=[one]
ptr=0x007A4BE0 M_left=0x00000000 M_parent=0x007A4C00
M_right=0x00000000 M_color=1
key=0 value=[zero]
ptr=0x007A4C60 M_left=0x007A4B40 M_parent=0x007A4C00
M_right=0x007A4C20 M_color=0
key=5 value=[five]
ptr=0x007A4B40 M_left=0x007A4CEE0 M_parent=0x007A4C60
M_right=0x00000000 M_color=1
key=3 value=[three]
ptr=0x007A4CE0 M_left=0x00000000 M_parent=0x007A4B40
M_right=0x00000000 M_color=0
key=2 value=[two]
ptr=0x007A4C20 M_left=0x00000000 M_parent=0x007A4C60
M_right=0x007A4D00 M_color=1
key=6 value=[six]
ptr=0x007A4D00 M_left=0x00000000 M_parent=0x007A4C20
M_right=0x00000000 M_color=0
key=9 value=[nine]
ptr=0x007A4B80 M_left=0x007A49A8 M_parent=0x007A4988
M_right=0x007A4BC0 M_color=1
key=100 value=[one hundred]
```