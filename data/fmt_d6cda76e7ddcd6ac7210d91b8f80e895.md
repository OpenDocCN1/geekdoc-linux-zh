
# 录 B：监控软件的 C 语言编程

以下代码片段处理状态文本读取与通道值设置：

```c
Trim(value, strlen(value));

if (strcmp(value, StatText)==0)
{
    ChanValue = i;
    printf("Readed channel value: %f\n", ChanValue);
    break;
}

if (ChanValue == -1)
{
    printf("Unknown status text!\n");
    printf("Sorry, the channel can not be written!\n");
    printf("Please type in a correct status text!\n");
    return;
}

/* 用户输入了数值，这很简单： */
printf("Please wait...\n");
```

```c
iResult = SetChannelValue(ChanHandle, DevHandle, ChanValue);

if (iResult==0)
{
    printf("Ok, channel: %d was written!\n", ChanHandle);
    fprintf(out_file_res, "Error, channel: %d was written!\n", ChanHandle); // 写入文件
    fprintf(out_file, "%15s", TextValue); // 写入文件
}
else
{
    printf("Error, channel was not written! Error code=%d", iResult);
    fprintf(out_file_res, "Error, channel was not written: Error code=%d", iResult);
    check=100;
}

fclose(out_file_res);
fclose(in_file);
```

## 函数：`DoStartDetection`

**描述**：开始设备检测（查找所有设备）  
**参数**：（无）  
**返回值**：（无）

```c
void DoStartDetection()
{
    int iErrorCode;
    int DevCnt;
    FILE *out_file;

    printf("Count of devices to search: ");
    scanf("%d", &DevCnt);

    printf("Searching, please wait...\n");

    /* 执行主命令并 yasiddoMasterCmdx("detect", DevCnt,0,0);) */
    iErrorCode = yasiddoMasterCmdx("detect", DevCnt,0,0);

    if (iErrorCode < 0)
    {
        printf("Sorry, but I have found less than %d devices... (please don't beat me)\n", DevCnt);
        out_file=fopen("status_connect_status.txt", "w");
        if(out_file!=NULL)
            fprintf(out_file, "I have found less than %d devices... (please don't beat me)\n", DevCnt);
    }
    else
    {
        printf(" I have found at least %d devices:\n", DevCnt);
        out_file=fopen("status_connect_status.txt", "w");
        if(out_file!=NULL)
            fprintf(out_file, "Ok, I have found %d devices:\n", DevCnt);
        else
            printf(" Failed to open the file \n"); // 测试
    }

    fclose(out_file);
    PrintList();
}
```

## 函数：`DoCommands`

**描述**：解释命令...  
**参数**：（无）  
**返回值**：（无）

```c
void DoCommands(int DetectCheck)
{
    FILE *out_file, *in_file;
    char Cmd,begin[25],Restart[25],
    command[]=begin,command2[]="restart", Device[5];

    int res;
    DWORD DevHandle;
    DWORD DevHandles[10];
    int DevHandles; // 注意参数
    DWORD i;
    DWORD DevCount=0;
    bool bend= false;

    struct block {
        time_t timer;
        int one_minute=0;
        static DWORD DevSet, HandleSet[10];
        char NameBuffer[200];
    };

    /* 获取所有设备句柄...（最多10个）*/
    DevCount = GetDeviceHandles(DevHandles, 10);
    DevSet = DevCount; // 静态

    for(i=0;i<DevCount;i++)
    {
        HandleSet[i] = DevHandles[i]; // 静态
        /* 获取此设备的名称 */
        GetDeviceName(DevHandles[i], NameBuffer, 200);
        printf("%d | %s\n", DevHandles[i], NameBuffer);
    }

    printf("---\n");
    printf("\n");

    while (!bend)
    {
        if (DetectCheck) // 检查是否连接
        {
            start:
            Cmd = '?'; // 安全起见，不应发生
            out_file=fopen("wait.txt", "r");
            if(out_file==NULL)
            {
                fgets(begin, 20, out_file); // 开始参数
            }
            else
                printf("Failed to open the file \n");
            fclose(out_file);

            out_file=fopen("restart.txt", "r");
            if(out_file==NULL)
            {
                fgets(Restart, 20, out_file); // 重启模块
            }
            else
                printf(" Failed to open the file \n");
            fclose(out_file);
        }
    }

    res=strcmp(begin, command); // 设置参数，比较
    res2=strcmp(Restart,command2); // 重启？
    if(res2==0)
    {
        int main(int argc
```

