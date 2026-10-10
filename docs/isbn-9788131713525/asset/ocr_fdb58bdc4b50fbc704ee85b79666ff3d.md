# 5.3 Kernel Command Line Processing

What we have left after simplification is the heart of the mechanism. First, the compiler generates an array of characters called `__setup_str_console_setup[]` initialized to contain the string console=. Next, the compiler generates a structure that contains three members: a pointer to the kernel command line string (the array just declared), the pointer to the setup function itself, and a simple flag. The key to the magic here is the section attribute attached to the structure. This attribute instructs the compiler to emit this structure into a special section within the ELF object module, called .init.setup. During the link stage, all the structures defined using the __setup macro are collected and placed into this .init.setup section, in effect creating an array of these structures. Listing 5-6, a snippet from .../init/main.c, shows how this data is accessed and used.

# Listing 5-6
Kernel Command Line Processing

```
1 extern struct obs_kernel_param __setup_start[], __setup_end[];
2
3 static int __init obsolete_checksetup(char *line)
4 {
5 struct obs_kernel_param *p;
6
7 p = __setup_start;
8 do {
9 int n = strlen(p->str);
10 if (!strncmp(line, p->str, n)) {
11 if (p->early) {
/* Already done in parse_early_param?
11 (Needs */
13 /* exact match on param part) */
14 if (line[n] == '\0' || line[n] == '=' )
15 return 1;
16 } else if (!p->setup_func) {
17 printk(KERN_WARNING "Parameter %s is
18 obsolete, */
19 " ignored\n", p->str);
20 return 1;
21 } else if (p->setup_func(line + n))
22 return 1;
23 }
24 p++;
25 } while (p < __setup_end);
26 return 0;
27 )
```