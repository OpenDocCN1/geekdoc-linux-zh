```
```
67		case 'a':				All directory entries
68		afig++;
69		continue;
70
71		case 's':				Size in blocks
72		sfig++;
73		statreq++;
74		continue;
75
76		case 'd':				Directory info, not contents
77		dfig++;
78		continue;
79
80		case 'g':				Group name instead of user name
81		gfig++;
82		continue;
83
84		case 'l':				Long listing
85		lfig++;
86		statreq++;
87		continue;
88
89		case 'r':				Reverse sort order
90		rfig = -1;
91		continue;
92
93		case 't':				Sort by time, not name
94		tfig++;
95		statreq++;
96		continue;
97
98		case 'u':				Access time, not modification time
99		ufig++;
100		continue;
101
102		case 'c':				Inode change time, not modification time
103		cfig++;
104		continue;
105
106		case 'i':				Include inode number
107		ifig++;
108		continue;
109
110		case 'f':				Force reading each arg as directory
111		ffig++;
112		continue;
113
114		default:				Ignore unknown option letters
115		continue;
116	}
117	argc--;
118	}
```
```