

```cpp
88                 parent_type_name);
89             }
90     new_sigdesc->left = NULL;
91     new_sigdesc->right = NULL;
92
93     if(sigdesc == NULL) {
94         sigdesc = new_sigdesc;
95     } else {
96         add_sigdesc_to_tree(new_sigdesc,sigdesc);
97     }
98 }
99 static void add_sigdesc_to_tree(SigDesc *new,SigDesc *node)
100 {
101     int cond;
102
103     if((cond = strcmp(new->type_name,
104                     node->type_name)) < 0) {
105         if(node->left == NULL)
106             node->left = new;
107         else
108             add_sigdesc_to_tree(new,node->left);
109     } else if(cond > 0) {
110         if(node->right == NULL)
111             node->right = new;
112         else
113             add_sigdesc_to_tree(new,node->right);
114     } else if((cond = strcmp(new->signal_name,
115                     node->signal_name)) < 0) {
116         if(node->left == NULL)
117             node->left = new;
118         else
119             add_sigdesc_to_tree(new,node->left);
120     } else if(cond > 0) {
121         if(node->right == NULL)
122             node->right = new;
123         else
124             add_sigdesc_to_tree(new,node->right);
125     }
126 }
127 static void print_signals(SigDesc *sd,FILE *file)
128 {
129     int i;
130     int j;
131     gchar string[256];
132
133     if(sd != NULL) {
134         print_signals(sd->left,file);
135         if(strcmp(last_name_printed,sd->type_name)) {
136             fprintf(file,"\n%5s (~%s)\n",
137                     sd->type_name,sd->parent_type_name);
138             strcpy(last_name_printed,sd->type_name);
139         }
140         sprintf(string, " %s\n%s", 
141         sd->signal_name, sd->fn);
142         if(strlen(string) > 63) {
143             for(i=63; i>0; i--) {
144                 if(string[i] == '.') {
145                     for(j = strlen(string); j > i; j--)
146                         string[j+9] = string[j];
147                     string[i+1] = '\n';
148                     for(j=2; j<i; j++)
149                         string[j+i] = ' ';
150                     break;
151                 }
152             }
153         }
154         }
155         fprintf(file, "%s\n", string);
156         print_signals(sd->right, file);
157     }
158 }
159 static gchar *inheritance(GtkType type)
160 {
161     GtkType parent_type;
162     gchar *parent_type_name;
163     static gchar string[256];
164
165     string[0] = '\0';
166     while(1) {
167         parent_type = gtk_type_parent(type);
168         parent_type_name = gtk_type_name(parent_type);
169         if(parent_type_name == NULL)
170             break;
171         if(strlen(string) > 1) {
172             strcat(string, "->");
173             strcat(string, parent_type_name);
174         } else {
175             strcpy(string, parent_type_name);
176         }
177         type = parent_type;
178     }
179     if(strlen(string) > 1)
180         return(string);
181     return("none");
182 }
```

第 35 行开始的 `main()` 函数通常像任何 GNOME 应用程序一样调用 `gnome_init()`，以初始化 GNOME 和 GTK+。接下来，它调用 `widget_list()` 通过创建对象实例来初始化信号信息。调用 `signames()` 函数以生成输出。在第 25 行的 `signames()` 函数中，调用 `load_signals()` 以检索信号信息并将其存储到一个排序列表中。最后，调用 `print_signals()` 将排序列表中的信号信息写入标准输出。

通过在 `widget_list()` 函数（第 30 行）中添加或移除控件创建调用，您可以添加或移除输出列表中包括的控件。在此示例中，有两个调用：一个用于创建按钮控件，另一个用于创建日历控件。没有必要保存返回的控件，因为只需要类自行初始化，从而使回调列表在内部表中得到定义。

> 该程序旨在作为独立程序运行，但经过简单修改，它可以编译并链接以在您的应用程序内部运行。为此，请删除 `main()` 和 `widget_list()` 函数，然后将其编译并与您的程序链接。在应用程序进入主循环之前——在创建完所有对象之后——添加代码以打开文件并调用 `signames()` 输出回调信息。例如：

```
FILE *file;
file = fopen("cbfile", "w");
signames(file);
fclose(file);
gtk_main();
```

