```
m, m->M_key_compare, &m->M_header, m->M_node_count;
dump_tree_node(m->M_header.M_parent, is_set, true, true);
printf("As a tree:\n");
printf("root--");
dump_as_tree(1, m->M_header.M_parent, is_set);
};
```

```
int main()
{
```

```
// map
```

```
std::map<int, const char*> m;
```

```
m[10]="ten"
m[20]="twenty"
m[3]="three"
m[101]="one hundred one"
m[100]="one hundred"
m[12]="twelve"
m[107]="one hundred seven"
m[0]="zero"
m[1]="one"
m[6]="six"
m[99]="ninety-nine"
m[5]="five"
m[11]="eleven"
m[1001]="one thousand one"
m[1010]="one thousand ten"
m[2]="two"
m[9]="nine";
```

```
printf("dumping m as map:\n");
dump_map_and_set((struct tree_struct *) (void*)&m, false);
```

```
std::map<int, const char*>::iterator it1=m.begin();
printf("m.begin():\n");
dump_tree_node((struct tree_node*) (void**)&itl, false,
false, true);
itl=m.end();
printf("m.end():\n");
dump_tree_node((struct tree_node*) (void**)&itl, false,
false, false);
```

```
// set
```

```
std::set<int> s;
s.insert(123);
s.insert(456);
```