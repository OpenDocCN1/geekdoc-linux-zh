```
37    gnome_init("signames","1.0",argc,argv);  
38    widget_list();  
39    signames(stdout);  
40    exit(0);  
41  
42 static void load_signals()  
43 {  
44    gint i = 0;  
45    gint j;  
46    gchar *type_name;  
47    gchar *parent_type_name;  
48    gchar *return_type_name;  
49    gchar *param_name;  
50    gchar fn[256];  
51    GSignalQuery *q;  
52  
53    while((q = gtk_signal_query(++i) != NULL) {  
54        type_name = gtk_type_name(q->object_type);  
55        return_type_name = gtk_type_name(q->return_val);  
56        parent_type_name = inheritance(q->object_type);  
57        sprintf(fn,"%s cb(GtkWidget *,",return_type_name);  
58        for(j=0; j<q->nparams; j++) {  
59            param_name = gtk_type_name(q->params[j]);  
60            strcat(fn,", ");  
61            strcat(fn,param_name);  
62        }  
63        strcat(fn,", gpointer");  
64        add_siglist(q->signal_name,type_name,  
65                    parent_type_name,fn);  
66    }  
67  
68 static void add_siglist(const gchar *signal_name,  
69                  const gchar *type_name,  
70                  const gchar *parent_type_name,const gchar *fn)  
71 {  
72    SigDesc *new_sigdesc;  
73  
74    new_sigdesc = g_malloc(sizeof(SigDesc));  
75    new_sigdesc->signal_name =  
76        g_malloc(strlen(signal_name)+1);  
77    strcpy(new_sigdesc->signal_name,signal_name);  
78    new_sigdesc->type_name = g_malloc(strlen(type_name)+1);  
79    strcpy(new_sigdesc->type_name,type_name);  
80    new_sigdesc->fn = g_malloc(strlen(fn)+1);  
81    strcpy(new_sigdesc->fn,fn);  
82    if(parent_type_name == NULL) {  
83        new_sigdesc->parent_type_name = NULL;  
84    } else {  
85        new_sigdesc->parent_type_name =  
86            g_malloc(strlen(parent_type_name)+1);  
87    strcpy(new_sigdesc->parent_type_name,
```