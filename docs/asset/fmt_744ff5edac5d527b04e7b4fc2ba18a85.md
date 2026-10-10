
```c
13. GNOME_STOCK_PIXMAP_REVERT,
14. GNOME_STOCK_PIXMAP_SAVE,
15. GNOME_STOCK_PIXMAP_SAVE_AS,
16. GNOME_STOCK_PIXMAP_CUT,
17. GNOME_STOCK_PIXMAP_COPY,
18. GNOME_STOCK_PIXMAP_PASTE,
19. GNOME_STOCK_PIXMAP_CLEAR,
20. GNOME_STOCK_PIXMAP_PROPERTIES,
21. GNOME_STOCK_PIXMAP_PREFERENCES,
22. GNOME_STOCK_PIXMAP_HELP,
23. GNOME_STOCK_PIXMAP_SCORER,
24. GNOME_STOCK_PIXMAP_PRINT,
25. GNOME_STOCK_PIXMAP_SCROLL,
26. GNOME_STOCK_PIXMAP_SEARCH,
27. GNOME_STOCK_PIXMAP_BACK,
28. GNOME_STOCK_PIXMAP_FORWARD,
29. GNOME_STOCK_PIXMAP_FIRST,
30. GNOME_STOCK_PIXMAP_LAST,
31. GNOME_STOCK_PIXMAP_HOME,
32. GNOME_STOCK_PIXMAP_STOP,
33. GNOME_STOCK_PIXMAP_REFRESH,
34. GNOME_STOCK_PIXMAP_UNDO,
35. GNOME_STOCK_PIXMAP_REDO,
36. GNOME_STOCK_PIXMAP_TIMER,
37. GNOME_STOCK_PIXMAP_TIMER_STOP,
38. GNOME_STOCK_PIXMAP_MAIL,
39. GNOME_STOCK_PIXMAP_MAIL_RCV,
40. GNOME_STOCK_PIXMAP_MAIL_SND,
41. GNOME_STOCK_PIXMAP_MAIL_RPL,
42. GNOME_STOCK_PIXMAP_MAIL_FWD,
43. GNOME_STOCK_PIXMAP_MAIL_NEW,
44. GNOME_STOCK_PIXMAP_TRASH,
45. GNOME_STOCK_PIXMAP_TRASH_FULL,
46. GNOME_STOCK_PIXMAP_UNDELETE,
47. GNOME_STOCK_PIXMAP_SPELLCHECK,
48. GNOME_STOCK_PIXMAP_MIC,
49. GNOME_STOCK_PIXMAP_LINE_IN,
50. GNOME_STOCK_PIXMAP_CDROM,
51. GNOME_STOCK_PIXMAP_VOLUME,
52. GNOME_STOCK_PIXMAP_MIDI,
53. GNOME_STOCK_PIXMAP_BOOK_RED,
54. GNOME_STOCK_PIXMAP_BOOK_GREEN,
55. GNOME_STOCK_PIXMAP_BOOK_BLUE,
56. GNOME_STOCK_PIXMAP_BOOK_YELLOW,
57. GNOME_STOCK_PIXMAP_BOOK_OPEN,
58. GNOME_STOCK_PIXMAP_ABOUT,
59. GNOME_STOCK_PIXMAP_QUIT,
60. GNOME_STOCK_PIXMAP_MULTIPLE,
61. GNOME_STOCK_PIXMAP_NOT,
62. GNOME_STOCK_PIXMAP_CONVERT,
63. GNOME_STOCK_PIXMAP_JUMP_TO,
64. GNOME_STOCK_PIXMAP_UP,
65. GNOME_STOCK_PIXMAP_DOWN,
66. GNOME_STOCK_PIXMAP_TOP,
67. GNOME_STOCK_PIXMAP_BOTTOM,
68. GNOME_STOCK_PIXMAP_ATTACH,
69. GNOME_STOCK_PIXMAP_INDEX,
70. GNOME_STOCK_PIXMAP_FONT,
71. GNOME_STOCK_PIXMAP_EXEC,
72. GNOME_STOCK_PIXMAP_ALIGN_LEFT,
73. GNOME_STOCK_PIXMAP_ALIGN_RIGHT,
74. GNOME_STOCK_PIXMAP_ALIGN_CENTER,
75. GNOME_STOCK_PIXMAP_ALIGN_JUSTIFY,
76. GNOME_STOCK_PIXMAP_TEXT_BOLD,
77. GNOME_STOCK_PIXMAP_TEXT_ITALIC,
78. GNOME_STOCK_PIXMAP_TEXT_UNDERLINE,
79. GNOME_STOCK_PIXMAP_TEXT_STRIKEOUT,
80. GNOME_STOCK_PIXMAP_TEXT_INDENT,
81. GNOME_STOCK_PIXMAP_TEXT_UNINDENT,
82. GNOME_STOCK_PIXMAP_EXIT,
83. GNOME_STOCK_PIXMAP_COLORSELECTOR,
84. GNOME_STOCK_PIXMAP_ADD,
85. GNOME_STOCK_PIXMAP_REMOVE,
86. GNOME_STOCK_PIXMAP_TABLE_BORDERS,
87. GNOME_STOCK_PIXMAP_TABLE_FILL,
88. GNOME_STOCK_PIXMAP_TEXT_BULLETED_LIST,
89. GNOME_STOCK_PIXMAP_TEXT_NUMBERED_LIST
90};

static GnomeUIInfo iconInfo = {
  GNOME_APP_UI_ITEM, NULL, NULL, NULL, NULL, NULL,
  GNOME_APP_PIXMAP_STOCK, NULL, 0, 0, NULL
};
static GnomeUIInfo endInfo = GNOMEUIINFO_END;
static GnomeUIInfo toolbarInfo[10];

int main(int argc, char *argv[]) 
{
 int s;
 int t;
 int count;
 int total_size;
 GtkWidget *app;

 gnome_init ("showstock", "1.0", argc, argv);
 app = gnome_app_new ("showstock",
 "Gnome Stock Icons");
 gtk_signal_connect (GTK_OBJECT (app), "delete_event", 
 GTK_SIGNAL_FUNC (eventDelete), NULL);
       gtk_signal_connect(GTK_OBJECT(app),"destroy", 
                             GTK_SIGNAL_FUNC(eventDestroy),NULL);
   
       total_size = sizeof(stock)/sizeof(gchar *);
       s = 0;
       while(s < total_size) {
           for(t=0, count=0; count<9; t++, count++) {
               memcpy(&toolBarInfo[t],
                          &iconInfo[s],sizeof(iconInfo));
               toolBarInfo[t].label = stock[s];
               toolBarInfo[t].pixmap_info = stock[5];
               memcpy(&toolBarInfo[t+1],
                          &endInfo,sizeof(endInfo));
           if(strlen(stock[s]) > 12)
               count++;
           if(++s >= total_size)
               break;
       }
       gnome_app_create_toolbar(GNOME_APP(app),
                              toolBarInfo);
       gtk_widget_show_all(app);
   }
   
       gtk_main();
       exit(0);
   }
   gint eventDelete(GtkWidget *widget,
                       GdkEvent *event,gpointer data) {
       return(FALSE);
   }
   gint eventDestroy(GtkWidget *widget,
                       GdkEvent *event,gpointer data) {
       gtk_main_quit();
       return(0);
   }
```

数组中第 9 行开始的字符串字符串标识每个图标。GNOME 头文件 `gnome-stock.h` 包含定义每个命名图标的字符串字符。您可以直接插入引号括起来的字符串，但这会阻止编译器检测拼写错误。名称的定义如下所示：

```c
```
