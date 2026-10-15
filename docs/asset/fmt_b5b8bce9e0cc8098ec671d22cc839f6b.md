
```c
1 #include <stdio.h>               /* 用于 printf, fprintf */
2 #include <string.h>      /* 用于 strcpy */
3 #include <ctype.h>        /* 用于 isdigit */
4 #include <fcntl.h>         /* 用于 O_RDONLY */
5 #include <dirent.h>    /* 用于 getents */
6 #include <sys/stat.h>       /* 用于 stat */
7 #include <sys/types.h>      /* 用于 types */
8 #include <time.h>               /* 用于 localtime, asctime */
9

10

11 /* define 语句 */
12 #define MAX_FILES           100
13 #define MAX_FILENAME        50
14 #define NOT_FOUND           -1
15 #define FOREVER             -1
16 #define DEFAULT_DELAY_TIME  10
17 #define DEFAULT_LOOP_COUNT FOREVER
18

19

20 /* * 布尔值 */
21 enum { FALSE, TRUE };
22

23

24 /* * 状态结构，每个文件一个。 */
25 struct statStruct
26 {
27     char fileName[MAX_FILENAME]; /* 文件名 */
28     int lastCycle, thisCycle; /* 用于变化 */
29     struct stat status; /* 来自 stat() 的信息 */
30};
31;
32

33 /* 全局变量 */
34     char* fileNames[MAX_FILES]; /* 每个命令行一个文件 */
35     int fileCount; /* 命令行文件数量 */
36     struct statStruct stats[MAX_FILES]; /* 每个匹配一个文件 */
37     int loopCount = DEFAULT_LOOP_COUNT; /* 循环次数 */
38     int delayTime = DEFAULT_DELAY_TIME; /* 循环之间的秒数 */
39

40 ***************************************
41

42 main (int argc, char *argv) {
43

44     int argc = argc;
45     char* argv[] = argv;

47 {
48 parseCommandLine(argc, argv); /* 解析命令行 */
49 monitorLoop(); /* 执行主循环 */
50 return (* EXIT_SUCCESS);
51 }
```

```c
95		case 'l':
96		loopCount = getNumber (str, &j);
97		break;
98		}
99	}
100		}
101	/**********************************************************************
104	getNumber (str, i)
106	char* str;
107	int* i;
109	/* 将数字 ASCII 选项转换为数字 */
112	int number = 0;
113	int digits = 0; /* 统计数字中的位数 */
115	while (isdigit (str[+i] + 1])) /** 将字符转换为整数 */
118	++digits;
121	if (digits == 0) usageError (); /* 必须有一个数字 */
122	return (number);
125	/**********************************************************************
127	usageError ()
130	printf (stderr, "Usage: monitor -t<seconds> -l<loops> <filename>\n");
131	exit (EXIT_FAILURE);
}
134	/**********************************************************************
136	monitorLoop ()
138	/* 主监控循环 */
141	do
monitorFiles (); /* * 扫描所有文件 */
flush(stdout); /* * 刷新标准输出 */
flush(stderr); /* * 刷新标准错误 */
sleep (deltaTime); /* * 等待下一次循环 */
} while (loopCount == FOREVER || --loopCount > 0);
}
/********************************************************************************/
monitorFiles () {
    /* 处理所有文件 */
    int i;

    for (i = 0; i < fileCount; i++)
        monitorFile(fileName[i]);

    for (i = 0; i < MAX_FILES; i++) /* * 更新 stat 数组 */
    {
        if (stats[i].lastCycle && stats[i].thisCycle)
            printf("DELETED %s\n", stats[i].fileName);
        stats[i].lastCycle = stats[i].thisCycle;
        stats[i].thisCycle = FALSE;
    }
}
/********************************************************************************
monitorFile(fileName) {
    char* fileName;
    /* 处理单个文件/目录 */
{
        struct stat statBuf;
        mode_t mode;
        int result;

        result = stat(fileName, &statBuf); /* * 获取文件状态 */
        if (result == -1) /* * 状态不可用 */
        {
            fprintf(stderr, "Cannot stat %s\n", fileName);
            return;
        }
```
