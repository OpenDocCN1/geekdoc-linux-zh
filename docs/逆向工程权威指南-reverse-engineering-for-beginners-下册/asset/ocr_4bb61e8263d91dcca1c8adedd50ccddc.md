```
int main()
{
    // map

    std::map<int, const char*> m;

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
    m[1001]="one thousand"
    m[1010]="one thousand ten"
    m[2]="two"
    m[9]="nine"
    printf("dumping m as map:\n")
    dump_map_and_set((struct tree_node*)(void**)&m, false);

    std::map<int, const char*>::iterator itl1=m.begin();
    printf("m.begin():\n")
    dump_tree_node((struct tree_node*)(void**)&itl1, false, false);
    itl1=m.end();
    printf("m.end():\n")
    dump_tree_node((struct tree_node*)(void**)&itl1, false, false);

    std::set<int> s;
    s.insert(123);
    s.insert(456);
    s.insert(11);
    s.insert(12);
    s.insert(100);
    s.insert(1001);
    printf("dumping s as set:\n")
    dump_map_and_set((struct tree_node*)(void**)&s, true);
    std::set<int>::iterator it2=s.begin();
    printf("s.begin():\n")
    dump_tree_node((struct tree_node*)(void**)&it2, true, false);
    it2=s.end();
    printf("s.end():\n")
    dump_tree_node((struct tree_node*)(void**)&it2, true, false);
}
}
```

指令清单51.35 MSVC 2012