第 42 行开始的 `load_signals()` 函数从内部表中读取信号和回调信息。每个新信号都被分配一个 ID 号，第一个为 1，第二个为 2，依此类推。这意味着从第 53 行开始的循环将通过从数字 1 开始并增加循环直到找到一个未分配的 ID 号来获取所有信号。循环顶部的 `gtk_signal_query()` 调用返回包含关于回调信息的 `GtkSignalQuery` 结构体。

`GtkSignalQuery` 结构中有很多可用信息。第 54 行对 `gtk_type_name()` 的调用使用对象类型 ID 来获取对象名称。第 55 行对 `gtk_type_name()` 的调用获取回调函数返回值的类型名称。在第 56 行，对 `inheritance()` 的调用返回一个字符串，其中包含一直到 `GObject` 的继承对象列表。

第 159 行开始的 `inheritance()` 函数遍历对象的父级链接以确定其整个谱系。对象类型作为参数传入，并用作遍历的起点。第 167 行对 `gtk_type_parent()` 的调用返回父对象的类型 ID，第 168 行对 `gtk_type_name()` 的调用获取其名称。随着每个名称被获取，它被添加到代表整个谱系的名称字符串中。

第 57 行开始构建原型函数调用，通过将返回值和第一个参数打印到字符串中。除了两个默认参数外，如果有其他参数，第 58 至 62 行的循环会将它们添加到字符串中。第 59 行对 `gtk_type_name()` 的调用用于提取每个参数的类型，但缺少一项信息。您无法从 `GtkSignalQuery` 结构体的内容中确定参数是否为指针。此信息确实存在，但保存在 GTK 源文件 `gtksignals.c` 中名为 `G_CK_signals` 的静态数组内部。在不修改 `gtksignals.c` 的情况下，没有办法提取这些信息。随源代码提供了一个此程序的版本（名为 `signames2.c`），其中的注释描述了使其正常工作所需的 GTK 代码更改。

第 68 行开始的函数 `add_siglist()` 为信号创建一个新节点并将其添加到树中。第 74 到 91 行创建节点并填充其值。第 93 到 97 行通过调用 `add_sigdesc_to_tree()` 将其添加到树中。

第 99 行开始的函数 `add_sigdesc_to_tree()` 遍历二叉树并将新成员添加到正确的位置。树首先按发出信号的对象的类型名称排序，然后按信号本身的名称排序。这样，信号就按字母顺序分组并按其对象类型排列。

输出由第 127 行开始的函数 `print_signals()` 生成。它是一个递归例程，期望一个树节点作为参数。它做三件事：向左看，打印当前节点，然后向右看。它通过在第 134 行用左指针调用自身来向左看。打印在第 135 到 153 行进行。在第 135 行，它比较最后打印的对象名称与当前对象名称，并仅在它们不同时打印（这为每组信号创建一个对象名称头）。如果一行太长（在此示例中，64 个字符被认为太长），它会在第 63 个字符左侧的第一个逗号处断开。最后，它通过在第 155 行调用自身向右看。

示例程序的输出如下所示：

```
GnomeClient      (-*GtkObject)
  "connect"     void cb(GtkWidget *,gboolean,gpointer)
  "die"         void cb(GtkWidget *,gpointer)
  "disconnect"  void cb(GtkWidget *,gpointer)
  "save-complete" void cb(GtkWidget *,gpointer)
  "save-yourself" gboolean cb(GtkWidget *,gint,GNom,
                   gboolean,GNom,gboolean,gpointer)
  "shutdown-canceled" void cb(GtkWidget *,gpointer)

GtkButton      (-*GtkBin->GtkContainer->GtkWidget->GtkObject)
  "clicked"     void cb(GtkWidget *,gpointer)
  "enter"       void cb(GtkWidget *,gpointer)
  "leave"       void cb(GtkWidget *,gpointer)
  "pressed"     void cb(GtkWidget *,gpointer)
  "released"    void cb(GtkWidget *,gpointer)

GtkCalendar      (-*GtkWidget->GtkObject)
  "day-selected"  void cb(GtkWidget *,gpointer)
```

