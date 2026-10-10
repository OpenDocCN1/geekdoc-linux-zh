```
76 joinStyleString(gcv.line_style);
77 }
78 return(TRUE);
79 }
80 static char *functionString(GdkFunction function)
81 {
82 switch(function) {
83 case GDK_COPY: return("copy");
84 case GDK_INVERT: return("invert");
85 case GDK_XOR: return("and invert");
86 case GDK_CLEAR: return("clear");
87 case GDK_AND: return("and");
88 case GDK_AND_REVERSE: return("and reverse");
89 case GDK_AND_INVERT: return("and invert");
90 case GDK_NOOP: return("noop");
91 case GDK_OR: return("or");
92 case GDK_EQUIV: return("equiv");
93 case GDK_OR_REVERSE: return("or reverse");
94 case GDK_COPY_INVERT: return("copy invert");
95 case GDK_OR_INVERT: return("or invert");
96 case GDK_NAND: return("nand");
97 case GDK_SET: return("set");
98 default: return("");
99 }
100 }
101 static char *fillString(GdkFill fill)
102 {
103 switch(fill) {
104 case GDK_SOLID: return("solid");
105 case GDK_TILED: return("tiled");
106 case GDK_STIPPLED: return("stippled");
107 case GDK_OPAQUE_STIPPLED: return("opaque stippled");
108 default: return("");
109 }
110 }
111 static char *subwindowString(GdkSubWindowMode mode)
112 {
113 if(mode == GDK_CLIP_BY_CHILDREN)
114 return("clip by children");
115 else if(mode == GDK_INCLUDE_INFERIORS)
116 return("include inferiors");
117 return("");
118 }
119 static char *lineStyleString(gint style)
120 {
121 switch(style) {
122 case GDK_LINE_SOLID: return("solid");
123 case GDK_LINE_ON_OFF_DASH: return("on off dash");
124 case GDK_LINE_DOUBLE_DASH: return("double dash");
125 default: return("");
126 }
127 }
128 static char *capStyleString(gint style)
```