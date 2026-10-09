```
```c
struct pathlist_node {
  struct pathlist_node *c_next;
  char c_name[1];  /** flexible array */
};
```
```

```
```c
static bool push_pathlist(struct pathlist_node **head, const char *name)
{
  struct pathlist_node *p;

  ec_null( p = malloc(sizeof(struct pathlist_node) + strlen(name)) )
  strcpy(p->c_name, name);
  p->c_next = *head;
  *head = p;
  return true;

EC_CLEANUP_BGN
  return false;
EC_CLEANUP_END
}
```
```

The size of each `pathlist_node` is variable; the structure has enough space for the NUL byte that terminates the string, and, when allocating a node, we have to add to this space for the name, which can be seen in the argument to `malloc`. Note that we put each node at the head of the list to keep the list in reverse order of when we encountered each node. That’s exactly the order in which we want to assemble the components of the path, as shown by the function `get_pathlist`:

```
```c
static char *get_pathlist(struct pathlist_node *head)
{
  struct pathlist_node *p;
  char *path;
  size_t total = 0;

  for (p = head; p != NULL; p = p->c_next)
    total += strlen(p->c_name) + 1;
  ec_null( path = malloc(total + 1) )
  path[0] = '\0';
  for (p = head; p != NULL; p = p->c_next) {
    strcat(path, "/");
    strcat(path, p->c_name);
  }

  return path;

EC_CLEANUP_BGN
  return NULL;
EC_CLEANUP_END
}
```
```