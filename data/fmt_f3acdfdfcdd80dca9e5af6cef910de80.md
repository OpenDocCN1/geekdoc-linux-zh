
# sys.c

```c
/*
* sys.c
* 作者: Eric Harlow
* Linux
*/
#include <stdio.h>
#include <string.h>
#include <gtk/gtk.h>
#include "device.h"

#define SEPARATORS ";"

void GetPacketInfo();

/*
* GetPacketInfo
* 获取跨包的信息。
* 信息在 /proc/dev 中，如果机器
* 支持 /proc 系统。
*/
void GetPacketInfo() {
    char *szfilename = "/proc/dev";
    char szBuffer[132];
    int nLineNo = 0;
    FILE *fp;
    char *sToken;
    char *sDevName;
    int nWord;
    long nIncoming;
    long nOutgoing;
    typDevice *dev;

    /* --- 打开文件获取信息 --- */
    fp = fopen(szFilename, "r");
    if (fp) {
        /* --- 有信息可以读 --- */
        while (fgets(szBuffer, sizeof(szBuffer), fp)) {
            nLineNo++;

            /* 读取一行文本 --- */
            fgets(szBuffer, sizeof(szBuffer), fp);

            /* 第3行之后是设备 --- */
            if (nLineNo >= 3) {
                nWord = 0;
                sDevName = NULL;
                sToken = strtok(szBuffer, SEPARATORS);
                while (sToken) {
                    switch (nWord) {
                        case 0:
                            sDevName = sToken;
                            break;
                        case 1:
                            nIncoming = atoi(sToken);
                            break;
                        case 6:
                            nOutgoing = atoi(sToken);
                            break;
                    }
                    nWord++;
                    sToken = strtok(NULL, SEPARATORS);

                    /* --- 得到了名字 --- */
                    if (sDevName) {
                        /* --- 查找它 --- */
                        dev = LookupDevice(sDevName);
                        /* --- 添加/更新它 --- */
                        if (dev) {
                            UpdateExistingDevice(sDevName, (long)nIncoming + nOutgoing));
                        } else {
                            UpdateDevice(sDevName, (long)nIncoming + nOutgoing), DELTA, 1);
                        }
                    }
                }
                szBuffer[0] = (char) 0;
                /* --- 全部完成 --- */
                fclose(fp);
            }
        }
    } else {
        /* --- 呃... 错误！ --- */
        printf("Unable to open file %s.", szFilename);
    }
}

/*
 * GetCPUInfo
 * 读取 /proc/loadavg 文件并解析 cpu 信息。
 */
void GetCPUInfo() {
    static char *szFile = "/proc/loadavg";
    char szBuffer[88];
    FILE *fp;
    float cpu1, cpu2, cpu3;
    long lcpu1, lcpu2, lcpu3;
    typDevice *dev;

    /* --- 打开带有 cpu 信息的文件 --- */
    fp = fopen(szFile, "r");

    /* --- 如果打开了... --- */
    if (fp) {
        fgets(szBuffer, sizeof(szBuffer), fp);

        /* --- 获取 CPU 利用率数字 --- */
        sscanf(fp, "%f %f %f", &cpu1, &cpu2, &cpu3);

        /* --- 想要 1-100+ 的范围而不是 .01 到 1.0+ --- */
        lcpu1 = cpu1 * 100;
        lcpu2 = cpu2 * 100;
        lcpu3 = cpu3 * 100;

        /* --- 查找设备 --- */
        dev = LookupDevice("cpu1");
        if (dev) {
            /* --- 已存在，更新 --- */
            UpdateExistingDevice("cpu1", lcpu1);
        } else {
            /* --- 第一次，创建设备 --- */
            UpdateDevice("cpu1", lcpu1, DELTA, 1);
        }
    }
}
```

## graph.c

所有处理绘制小部件的内容都进入此文件。信息是使用 `sys.c` 中使用的设备发明名称进行查询的。`UpdateDevice` 和 `UpdateExistingDevice` 创建了设备并关联了数值信息。`graph.c` 中的例程通过调用 `device.c` 中的例程来访问信息。由于使用了 `/proc` 文件系统，如果内核发生变化（不太可能），以后更改实现细节（`sys.c`），或者将应用程序移植到不支持 `/proc` 系统的操作系统。

许多例程与更新时钟的例程相似。主要的区别在于“笔”（实际上是绘制中颜色的使用）。当应用程序创建时，会创建几个（实际上是 `GdkGC`），以便以特定的颜色进行绘制。这些笔是预分配的，以加快绘制（否则，每次你想重绘屏幕时都要创建一个新的 `GdkGC`）。笔在 `GetPen` 函数中创建，这使得代码比在 `GetGdkGC` 函数中更具可读性。

```c
void DrawDevice(GtkWidget *drawing_area, char *szName, GdkGC *pen,
    int bAvg);
    int NetworkButtonDown();
    int NetworkAvgButtonDown();
    int CPUButton15Down();
    int CPUButton5Down();
    int CPUButton1Down();
    void Repaint();
```

248 第 10 章 绘图工具包
