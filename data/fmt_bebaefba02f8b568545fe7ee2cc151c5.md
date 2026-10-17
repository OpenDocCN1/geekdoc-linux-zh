
```cpp
void dump_tree_node (struct tree_node *n, bool is_set, bool
    traverse, bool dump_keys_and_values)
{
    printf("0x%p left=0x%p parent=0x%p right=0x%p color=%d\n",
        n, n->left, n->parent, n->right, n->M_color);

    void *point_after_struct=((char*)n)+sizeof(struct tree_node);
    if (is_set)
    {
        printf("key=%d\n", (int*)point_after_struct);
    }
    else
    {
        struct map_pair *p=(struct map_pair*)point_after_struct;
        printf("key=%d, value=%s\n", p->key, p->value);
    }
    if (traverse==false)
        return;
    if (n->left)
        dump_tree_node(n->left, is_set, traverse, dump_keys_and_values);
    if (n->right)
        dump_tree_node(n->right, is_set, traverse, dump_keys_and_values);
}

void dump_map_and_set(struct tree_struct *m, bool is_set)
{
    printf("ptr=0x%p, M_key_compare=0x%p, M_header=0x%p, M_node_count=%d\n",
        m, m->M_key_compare, &m->M_header, m->M_node_count);
    if (is_set)
    {
        printf("As a tree:\n");
        printf("root---%d\n", m->M_header.M_color); // 注意：此处 OCR 逻辑似乎有误，保留结构
        dump_as_tree(1, m->M_header.M_parent, is_set);
    }
}

void dump_as_tree(int first, struct tree_node n, bool is_set)
{
    if (n.Isnil)
        return;
    if (first)
        printf("root---%d\n", n.M_color); // 基于 OCR 的占位逻辑
    // ... 这部分代码在 OCR 中片段化
}

int main()
{
    // map
    std::map<int, const char*> m;

    m[10]="ten";
    m[20]="twenty";
    m[3]="three";
    m[101]="one hundred one";
    m[100]="one hundred";
    m[12]="twelve";
    m[107]="hundred seven";
    m[0]="zero";
    m[1]="one";
    m[6]="six";
    m[99]="ninety-nine";
    m[5]="five";
    m[11]="eleven";
    m[1001]="one thousand one";
    m[1010]="one thousand ten";
    m[2]="two";
    m[9]="nine";

    printf("dumping m as map:\n");
    dump_map_and_set((struct tree_struct *) &m, false);

    std::map<int, const char*>::iterator it1=m.begin();
    printf("m.begin():\n");
    dump_tree_node((struct tree_node*) (void*)&it1, false, false, true);
    it1=m.end();
    printf("m.end():\n");
    dump_tree_node((struct tree_node*) (void*)&it1, false, false, false);

    // set
    std::set<int> s;
    s.insert(123);
    s.insert(456);
    s.insert(11);
    s.insert(12);
    s.insert(100);
    s.insert(1001);
    printf("dumping s as set:\n");
    dump_map_and_set((struct tree_struct*) &s, true);
    std::set<int>::iterator it2=s.begin();
    printf("s.begin():\n");
    dump_tree_node((struct tree_node*) (void*)&it2, true, false, true);
    it2=s.end();
    printf("s.end():\n");
    dump_tree_node((struct tree_node*) (void*)&it2, true, false, false);
}
```