```c
for(i=0;i<DevCount;i++){
    PrintChannelValues(HandleSet[i], DevCount); // 仅通道
}
break;
```

```c
case 's':
    SetParamValue(); // 设置参数后在网页上打印新数据
    in_file=fopen("device.txt","r"); // 从设备读取
    if(in_file!=NULL)
    {
        fgets(Device, 5, in_file);
    }
    else
        printf(" Failed to open the file \n");
    fclose(in_file);
    sscanf(Device,"%ld", &DevHandle); // 复制到设备并转换为整数
    DevCount = GetDevHandles(DevHandles, 10);
    PrintChannelValues(DevHandle, DevCount); // 所有通道
    out_file=fopen("status.txt","w"); // 表示完成所有参数设置
    fprintf(out_file,"555555555555"); // 参数
    fclose(out_file);
    break;
```

```c
case 'r':
    yasdiReset();
    break;
```

```c
case 'q':
    bEnd = true;
    break;
```

```c
case 'x':
    DoMasterCmd("shutdown");
    //bEnd = true;
    break;
```

```c
case '?':
default:
    printf("Commands:\n");
    printf(" ? => 此列表...\n");
    printf(" s => 连接设备计数\n");
    printf(" d => 打印设备列表\n");
    printf(" a => 显示通道值\n");
    printf(" p => 显示参数通道值\n");
    // printf(" t => 显示通道值\n");
    printf(" s => 写参数\n");
    printf(" r => 重置\n");
    printf(" h => 停止/启动 <0|1>\n");
    printf(" x => 关闭\n");
    printf(" q => 退出\n");
    break;
```

## 函数：`main`

**描述**：这是启动（"main"）  
**参数**：（无）  
**返回值**：（无）

```c
int main (int argc, char *argv) {
    FILE *in_file;
    DWORD i;
    DWORD dDriverNum;
    DWORD Driver[10]; // 最多10个使用的驱动程序（COM端口?")
    char DriverName[30], DeviceCount[5];
    char InFile[50]="ini.ini";

    int iErrorCode;
    int DevCnt=0, DetectCheck=0;

    FILE *out_file;
    if (argv[2]==2) {
        strcpy(InFile,argv[1]);
    }
    printf("*******************************************************\n");
    printf("YASDI-Common-Shell-UI (Operating System: %s \n", os_GetSIIdentifier());
    printf("*******************************************************\n");

    /* 初始化 Yasidi 和 Yasidi-Master-Library */
    yasdiInitialize(InFile, &dDriverNum);

    /* 获取所有支持的驱动程序列表... */
    dDriverNum = yasdiGetDriver(Driver, 10);

    /* 将所有驱动程序在线（你只需要切换其中一个！）*/
    for(i=0;i<dDriverNum;i++) {
        /* 驱动程序的名称 */
        yasdiGetDriverName(Driver[i], DriverName, sizeof(Driver));
        printf("Try to put Driver '%s' in online state...", DriverName);
        if (yasdiSetDriverOnline(Driver[i])) {
            printf("success\n");
        } else {
            printf("false\n");
        }
    }
}
}
```

```c
sscanf(DevCount, "%d",&DevCnt);
/**** 开始检测设备 ****/
printf("Searching for: %d Device(s), please wait...\n", DevCnt);

/* 执行主命令并等待... */
//DevCnt = 2;
// // 如果它没有再次执行 2 次 */
do {
    iErrorCode = yasdiDoMasterCmdEx("detect", DevCnt,0, 0 );

    if (iErrorCode < 0) // 错误?
    {
        printf("Sorry, I have found only than %d devices\ndes....(please don't beat me)\n",
            DevCnt);
        out_file=fopen("status/connect_status.txt","w");
        if(out_file==NULL)
            printf(out_file,"I found less than %d devices\n", DevCnt);
        else
            printf(" Failed to open the file \n"); // test
        fclose(out_file);
    }
}
else
{
    printf("Ok, I have found %d devices:\n", DevCnt);
    out_file=fopen("status/connect_status.txt","w");
    if(out_file==NULL)
        printf(out_file,"Ok, I have found %d devices:\n", DevCnt);
    // 如果 0==零 K...为了在 index.php 中打印
    else
        printf(" Failed to open the file \n"); // test
        fclose(out_file);
}

    detectCheck++;
}while(iErrorCode<0 && DetectCheck<3);

PrintDevList();

/* “用户界面”... */

DoCommands(DetectCheck);

/* 关闭 YASI..., 再见 * */

yasdiMasterShutdown();

return (0);
```
